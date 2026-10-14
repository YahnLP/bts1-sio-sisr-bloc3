---
author: YLP
title: 📚 FICHE DE COURS
---


# 📚 FICHE DE COURS ÉLÈVE
## "Droits d'Accès · Principe du Moindre Privilège · Modèles d'Accès"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 10*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.4** | Gérer les accès et les droits des utilisateurs |

---

## PARTIE I — Authentification vs Autorisation

### I.A. Deux Concepts Distincts

```
   AUTHENTIFICATION vs AUTORISATION
   ═══════════════════════════════════════════════════════════════

   AUTHENTIFICATION (Qui êtes-vous ?)
   ──────────────────────────────────────────────────────────────
   Vérifier l'IDENTITÉ d'un utilisateur

   Méthodes :
   • Mot de passe (ce que je sais)
   • Badge / clé (ce que j'ai)
   • Empreinte / Face ID (ce que je suis)
   • MFA = Combinaison de plusieurs facteurs

   Analogie : Montrer sa CARTE D'IDENTITÉ à l'entrée

   Résultat : L'utilisateur est reconnu → Session ouverte


   AUTORISATION (Que pouvez-vous faire ?)
   ──────────────────────────────────────────────────────────────
   Vérifier les DROITS d'un utilisateur authentifié

   Questions posées par le système :
   • L'utilisateur peut-il LIRE ce fichier ?
   • L'utilisateur peut-il MODIFIER cette base de données ?
   • L'utilisateur peut-il SUPPRIMER cet enregistrement ?
   • L'utilisateur peut-il EXÉCUTER ce programme ?

   Analogie : Votre badge d'entrée OUVRE certaines portes
              mais PAS d'autres (même si vous êtes identifié)

   Résultat : Accès accordé ou refusé selon les droits

   ──────────────────────────────────────────────────────────────
   ORDRE OBLIGATOIRE : Authentification → PUIS → Autorisation
   ──────────────────────────────────────────────────────────────
```

---

## PARTIE II — Le Principe du Moindre Privilège

### II.A. Définition

**Principe du Moindre Privilège** (Least Privilege Principle) :

> *Un utilisateur, un programme ou un processus ne doit disposer que des droits strictement nécessaires à l'accomplissement de sa mission, ni plus, ni moins.*

**Origine :** Principe fondateur de la sécurité informatique, formulé par Jerome Saltzer et Michael Schroeder (MIT, 1975). Toujours d'actualité 50 ans après.

---

### II.B. Pourquoi ce Principe est-il Critique ?

```
   SCÉNARIO SANS MOINDRE PRIVILÈGE
   ═══════════════════════════════════════════════════════════════

   Entreprise de 50 personnes.
   Tous les salariés ont un accès "Administrateur" sur leur PC
   (plus pratique pour installer des logiciels...)

   MARDI 14H : Le comptable ouvre un email de phishing.
   ──────────────────────────────────────────────────────────────
   → Il clique sur la pièce jointe
   → Le malware s'exécute... avec les droits ADMINISTRATEUR
   → Le malware peut :
     • S'installer dans les dossiers système (C:\Windows\System32)
     • Désactiver l'antivirus
     • Modifier les paramètres système
     • Se propager sur le réseau avec les droits admin
     • Chiffrer TOUS les fichiers accessibles (ransomware)

   AVEC MOINDRE PRIVILÈGE :
   ──────────────────────────────────────────────────────────────
   → Le comptable a des droits LIMITÉS (utilisateur standard)
   → Le malware s'exécute avec les droits limités du comptable
   → Il NE PEUT PAS :
     • S'installer dans les dossiers système
     • Désactiver l'antivirus (droits insuffisants)
     • Modifier les paramètres système
   → Impact CONTENU au profil de l'utilisateur uniquement
   → Pas de propagation (pas de droits réseau admin)
```

**La règle d'or :**

```
   DROITS = BESOIN MÉTIER RÉEL (ni plus, ni moins)
   ═══════════════════════════════════════════════════════════════

   ❌ "Il vaut mieux lui donner trop de droits que pas assez"
      → C'est l'erreur la plus commune et la plus dangereuse

   ✅ "Il obtient exactement les droits dont il a besoin"
      → Si besoin de droits supplémentaires → Demande formelle

   ❌ "Il était admin avant, autant le laisser admin"
      → Les droits doivent évoluer avec le poste

   ✅ "Il a changé de poste → Revue et adaptation des droits"
```

---

### II.C. Applications Concrètes du Moindre Privilège

```
   EXEMPLES PAR RÔLE EN ENTREPRISE
   ═══════════════════════════════════════════════════════════════

   RÔLE                 │ DROITS APPROPRIÉS
   ─────────────────────┼──────────────────────────────────────────
   Commercial           │ Lecture/Écriture sur /Clients/
                        │ Lecture sur /Produits/
                        │ ❌ Pas /Comptabilité/ ni /RH/

   Comptable            │ Lecture/Écriture sur /Comptabilité/
                        │ Lecture sur /Clients/ (facturation)
                        │ ❌ Pas /RH/ ni /Développement/

   Développeur          │ Lecture/Écriture sur /Dev/ (projet assigné)
                        │ Lecture sur /Dev/ (autres projets)
                        │ ❌ Pas /Comptabilité/ ni /Production/

   DRH                  │ Lecture/Écriture sur /RH/
                        │ ❌ Pas /Comptabilité/ ni /Dev/

   Technicien IT        │ Admin système (installation, config)
                        │ Lecture logs sur tous les serveurs
                        │ ❌ Pas de lecture /RH/ ni /Comptabilité/
                        │ (sauf incident documenté)

   Stagiaire            │ Lecture uniquement sur dossier projet
                        │ ❌ Rien d'autre

   PRINCIPES ASSOCIÉS
   ──────────────────────────────────────────────────────────────
   • Séparation des tâches : Deux personnes pour valider une action
     sensible (ex : comptable saisit, directeur approuve)
   • Rotation des rôles : Éviter qu'une personne accumule les droits
   • Révocation immédiate : Départ salarié = désactivation le jour J
```

---

## PARTIE III — Les Modèles de Contrôle d'Accès

### III.A. DAC — Discretionary Access Control

**Contrôle d'accès discrétionnaire**

```
   DAC — PRINCIPE
   ═══════════════════════════════════════════════════════════════

   Le PROPRIÉTAIRE du fichier décide qui peut y accéder.

   Fonctionnement :
   → Sophie crée un fichier → Sophie est propriétaire
   → Sophie choisit : "Marc peut lire, Julie peut lire et écrire"
   → Marc et Julie ont accès selon le choix de Sophie

   IMPLÉMENTATION
   ──────────────────────────────────────────────────────────────
   Windows NTFS (clic droit → Propriétés → Sécurité)
   Linux : chmod / chown

   AVANTAGES                    INCONVÉNIENTS
   ──────────────────────       ──────────────────────────────
   ✅ Simple et flexible         ❌ Peu adapté aux grandes structures
   ✅ L'utilisateur contrôle     ❌ Difficile à auditer globalement
   ✅ Pas besoin d'admin         ❌ Risque : Utilisateur peut accorder
      pour chaque modification     des droits à n'importe qui

   USAGE TYPIQUE
   ──────────────────────────────────────────────────────────────
   • PME simple
   • Partages de fichiers entre collègues de confiance
   • Environnements peu réglementés
```

---

### III.B. MAC — Mandatory Access Control

**Contrôle d'accès obligatoire**

```
   MAC — PRINCIPE
   ═══════════════════════════════════════════════════════════════

   L'ADMINISTRATEUR (ou le système) définit centralement les droits.
   Les utilisateurs NE PEUVENT PAS modifier les permissions.

   Fonctionnement basé sur des NIVEAUX DE CLASSIFICATION :
   ────────────────────────────────────────────────────────
   NIVEAU 4 : TOP SECRET     → Accès : Directeurs uniquement
   NIVEAU 3 : SECRET         → Accès : Cadres + Directeurs
   NIVEAU 2 : CONFIDENTIEL   → Accès : Tous les employés permanents
   NIVEAU 1 : PUBLIC         → Accès : Tous (y compris stagiaires)

   Règle : Un utilisateur de niveau N peut accéder
           aux données de niveau ≤ N
           (Pas d'accès aux données de niveau supérieur)

   AVANTAGES                    INCONVÉNIENTS
   ──────────────────────       ──────────────────────────────
   ✅ Très sécurisé              ❌ Rigide et complexe à gérer
   ✅ Contrôle centralisé        ❌ Déploiement coûteux
   ✅ Audit simplifié            ❌ Peu adapté au secteur privé

   USAGE TYPIQUE
   ──────────────────────────────────────────────────────────────
   • Défense nationale / renseignement
   • Secteur militaire
   • Environnements haute sécurité (nucléaire)
   • OS : SELinux (Linux), Trusted Solaris
```

---

### III.C. RBAC — Role-Based Access Control ⭐

**Contrôle d'accès basé sur les rôles**

> Le modèle **le plus utilisé en entreprise**. C'est celui que les apprenants configureront en alternance.

```
   RBAC — PRINCIPE
   ═══════════════════════════════════════════════════════════════

   Les droits sont attribués à des RÔLES.
   Les utilisateurs reçoivent un ou plusieurs RÔLES.
   → Modification de rôle = Modification automatique des droits

   STRUCTURE
   ──────────────────────────────────────────────────────────────

   RÔLES (définissent les droits)
   ├── Rôle "Commercial"      → /Clients/ L+E, /Produits/ L
   ├── Rôle "Comptable"       → /Comptabilité/ L+E, /Clients/ L
   ├── Rôle "DRH"             → /RH/ L+E
   ├── Rôle "Développeur"     → /Dev/ L+E
   └── Rôle "Admin IT"        → Tout en administration

   UTILISATEURS (reçoivent des rôles)
   ├── Sophie MARTIN    → Rôle "Commercial"
   ├── Marc DUPONT      → Rôle "Comptable"
   ├── Julie BERNARD    → Rôle "DRH"
   └── Pierre LEFEBVRE  → Rôle "Développeur" + "Commercial"
                          (double mission → double rôle)

   AVANTAGES                    INCONVÉNIENTS
   ──────────────────────       ──────────────────────────────
   ✅ Facile à gérer             ❌ Risque "role explosion"
      (modifier le rôle =           (trop de rôles différents)
      modifier tous les users)
   ✅ Auditabilité claire        ❌ Droits individuels limités
   ✅ Onboarding rapide
   ✅ Scalable (1 → 10 000)

   IMPLÉMENTATION
   ──────────────────────────────────────────────────────────────
   Windows Active Directory :
   → Groupes de sécurité AD = Rôles RBAC
   → Utilisateur rejoint le groupe → Droits automatiques

   Linux :
   → Groupes Linux (addgroup, usermod -aG)

   Applications web :
   → Table roles + Table user_roles en base de données
```

---

## PARTIE IV — La Matrice de Droits (ACL)

### IV.A. Définition et Structure

**Matrice de droits** (ou **matrice d'habilitation** ou **ACL — Access Control List**) :

> Tableau à double entrée listant les **utilisateurs** (ou groupes) en ligne et les **ressources** (ou fonctionnalités) en colonne, avec le **niveau d'accès** à l'intersection.

```
   STRUCTURE DE BASE
   ═══════════════════════════════════════════════════════════════

   CODES D'ACCÈS STANDARDS
   ──────────────────────────────────────────────────────────────
   — (tiret)  : Aucun accès
   L          : Lecture seule (Read)
   L+E        : Lecture + Écriture (Read + Write)
   L+E+S      : Lecture + Écriture + Suppression (Full Write)
   A          : Accès total (Admin/Full Control)
   X          : Exécution uniquement (scripts, programmes)

   EXEMPLE DE MATRICE SIMPLE
   ──────────────────────────────────────────────────────────────

                  │/Clients/│/Compta/│/RH/ │/Dev/│/Système/
   ───────────────┼─────────┼────────┼─────┼─────┼─────────
   G_Commercial   │  L+E    │   —    │  —  │  —  │   —
   G_Comptable    │   L     │  L+E   │  —  │  —  │   —
   G_DRH          │   —     │   —    │ L+E │  —  │   —
   G_Dev          │   —     │   —    │  —  │ L+E │   —
   G_Directeur    │   L     │   L    │  L  │  L  │   —
   G_Admin_IT     │   —     │   —    │  —  │  —  │   A
   G_Tous         │   —     │   —    │  —  │  —  │   —
   ───────────────┴─────────┴────────┴─────┴─────┴─────────

   → G_Directeur a L sur tous (vision globale sans modification)
   → G_Admin_IT a A sur /Système/ mais PAS sur les données métier
     (Technicien IT NE LIT PAS les salaires ou données clients)
   → G_Tous = Aucun droit (droits explicites obligatoires)
```

---

### IV.B. Matrice Complète avec Niveaux Fins

```
   MATRICE DE DROITS — EXEMPLE PME COMPLET
   ═══════════════════════════════════════════════════════════════

   LÉGENDE :
   — = Aucun accès
   L = Lecture
   E = Écriture
   S = Suppression
   A = Administration (tous droits)
   Les cellules combinées : L+E = Lecture ET Écriture

                     │ Clients │ Compta │ Paie  │  RH   │  Dev  │ Sauv. │ Logs
   ──────────────────┼─────────┼────────┼───────┼───────┼───────┼───────┼──────
   G_Direction       │   L     │   L    │   L   │   L   │   —   │   —   │  —
   G_Commercial      │  L+E    │   —    │   —   │   —   │   —   │   —   │  —
   G_Comptable       │   L     │  L+E+S │  L+E  │   —   │   —   │   —   │  —
   G_DRH             │   —     │   —    │  L+E  │  L+E+S│   —   │   —   │  —
   G_Dev_Senior      │   —     │   —    │   —   │   —   │  L+E+S│   —   │  —
   G_Dev_Junior      │   —     │   —    │   —   │   —   │  L+E  │   —   │  —
   G_Stagiaire       │   —     │   —    │   —   │   —   │   L   │   —   │  —
   G_Admin_IT        │   —     │   —    │   —   │   —   │   —   │   A   │  L+E
   G_RSSI            │   —     │   —    │   —   │   —   │   L   │   L   │  L+E+S
   ──────────────────┴─────────┴────────┴───────┴───────┴───────┴───────┴──────

   POINTS CLÉS DE CETTE MATRICE :
   ──────────────────────────────────────────────────────────────
   → G_Dev_Junior : L+E mais PAS Suppression (pas de droit détruire)
   → G_Dev_Senior : L+E+S (peut gérer la suppression du code)
   → G_Stagiaire : Lecture uniquement sur /Dev/ (pas d'écriture)
   → G_Admin_IT : Admin sauvegardes ET logs, mais ZÉRO accès données
   → G_RSSI : Lecture sur tout (audit) mais NE MODIFIE RIEN
   → G_DRH : Accès paie ET RH (les deux dossiers liés)
   → G_Direction : Lecture seule sur tout (vision stratégique)
```

---

### IV.C. Revue Périodique des Droits

**La matrice de droits est un document VIVANT.**

```
   CYCLE DE GESTION DES DROITS
   ═══════════════════════════════════════════════════════════════

   ÉVÉNEMENTS DÉCLENCHEURS DE MODIFICATION
   ──────────────────────────────────────────────────────────────
   ① ARRIVÉE (Onboarding)
   → Créer le compte, assigner les groupes selon le rôle
   → Fiche d'arrivée signée par le manager (liste des accès requis)

   ② CHANGEMENT DE POSTE
   → Retirer les anciens droits (rôle précédent)
   → Ajouter les nouveaux droits (nouveau rôle)
   → Principe : Jamais d'accumulation de droits

   ③ DÉPART (Offboarding) — CRITIQUE
   → DÉSACTIVER le compte LE JOUR DU DÉPART (pas "la semaine prochaine")
   → Révoquer tous les accès (VPN, email, apps cloud, AD)
   → Transférer les données si nécessaire
   → Conserver le compte désactivé 30 jours puis supprimer

   ④ REVUE PÉRIODIQUE (tous les 6 mois)
   → Parcourir la matrice avec les managers
   → "Untel a-t-il encore besoin de ce droit ?"
   → Supprimer les droits inutilisés (audit des logs d'accès)
   → Documenter la revue (date, participants, actions)

   INDICATEUR ROUGE : DROIT JAMAIS UTILISÉ
   ──────────────────────────────────────────────────────────────
   Si un utilisateur a le droit de lire /Comptabilité/ mais
   n'y a jamais accédé en 6 mois → Supprimer ce droit
   → Logs d'accès : Requête SQL sur la table d'audit
     SELECT user, resource, COUNT(*) as nb_acces
     FROM access_log
     WHERE date > DATE_SUB(NOW(), INTERVAL 6 MONTH)
     GROUP BY user, resource
     ORDER BY nb_acces ASC
```

---

## PARTIE V — Implémentation Technique

### V.A. Windows Active Directory (RBAC avec Groupes)

```
   IMPLÉMENTATION AD — RBAC PAR GROUPES DE SÉCURITÉ
   ═══════════════════════════════════════════════════════════════

   ÉTAPE 1 — Créer les groupes (= Rôles RBAC)
   ──────────────────────────────────────────────────────────────
   Dans Active Directory Users and Computers (ADUC) :

   Créer dans l'OU "Groupes_Securite" :
   • GS_Commercial
   • GS_Comptable
   • GS_DRH
   • GS_Dev_Junior
   • GS_Dev_Senior
   • GS_Admin_IT

   PowerShell :
   New-ADGroup -Name "GS_Commercial" `
     -GroupScope Global `
     -GroupCategory Security `
     -Path "OU=Groupes_Securite,DC=entreprise,DC=local"

   ÉTAPE 2 — Ajouter les utilisateurs aux groupes
   ──────────────────────────────────────────────────────────────
   PowerShell :
   Add-ADGroupMember -Identity "GS_Commercial" `
     -Members "s.martin", "j.dubois", "a.petit"

   ÉTAPE 3 — Configurer les droits NTFS sur les dossiers partagés
   ──────────────────────────────────────────────────────────────
   PowerShell :
   # Dossier /Clients/ — GS_Commercial : Modifier (L+E)
   $acl = Get-Acl "\\SERVEUR\Données\Clients"
   $rule = New-Object System.Security.AccessControl.FileSystemAccessRule(
     "ENTREPRISE\GS_Commercial",
     "Modify",      # Lecture + Écriture (pas Suppression)
     "ContainerInherit,ObjectInherit",
     "None",
     "Allow"
   )
   $acl.SetAccessRule($rule)
   Set-Acl "\\SERVEUR\Données\Clients" $acl

   NIVEAUX NTFS COURANTS
   ──────────────────────────────────────────────────────────────
   • FullControl     = L+E+S + Droits (Admin complet)
   • Modify          = L+E + Suppression des propres fichiers
   • ReadAndExecute  = Lecture + Exécution (pas d'écriture)
   • Write           = Écriture seulement (pas lecture !)
   • Read            = Lecture seule
   • ListDirectory   = Voir le contenu du dossier uniquement

   ÉTAPE 4 — Désactiver un compte lors d'un départ
   ──────────────────────────────────────────────────────────────
   PowerShell :
   Disable-ADAccount -Identity "prenom.nom"
   Move-ADObject -Identity "CN=Prenom Nom,OU=Utilisateurs,..." `
     -TargetPath "OU=Comptes_Desactives,DC=entreprise,DC=local"
```

---

### V.B. Linux (Permissions et Groupes)

```
   IMPLÉMENTATION LINUX — DROITS ET GROUPES
   ═══════════════════════════════════════════════════════════════

   RAPPEL PERMISSIONS LINUX
   ──────────────────────────────────────────────────────────────
   -rwxr-xr-- 1 sophie comptable 1024 mars 15 fichier.txt
    │││││││││
    ││││││└└└─ Autres (r = lecture, - = pas écriture, - = pas exéc.)
    │││└└└──── Groupe (r = lecture, - = pas écriture, x = exéc.)
    └└└──────── Propriétaire (r+w+x = lecture, écriture, exécution)

   CODES NUMÉRIQUES (chmod)
   ──────────────────────────────────────────────────────────────
   4 = Lecture (r)
   2 = Écriture (w)
   1 = Exécution (x)
   0 = Aucun droit (-)

   chmod 750 dossier → Propriétaire: 7(r+w+x), Groupe: 5(r+x), Autres: 0

   GESTION DES GROUPES
   ──────────────────────────────────────────────────────────────
   # Créer un groupe
   groupadd gs_commercial

   # Créer un utilisateur et l'assigner au groupe
   useradd -m -G gs_commercial sophie.martin
   usermod -aG gs_commercial jean.durand

   # Appliquer les droits sur un dossier
   chown -R :gs_commercial /data/clients/
   chmod -R 770 /data/clients/
   # 770 → Propriétaire: rwx, Groupe: rwx, Autres: ---

   # Vérifier les membres d'un groupe
   getent group gs_commercial

   # Supprimer un utilisateur d'un groupe (départ)
   gpasswd -d prenom.nom gs_commercial

   SUDO — ACCÈS ADMINISTRATEUR CONTRÔLÉ
   ──────────────────────────────────────────────────────────────
   # /etc/sudoers — Donner des droits ciblés sans accès root total
   # Technicien IT peut redémarrer les services Apache uniquement :
   technicien_it ALL=(root) NOPASSWD: /usr/bin/systemctl restart apache2

   # Comptable peut lire les logs uniquement :
   comptable_user ALL=(root) NOPASSWD: /usr/bin/journalctl -u mysql
```

---

## VI. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Authentification** | Vérification de l'identité d'un utilisateur (Qui êtes-vous ?) |
| **Autorisation** | Vérification des droits d'un utilisateur authentifié (Que pouvez-vous faire ?) |
| **Moindre privilège** | Principe : Donner uniquement les droits strictement nécessaires à la mission |
| **DAC** | Discretionary Access Control — Le propriétaire définit les droits |
| **MAC** | Mandatory Access Control — Le système définit des niveaux de classification |
| **RBAC** | Role-Based Access Control — Les droits sont liés à des rôles, pas à des individus |
| **Matrice de droits** | Tableau croisant utilisateurs/groupes et ressources avec le niveau d'accès |
| **ACL** | Access Control List — Liste de contrôle d'accès implémentant la matrice |
| **NTFS** | New Technology File System — Système de fichiers Windows permettant les ACL |
| **Groupe de sécurité AD** | Objet Active Directory regroupant des utilisateurs pour leur attribuer des droits |
| **Onboarding** | Processus d'arrivée d'un collaborateur, incluant la création de son compte et droits |
| **Offboarding** | Processus de départ d'un collaborateur, incluant la désactivation immédiate du compte |
| **Revue des droits** | Audit périodique (6 mois) vérifiant que chaque droit est toujours nécessaire |
| **Séparation des tâches** | Principe : Deux personnes pour valider une action sensible (éviter fraude interne) |

---