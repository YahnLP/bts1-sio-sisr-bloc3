---
author: YLP
title: 📚 FICHE DE COURS 2
---

# 📚 FICHE DE COURS ÉLÈVE 2
## "Sécurité BIOS/UEFI · Secure Boot · TPM · Mots de Passe Firmware"

*BTS SIO SISR — Année 1 — Semaine 15 — Partie 2/2*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence RNCP** |
|----------|---------------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.8** | Protéger l'intégrité du démarrage système |

---

## I. La Chaîne de Démarrage Sécurisée

### I.A. BIOS vs UEFI

**Évolution du firmware :**

| **Caractéristique** | **BIOS (1975-2010)** | **UEFI (2006+)** |
|---------------------|----------------------|------------------|
| **Architecture** | 16 bits | 64 bits |
| **Limite disque** | 2,2 To (MBR) | > 2 To (GPT, jusqu'à 9,4 Zo) |
| **Partitions primaires** | 4 maximum | 128 maximum |
| **Interface** | Texte uniquement | Graphique, souris possible |
| **Vitesse démarrage** | Lent | Rapide (Fast Boot) |
| **Sécurité native** | ❌ Aucune | ✅ **Secure Boot** |
| **Réseau** | Basique (PXE) | Intégré, avancé |

**BIOS** = **B**asic **I**nput/**O**utput **S**ystem
**UEFI** = **U**nified **E**xtensible **F**irmware **I**nterface

**Obligation Windows 11** : UEFI + Secure Boot + TPM 2.0 (depuis 2021)

→ Tous les PC vendus depuis ~2012 ont UEFI
→ En 2025, le BIOS Legacy est obsolète

---

### I.B. La Chaîne de Démarrage (Boot Chain)

**DÉMARRAGE CLASSIQUE SANS SÉCURITÉ (BIOS Legacy)**

```
① Mise sous tension
    ↓
② BIOS/UEFI s'exécute (firmware stocké dans puce ROM)
    ↓
③ POST (Power-On Self-Test) : Test du matériel
    ↓
④ Recherche du périphérique de boot (ordre : HDD, USB, CD, réseau PXE...)
    ↓
⑤ Chargement du BOOTLOADER (GRUB pour Linux, Windows Boot Manager)
    ↓
⑥ Le bootloader charge le NOYAU (kernel Linux ou ntoskrnl.exe Windows)
    ↓
⑦ Le noyau charge les PILOTES (drivers)
    ↓
⑧ Démarrage du système d'exploitation
```

**⚠️ PROBLÈME DE SÉCURITÉ**

À **AUCUN** moment le firmware ne vérifie que les composants sont **authentiques** et **non modifiés**.

→ Un attaquant peut :
- Remplacer le bootloader par un **bootkit** malveillant
- Injecter un **rootkit** dans le noyau
- Le système démarre normalement, mais est **compromis dès le boot**

---

**AVEC SECURE BOOT : Chaîne de Confiance Cryptographique**

```
    UEFI possède des CLÉS PUBLIQUES de confiance
    (Microsoft, Canonical, Red Hat, fabricants...)
              ↓
    ① Le bootloader est SIGNÉ NUMÉRIQUEMENT
       par son éditeur avec sa clé privée
              ↓
    ② UEFI vérifie la SIGNATURE du bootloader
       avec la clé publique correspondante
              ↓
    ③ Signature valide ✅ → Bootloader authentique → Continue
       Signature invalide ❌ → ARRÊT DU DÉMARRAGE
              ↓
    ④ Le bootloader vérifie la signature du NOYAU
              ↓
    ⑤ Le noyau vérifie la signature des PILOTES
              ↓
    → Chaîne de confiance de bout en bout
    → Tout composant non signé = Rejeté
```

![Schéma chaîne de confiance Secure Boot]
*Légende illustration : Diagramme vertical montrant les étapes du démarrage sécurisé. En haut, puce UEFI avec cadenas (contient clés publiques Microsoft/Canonical). Flèche vers bootloader Windows avec certificat vert (signé). Flèche vers noyau Windows avec certificat vert (signé). Flèche vers pilotes avec certificat vert (signés). À côté, un bootloader malveillant avec croix rouge et message "Signature invalide - Démarrage bloqué". Utiliser couleurs : vert pour validé, rouge pour bloqué.*

---

### I.C. Secure Boot : Fonctionnement Détaillé

**Les 4 bases de données de clés dans UEFI :**

```
┌─────────────────────────────────────────────────────────────┐
│                  BASES DE DONNÉES UEFI                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ① PK (Platform Key)                                        │
│  ──────────────────────────────────────────────────────────│
│  Clé du fabricant du matériel (Dell, HP, Lenovo...)        │
│  → Contrôle qui peut modifier les autres bases de données   │
│  → Une seule clé PK, propriétaire du système                │
│                                                             │
│  ② KEK (Key Exchange Keys)                                  │
│  ──────────────────────────────────────────────────────────│
│  Clés autorisées à modifier les bases db et dbx             │
│  → Typiquement : Microsoft, fabricant matériel              │
│                                                             │
│  ③ db (Signature Database — Authorized)                    │
│  ──────────────────────────────────────────────────────────│
│  LISTE BLANCHE des certificats/hashs AUTORISÉS             │
│  → Contient les clés publiques de :                        │
│    • Microsoft (Windows Boot Manager)                      │
│    • Canonical (Ubuntu, shim.efi signé)                    │
│    • Red Hat (Fedora, RHEL)                                │
│    • SUSE, et autres éditeurs Linux                        │
│                                                             │
│  ④ dbx (Forbidden Signature Database)                      │
│  ──────────────────────────────────────────────────────────│
│  LISTE NOIRE des certificats/hashs INTERDITS               │
│  → Bootloaders compromis connus                            │
│  → Révocation de certificats (mises à jour Microsoft)      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Processus de vérification lors du boot :**

```
  Bootloader demande à démarrer
         │
         ▼
  UEFI extrait la SIGNATURE du bootloader
         │
         ▼
  ① Vérification dans dbx (blacklist)
     │
     ├─ Présent dans dbx → ❌ BLOCAGE IMMÉDIAT
     │                      "Bootloader révoqué/malveillant"
     │
     └─ Absent de dbx → Continue ↓
                │
                ▼
  ② Vérification dans db (whitelist)
     │
     ├─ Signature correspond à une clé dans db
     │  → ✅ Bootloader authentique → DÉMARRAGE
     │
     └─ Signature ne correspond à aucune clé dans db
        → ❌ BLOCAGE
           "Unauthorized bootloader detected"
           "Secure Boot Violation"
```

**Affichage en cas de blocage :**

```
╔═══════════════════════════════════════════════════════════╗
║                                                           ║
║           SECURE BOOT VIOLATION                           ║
║                                                           ║
║   An unauthorized bootloader has been detected.           ║
║   The signature of the boot file is invalid.              ║
║                                                           ║
║   Press any key to enter UEFI Setup                       ║
║                                                           ║
╚═══════════════════════════════════════════════════════════╝
```

→ L'utilisateur doit **manuellement** désactiver Secure Boot dans le BIOS/UEFI pour booter (par exemple : clé USB Linux non signé)

---

### I.D. Windows 11 et Secure Boot

**Exigences matérielles obligatoires Windows 11 (2021) :**

| **Composant** | **Exigence** |
|---------------|--------------|
| **Firmware** | UEFI (plus de BIOS Legacy) |
| **Secure Boot** | Activé |
| **TPM** | Version 2.0 minimum |
| **Processeur** | 8e génération Intel (2017+) ou Ryzen 2000+ (2018+) |
| **RAM** | 4 Go minimum |
| **Stockage** | 64 Go minimum |

**Pourquoi ces exigences ?**

- **Protection contre rootkits et bootkits** : Secure Boot bloque les malwares de bas niveau
- **Chiffrement BitLocker plus sûr** : Clés stockées dans le TPM
- **Authentification Windows Hello** : Biométrie sécurisée via TPM

**Conséquence pour le technicien IT :**

Lors du déploiement de Windows 11 en entreprise :
- ✅ Vérifier que **tous** les PC ont UEFI + Secure Boot
- ⚠️ PC < 2016 : Souvent **incompatibles** (upgrade matériel requis)
- ⚠️ PC 2016-2019 : Compatible mais Secure Boot parfois **désactivé par défaut**
  → À activer dans le BIOS/UEFI **avant** installation Windows 11

---

## II. TPM (Trusted Platform Module)

### II.A. Définition et Rôle

**TPM** = **T**rusted **P**latform **M**odule

**Définition** : Puce cryptographique dédiée (matérielle ou firmware) qui stocke de façon **sécurisée** et **isolée** :
- Clés cryptographiques (RSA, ECDSA)
- Certificats numériques
- Mots de passe
- Mesures d'intégrité du système (hashs)

**Versions :**
- **TPM 1.2** (2011) : Standard ancien, SHA-1 (obsolète, failles connues)
- **TPM 2.0** (2014) : Standard moderne, SHA-256, **obligatoire Windows 11**

**Types d'implémentation :**

| **Type** | **Description** | **Sécurité** |
|----------|-----------------|--------------|
| **dTPM** (Discrete TPM) | Puce dédiée soudée sur la carte mère | ✅✅ Maximale (isolation physique) |
| **fTPM** (Firmware TPM) / **PTT** (Intel Platform Trust Technology) | Implémenté dans le firmware du processeur | ✅ Bonne (suffit pour Win 11) |
| **sTPM** (Software TPM) | Émulé en logiciel | ❌ Faible (déconseillé) |

---

### II.B. Utilisations du TPM

**① BitLocker (chiffrement de disque Windows)**

Le TPM stocke la **clé de chiffrement** du disque.
- Clé verrouillée dans le TPM, inaccessible au système d'exploitation
- À chaque démarrage, le TPM déverrouille le disque **seulement si** le système est intègre
- Si le disque est volé et branché sur un autre PC → La clé reste verrouillée → Données illisibles

**② Windows Hello (authentification biométrique)**

Le TPM stocke les **données biométriques** (empreinte digitale, reconnaissance faciale).
- Les données ne quittent jamais le TPM
- Protection contre le vol de données biométriques

**③ Measured Boot (Démarrage Mesuré)**

À chaque étape du démarrage, le TPM :
1. Calcule le **hash SHA-256** du composant à charger (firmware, bootloader, noyau...)
2. Enregistre ce hash dans un **PCR** (Platform Configuration Register)
3. Charge le composant

**PCR** = Registres numérotés 0 à 23 dans le TPM 2.0

| **PCR** | **Contenu** |
|---------|-------------|
| PCR 0 | Firmware UEFI |
| PCR 1 | Configuration UEFI |
| PCR 4 | Bootloader (Windows Boot Manager) |
| PCR 7 | État Secure Boot (activé/désactivé) |
| PCR 11 | BitLocker Access Control |

**④ Attestation à distance (Remote Attestation)**

Le TPM peut **prouver à distance** que le système a démarré dans un état sûr.

**Scénario VPN d'entreprise :**

```
  Client VPN se connecte au serveur VPN
         ↓
  Serveur : "Prouve que tu as démarré sur un OS légitime"
         ↓
  TPM du client envoie les valeurs des PCR, signées
  par sa clé privée interne (impossible à falsifier)
         ↓
  Serveur vérifie :
  ① Les PCR correspondent aux valeurs attendues ?
  ② Secure Boot était activé ? (PCR 7)
  ③ BitLocker actif ? (PCR 11)
         ↓
  ✅ Tout conforme → Accès VPN accordé
  ❌ Non conforme → Accès VPN refusé
```

→ **Protection** contre les postes compromis (bootkits, rootkits) sur le réseau d'entreprise

---

## III. Mots de Passe BIOS/UEFI

### III.A. Les 3 Types de Mots de Passe Firmware

**① SUPERVISOR PASSWORD** (Mot de passe administrateur)

**Rôle** : Protège l'accès aux **paramètres** du BIOS/UEFI.

**Requis pour** :
- Modifier les paramètres BIOS (ordre de boot, Secure Boot, horloges...)
- Désactiver Secure Boot
- Modifier les dates/heures système
- Changer les mots de passe BIOS

**Ne bloque PAS** le démarrage du système (seulement l'accès aux réglages)

---

**② USER PASSWORD / POWER-ON PASSWORD** (Mot de passe utilisateur)

**Rôle** : Requis **AVANT** le démarrage du système.

**Fonctionnement** :
- Au démarrage, le firmware demande le mot de passe
- Sans le mot de passe → Le PC ne démarre pas
- Avec le mot de passe → Le système démarre normalement

**Protège contre** :
- Utilisation non autorisée du PC (vol de PC)
- Accès physique au système (quelqu'un branche votre PC)

**⚠️ Limite** : Ne protège PAS les données sur le disque si on retire le disque et on le branche sur un autre PC

---

**③ HDD/SSD PASSWORD** (Mot de passe disque dur)

**Rôle** : Mot de passe stocké **DANS** le contrôleur du disque dur/SSD (matériel).

**Fonctionnement** :
- Le disque refuse de démarrer sans le bon mot de passe
- **Même** si on retire le disque et on le branche sur un autre PC → Le disque reste **verrouillé**

**Protection maximale** contre le vol de données

**⚠️ ATTENTION CRITIQUE** :
- Mot de passe oublié = Disque **INUTILISABLE** définitivement
- **Aucune** récupération possible (pas de master password)
- Les données sont **perdues** à jamais

→ À utiliser uniquement pour des données **ultra-sensibles** et avec un gestionnaire de mots de passe fiable

---

### III.B. Configuration et Bonnes Pratiques

**Procédure de configuration (générale) :**

```
① Démarrer le PC et appuyer sur la touche BIOS
   (varie selon le fabricant, affiché au boot)

   Dell     : F2
   HP       : F10 ou Échap puis F10
   Lenovo   : F1 ou F2
   ASUS     : F2 ou Suppr
   MSI      : Suppr
   Gigabyte : Suppr

② Naviguer dans le menu Security (ou Advanced)

③ Définir **Supervisor Password**
   → Entrer le mot de passe (12+ caractères recommandés)
   → Confirmer le mot de passe

④ (Optionnel) Définir **User Password** si requis (postes nomades)

⑤ Enregistrer et quitter
   → F10 ou "Save and Exit"
   → Confirmer

À la prochaine entrée dans le BIOS :
→ Le mot de passe Supervisor sera demandé
```

---

**Bonnes pratiques en entreprise :**

| **Pratique** | **Justification** |
|--------------|-------------------|
| ✅ Toujours définir un **Supervisor Password** | Empêche un utilisateur de désactiver Secure Boot |
| ✅ Gestionnaire de mots de passe professionnel | KeePass, 1Password, Bitwarden avec chiffrement |
| ✅ Documenter les MDP dans un **coffre-fort sécurisé** | Accessible uniquement à l'équipe IT |
| ✅ Pour postes **nomades** : User Password obligatoire | Protection vol de laptop |
| ✅ Désactiver le **boot sur USB** | Éviter les bootkits via clé USB malveillante |
| ✅ Activer **Secure Boot** systématiquement | Protection bootkits/rootkits |
| ✅ Vérifier **TPM activé** (Windows 11, BitLocker) | Prérequis obligatoire |

---

**Récupération en cas de perte du mot de passe :**

| **Type de PC** | **Procédure** |
|----------------|---------------|
| **PC grand public** (Dell, HP, Lenovo) | Contacter le support avec **preuve d'achat** → Master password fourni (unique par machine basé sur Service Tag) |
| **PC professionnel** (Dell OptiPlex, HP EliteBook) | Code de récupération via le support fabricant avec email corporate |
| **Dernière option** | Reset matériel (retirer pile CMOS 10 min) ⚠️ Ne fonctionne **pas** toujours sur UEFI moderne ⚠️ Efface **tous** les paramètres BIOS |

---

## IV. Attaques Contre le Firmware

### IV.A. Menaces Principales

**① EVIL MAID ATTACK** (Attaque de la Femme de Chambre)

**Scénario** :
1. Vous laissez votre laptop dans une chambre d'hôtel (ou au bureau)
2. Un attaquant y accède **physiquement** pendant votre absence (5 minutes suffisent)
3. Il boot sur une **clé USB malveillante**
4. Il installe un **bootkit** ou un **keylogger matériel** (USB interne)
5. Vous revenez, rien ne semble changé extérieurement
6. Le bootkit capture vos mots de passe **BitLocker**, **VPN**, sessions...

**Nom** : Référence aux femmes de chambre d'hôtel (accès physique aux chambres)

**CONTRE-MESURE** :
- ✅ **Secure Boot** activé (blocage des bootloaders non signés)
- ✅ **User Password BIOS** (impossible de booter sans MDP)
- ✅ **Boot uniquement sur HDD interne** (USB boot désactivé)
- ✅ TPM + BitLocker (détecte les modifications matérielles)

---

**② BOOTKIT / ROOTKIT UEFI**

**Définition** : Malware qui s'installe **DANS** le firmware UEFI lui-même (pas seulement sur le disque).

**Caractéristiques** :
- ✅ Persiste **même après** réinstallation complète de Windows
- ✅ Invisible pour l'antivirus (s'exécute **AVANT** le système d'exploitation)
- ✅ Très difficile à détecter et supprimer (nécessite reflash firmware)

**Exemples réels** :

| **Nom** | **Année** | **Origine** | **Description** |
|---------|-----------|-------------|-----------------|
| **LoJax** | 2018 | APT Sednit/Fancy Bear (Russie) | Premier rootkit UEFI in-the-wild découvert (Kaspersky) |
| **MosaicRegressor** | 2020 | APT inconnu | Rootkit UEFI ciblant diplomates et ONG |
| **MoonBounce** | 2022 | APT41 (Chine) | Implant UEFI découvert par Kaspersky |

**CONTRE-MESURE** :
- ✅ **Secure Boot** (empêche chargement firmware non signé)
- ✅ **Firmware updates réguliers** (patchs de sécurité fabricant)
- ✅ Acheter matériel professionnel de distributeurs agréés (pas de firmware pré-infecté)

---

**③ FIRMWARE MALVEILLANT PRÉ-INSTALLÉ**

**Scénario** : PC acheté sur un site douteux (revendeur non officiel, marketplace) avec firmware déjà **compromis** à la sortie d'usine.

**CONTRE-MESURE** :
- ✅ Acheter du matériel professionnel auprès de **distributeurs agréés** uniquement (Dell Direct, HP Official, Lenovo...)
- ✅ Vérifier l'intégrité du firmware à réception (hash SHA-256 vs site fabricant)

---

**④ DOWNGRADE ATTACK**

**Scénario** : Réinstaller une **ancienne version** du firmware UEFI contenant des **vulnérabilités connues** (déjà patchées).

**Fonctionnement** :
1. Attaquant force un downgrade du firmware
2. Exploite une faille de sécurité de l'ancienne version
3. Installe un rootkit

**CONTRE-MESURE** :
- ✅ **UEFI Capsule Update** avec **rollback protection** (vérification de version)
- ✅ Firmware doit vérifier que la nouvelle version est ≥ version actuelle

---

## V. Vocabulaire Clé à Maîtriser

| **Terme** | **Définition** |
|-----------|----------------|
| **BIOS** | Basic Input/Output System — Firmware historique (16 bits, MBR, non sécurisé) |
| **UEFI** | Unified Extensible Firmware Interface — Firmware moderne (64 bits, GPT, Secure Boot) |
| **Secure Boot** | Mécanisme UEFI vérifiant la signature numérique de chaque composant de la chaîne de démarrage |
| **Boot chain** | Chaîne de démarrage (firmware → bootloader → noyau → pilotes → OS) |
| **Bootloader** | Programme chargeant le noyau (GRUB pour Linux, Windows Boot Manager) |
| **Bootkit** | Malware s'exécutant au niveau du bootloader (avant l'OS) |
| **Rootkit** | Malware masquant sa présence en s'intégrant profondément dans le système |
| **TPM** | Trusted Platform Module — Puce cryptographique stockant clés et mesures d'intégrité |
| **Measured Boot** | Enregistrement des empreintes (hashs SHA-256) de chaque étape du boot dans les PCR du TPM |
| **PCR** | Platform Configuration Register — Registres TPM (0-23) stockant les hashs d'intégrité |
| **db** | Signature Database UEFI — Liste blanche des certificats/hashs autorisés |
| **dbx** | Forbidden Signature Database UEFI — Liste noire des certificats révoqués |
| **PK** | Platform Key — Clé unique du fabricant contrôlant les autres bases UEFI |
| **KEK** | Key Exchange Keys — Clés autorisées à modifier db et dbx |
| **Supervisor Password** | Mot de passe BIOS protégeant l'accès aux paramètres firmware |
| **User Password** | Mot de passe requis avant le démarrage du système |
| **HDD Password** | Mot de passe matériel du disque (verrouillage dans le contrôleur HDD/SSD) |
| **Evil Maid Attack** | Attaque par accès physique au PC laissé sans surveillance (installation bootkit via USB) |
| **Attestation à distance** | Mécanisme TPM prouvant à un serveur distant que le système a démarré de façon sûre |
| **dTPM / fTPM / sTPM** | Types d'implémentation TPM : Discrete (puce) / Firmware / Software |

---
