---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Supports Amovibles · Risques · Bonnes Pratiques"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 4*

---

## PARTIE VI — Types de Supports Amovibles

### VI.A. Clé USB (Flash Drive)

```
   CLÉ USB
   ═══════════════════════════════════════════════════════════════
   
   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   • Capacité : 8 Go - 1 To
   • Prix : 10-150 €
   • Vitesse : 20-500 Mo/s (USB 2.0 à USB 3.2)
   • Durée de vie : 10 000-100 000 cycles écriture
   
   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Petite, portable
   ✅ Plug & Play (aucun pilote)
   ✅ Compatible tous OS
   ✅ Bon marché
   
   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ Facilement perdue
   ❌ Durée de vie limitée
   ❌ Vecteur de malware (USB drop attack)
   ❌ Peut corrompre sans prévenir
   
   USAGE RECOMMANDÉ
   ──────────────────────────────────────────────────────────────
   • Transfert temporaire de fichiers
   • Installation système (ISO bootable)
   • PAS pour stockage long terme
   • PAS pour sauvegarde unique
```

---

### VI.B. Disque Dur Externe (HDD)

```
   DISQUE DUR EXTERNE (HDD)
   ═══════════════════════════════════════════════════════════════
   
   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   • Capacité : 1 To - 20 To
   • Prix : 50-400 €
   • Vitesse : 100-150 Mo/s
   • Durée de vie : 5-10 ans
   • Technologie : Plateaux magnétiques rotatifs
   
   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Grande capacité
   ✅ Bon rapport capacité/prix
   ✅ Fiable pour archivage
   
   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ Fragile (chocs = mort)
   ❌ Plus lent qu'un SSD
   ❌ Bruit (moteur, têtes de lecture)
   ❌ Consommation électrique
   
   USAGE RECOMMANDÉ
   ──────────────────────────────────────────────────────────────
   ✅ Sauvegarde régulière (Time Machine, Windows Backup)
   ✅ Archivage long terme (photos, vidéos)
   ✅ Copie hors site (à débrancher après sauvegarde)
```

---

### VI.C. SSD Externe

```
   SSD EXTERNE
   ═══════════════════════════════════════════════════════════════
   
   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   • Capacité : 250 Go - 8 To
   • Prix : 80-1000 €
   • Vitesse : 500-2000 Mo/s (NVMe)
   • Durée de vie : 5-7 ans (selon usage)
   • Technologie : Mémoire flash NAND
   
   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Très rapide (3-10× HDD)
   ✅ Résistant aux chocs (pas de pièces mobiles)
   ✅ Silencieux
   ✅ Compact et léger
   
   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ Cher (€/Go)
   ❌ Durée de vie limitée (usure cellules)
   ❌ Perte de données si non alimenté longtemps (> 1 an)
   
   USAGE RECOMMANDÉ
   ──────────────────────────────────────────────────────────────
   ✅ Sauvegarde quotidienne rapide
   ✅ Transfert gros fichiers (vidéo 4K)
   ⚠️ PAS pour archivage très long terme non alimenté
```

---

### VI.D. NAS (Network Attached Storage)

```
   NAS
   ═══════════════════════════════════════════════════════════════
   
   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   • Capacité : 2-100 To (selon nombre de disques)
   • Prix : 200-3000 € (NAS + disques)
   • Vitesse : 100-1000 Mo/s (selon réseau)
   • RAID : Redondance des données (RAID 1, 5, 6, 10)
   
   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Accessible par le réseau (plusieurs PC)
   ✅ Toujours allumé (sauvegarde auto)
   ✅ RAID = protection panne disque
   ✅ Évolutif (ajouter disques)
   
   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ Coût initial élevé
   ❌ Complexité configuration
   ❌ Consommation électrique continue
   ❌ Pas "hors site" (même lieu)
   
   USAGE RECOMMANDÉ
   ──────────────────────────────────────────────────────────────
   ✅ PME : sauvegarde centralisée
   ✅ Famille : stockage photos/vidéos partagé
   ✅ DOIT être complété par sauvegarde cloud (règle 3-2-1)
```

---

## PARTIE VII — Risques des Supports Amovibles

### VII.A. Perte et Vol

```
   STATISTIQUES
   ═══════════════════════════════════════════════════════════════
   
   • 1 clé USB perdue toutes les 6 secondes dans le monde
   • 25% des employés ont déjà perdu une clé USB professionnelle
   • 60% des clés USB perdues contiennent des données sensibles
   
   CONSÉQUENCES
   ──────────────────────────────────────────────────────────────
   ❌ Perte de données
   ❌ Fuite d'informations confidentielles
   ❌ Vol d'identité
   ❌ Amende RGPD (jusqu'à 20 M€ ou 4% CA)
   
   CAS RÉEL : British Airways (2018)
   ──────────────────────────────────────────────────────────────
   Un disque dur externe contenant les données de 380 000 clients
   a été volé dans une voiture.
   
   Données : Noms, adresses, numéros de cartes bancaires
   
   Conséquence : Amende RGPD de 183 M£ (réduite à 20 M£ en appel)
```

---

### VII.B. Malware (Vecteur d'Infection)

```
   USB = VECTEUR PRIVILÉGIÉ DES MALWARES
   ═══════════════════════════════════════════════════════════════
   
   ATTAQUE "USB DROP"
   ──────────────────────────────────────────────────────────────
   L'attaquant abandonne des clés USB infectées dans :
   • Parkings d'entreprise
   • Cafétérias
   • Salles d'attente
   
   Étiquettes attrayantes : "Salaires 2024", "Confidentiel"
   
   Taux de réussite : 45% des clés sont branchées
                      (étude Université Illinois 2016)
   
   AUTORUN / AUTOPLAY
   ──────────────────────────────────────────────────────────────
   Fonctionnalité Windows qui exécute automatiquement un programme
   quand une clé USB est branchée.
   
   ⚠️ Désactivé par défaut depuis Windows 7, mais peut être réactivé
   
   STUXNET (2010)
   ──────────────────────────────────────────────────────────────
   Ver informatique propagé par clé USB pour attaquer les
   centrifugeuses nucléaires iraniennes.
   
   Infectait les clés USB, puis se propageait aux PC déconnectés
   d'Internet (air gap bypass).
```

---

### VII.C. Corruption et Défaillance

```
   CAUSES DE CORRUPTION
   ═══════════════════════════════════════════════════════════════
   
   ① DÉBRANCHEMENT BRUTAL
   ──────────────────────────────────────────────────────────────
   Arracher la clé USB pendant une écriture
   → Corruption du système de fichiers
   → Fichiers illisibles ou perdus
   
   ② CYCLES D'ÉCRITURE ÉPUISÉS
   ──────────────────────────────────────────────────────────────
   Clé USB : 10 000-100 000 cycles (selon qualité)
   SSD : 1 000-10 000 cycles (selon type TLC/MLC/SLC)
   
   Après épuisement : Données corrompues, pertes aléatoires
   
   ③ ENVIRONNEMENT
   ──────────────────────────────────────────────────────────────
   • Chaleur excessive (> 60°C)
   • Humidité
   • Champs magnétiques puissants (HDD uniquement)
   
   STATISTIQUES FIABILITÉ
   ──────────────────────────────────────────────────────────────
   • 25% des clés USB échouent dans les 5 ans
   • 40% des disques durs externes échouent dans les 10 ans
   • 15% des SSD ont des problèmes dans les 5 ans
```

---

## PARTIE VIII — Bonnes Pratiques

### VIII.A. Chiffrement Obligatoire

**Règle :** Toute donnée sensible sur support amovible DOIT être chiffrée.

```
   POURQUOI CHIFFRER ?
   ═══════════════════════════════════════════════════════════════
   
   SANS CHIFFREMENT
   ──────────────────────────────────────────────────────────────
   Clé USB perdue → Fichiers lisibles par quiconque la trouve
   → Fuite de données
   
   AVEC CHIFFREMENT
   ──────────────────────────────────────────────────────────────
   Clé USB perdue → Fichiers chiffrés, illisibles sans mot de passe
   → Données protégées
```

**Outils de chiffrement :**

| **Outil** | **OS** | **Prix** | **Niveau** | **Usage** |
|---|---|---|---|---|
| **VeraCrypt** | Win/Mac/Linux | Gratuit | Fort (AES-256) | Recommandé |
| **BitLocker** | Windows Pro | Inclus | Fort (AES-256) | Entreprise |
| **LUKS** | Linux | Gratuit | Fort (AES-256) | Linux natif |
| **FileVault** | macOS | Inclus | Fort (AES-256) | Mac natif |

---

### VIII.B. Politique d'Usage en Entreprise

```
   POLITIQUE TYPE D'USAGE DES SUPPORTS AMOVIBLES
   ═══════════════════════════════════════════════════════════════
   
   ① INTERDICTION DES CLÉS USB PERSONNELLES
   ──────────────────────────────────────────────────────────────
   • Seules les clés USB d'entreprise (fournies et chiffrées) autorisées
   • Blocage des ports USB par GPO (sauf autorisations)
   
   ② CHIFFREMENT OBLIGATOIRE
   ──────────────────────────────────────────────────────────────
   • Toute clé USB professionnelle doit être chiffrée (BitLocker)
   • Mot de passe robuste requis (12+ caractères)
   
   ③ SCAN ANTIVIRUS AUTOMATIQUE
   ──────────────────────────────────────────────────────────────
   • Analyse automatique à chaque branchement
   • Blocage si malware détecté
   
   ④ TRAÇABILITÉ
   ──────────────────────────────────────────────────────────────
   • Registre des clés USB : qui, quoi, quand
   • Numéro de série enregistré
   
   ⑤ FORMATION
   ──────────────────────────────────────────────────────────────
   • Sensibilisation aux risques (USB drop, malware)
   • Procédure de signalement si clé perdue
```

---

### VIII.C. Checklist Bonnes Pratiques

```
☐ NE JAMAIS brancher une clé USB trouvée ou inconnue
☐ TOUJOURS chiffrer les données sensibles (VeraCrypt, BitLocker)
☐ SCANNER avec antivirus avant d'ouvrir des fichiers
☐ ÉJECTER proprement (ne pas arracher)
☐ SAUVEGARDER ailleurs (ne pas stocker uniquement sur clé USB)
☐ DÉBRANCHER après usage (protection ransomware)
☐ STOCKER dans un lieu sûr (pas dans la voiture, pas dans le sac)
☐ ÉTIQUETER clairement (mais sans info sensible : "Backup 2024" ❌ "Salaires confidentiels" ✅)
☐ TESTER régulièrement l'intégrité
☐ REMPLACER tous les 3-5 ans (usure)
```

---
