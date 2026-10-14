---
author: YLP
title: 📖 Cahier des Charges Projet
---

# Cahier des Charges Projet
## Sécurisation Infrastructure DataCorp SARL

---

## 📋 CONTEXTE ENTREPRISE

**Nom** : DataCorp SARL  
**Activité** : Développement logiciels sur-mesure + Conseil IT  
**Effectif** : 45 salariés  
**CA** : 3,2 M€/an  
**Locaux** : 1 site unique (Toulouse)

---

## 👥 ORGANISATION

**Services** :

| Service | Effectif | Responsable |
|---------|----------|-------------|
| **Direction** | 3 | M. Dubois (PDG) |
| **Comptabilité** | 5 | Mme Martin |
| **RH** | 3 | Mme Lefebvre |
| **Développement** | 25 | M. Durand (CTO) |
| **Commercial** | 7 | Mme Bernard |
| **IT** | 2 | Vous (Technicien SISR) |

---

## 🖥️ INFRASTRUCTURE ACTUELLE

**Serveurs** :
- **SRV-DC** : Contrôleur domaine AD (Windows Server 2022)
- **SRV-FILES** : Serveur fichiers (Windows Server 2022)
- **SRV-SQL** : SQL Server 2019 (bases clients)
- **SRV-WEB** : Apache Ubuntu 22.04 (site vitrine)

**Réseau** :
- 1 switch manageable 48 ports
- 1 routeur/firewall pfSense
- 45 PC Windows 11 Pro (domaine AD)
- Connexion fibre 1 Gb/s symétrique

**Stockage** :
- SRV-FILES : 2 To utilisés / 4 To total
- SRV-SQL : 500 Go BDD
- NAS Synology 8 To (backup actuel manuel)

---

## 🎯 MISSION

Le PDG, M. Dubois, vous mandate pour **sécuriser l'infrastructure** suite à un audit externe révélant des failles critiques.

**Objectif** : Concevoir et documenter une infrastructure sécurisée selon les bonnes pratiques.

---

## 📝 LIVRABLES ATTENDUS

### Livrable 1 : Schéma Réseau Sécurisé

**Contenu** :
- Architecture réseau avec zones LAN / DMZ / Internet
- Placement de chaque serveur (LAN ou DMZ)
- Pare-feu (externe et interne)
- Adressage IP de chaque zone
- Règles pare-feu principales (tableau)

**Format** : Schéma Draw.io, Visio, ou papier scanné (propre)

**Critères qualité** :
- Zones clairement séparées
- Flux réseau indiqués (flèches)
- Légende (couleurs, symboles)

---

### Livrable 2 : Documentation GPO

**Contenu** :
- Liste des GPO créées (min 5)
- Pour chaque GPO :
  - Nom
  - OU cible (Ordinateurs / Utilisateurs)
  - Paramètres configurés
  - Justification (pourquoi cette GPO ?)
  - Capture écran configuration

**Format** : Document Word/PDF (3-5 pages)

**GPO obligatoires** :
1. Politique mot de passe
2. Politique verrouillage compte
3. Pare-feu Windows
4. + 2 GPO au choix (écran verrouillage, restriction logiciels...)

---

### Livrable 3 : Matrice Droits NTFS

**Contenu** :
- Structure dossiers partagés `\\SRV-FILES\`
- Matrice permissions par groupe AD

**Format** : Tableau Excel ou Word

**Exemple** :

| Dossier | Direction | Compta | RH | Dev | Commercial | IT |
|---------|-----------|--------|-----|-----|------------|-----|
| Commun | Modification | Lecture | Lecture | Lecture | Lecture | Contrôle |
| Comptabilite | Lecture | Modification | ❌ | ❌ | ❌ | Contrôle |
| RH | Lecture | ❌ | Modification | ❌ | ❌ | Contrôle |
| ... | ... | ... | ... | ... | ... | ... |

**Contraintes** :
- Minimum 6 dossiers partagés
- Principe moindre privilège respecté
- Justifier chaque choix

---

### Livrable 4 : Plan de Sauvegarde

**Contenu** :
- Stratégie sauvegarde (type, fréquence)
- Tableau détaillé :
  - Quoi (serveur/données)
  - Quand (horaire, fréquence)
  - Où (support, localisation)
  - Comment (outil)
  - Rétention (combien de temps)
- Respect règle 3-2-1
- Procédure test restauration mensuelle

**Format** : Document Word/PDF (2-3 pages)

---

### Livrable 5 : Configuration HTTPS

**Contenu** :
- Choix certificat (Let's Encrypt / Payant / Auto-signé)
- Justification du choix
- Procédure d'installation détaillée (commandes Linux)
- Configuration Apache (fichier .conf)
- Test de validation (capture `https://` avec cadenas)

**Format** : Document Word/PDF (1-2 pages) + Capture écran

---

### Livrable 6 : Soutenance Orale (5 min)

**Structure** :
1. Présentation entreprise DataCorp (30 sec)
2. Schéma réseau sécurisé (1 min 30)
3. GPO principales (1 min)
4. Droits NTFS (1 min)
5. Sauvegardes + HTTPS (1 min)
6. Questions jury (3 min)

**Support** : PowerPoint ou Présentation orale avec docs imprimés

---

## ⚙️ CONTRAINTES TECHNIQUES

**Budget** :
- Pas d'achat matériel (utiliser équipements existants)
- Certificat SSL : Gratuit (Let's Encrypt) ou auto-signé

**Délais** :
- S17 : Début projet (4h)
- S18 : Finalisation (3h) + Soutenances (1h)

**Groupes** :
- 2-3 apprenants par groupe
- Répartition des tâches équitable

---

## 📊 CRITÈRES D'ÉVALUATION

**40 points au total** :
- Schéma réseau : 8 pts
- GPO : 8 pts
- NTFS : 6 pts
- Sauvegardes : 6 pts
- HTTPS : 4 pts
- Soutenance : 8 pts

**Voir grille détaillée** : S17_05_Grille_Evaluation.md

---

## 💡 CONSEILS

**Méthodologie** :
1. Lire tout le cahier des charges AVANT de commencer
2. Répartir les tâches dans le groupe (qui fait quoi)
3. Commencer par le schéma réseau (base de tout)
4. Documenter au fur et à mesure (pas à la fin)
5. Tester vos configurations (VM si possible)
6. Préparer la soutenance dès S17

**Pièges à éviter** :
- ❌ Serveur web dans le LAN (doit être en DMZ)
- ❌ Tous les utilisateurs "Admins"
- ❌ Sauvegarde uniquement locale (pas de hors site)
- ❌ HTTP sans redirection vers HTTPS
- ❌ Documentation bâclée (illisible, incomplète)

---

*Cahier des Charges S17 BLOC 3 — BTS SIO SISR*
