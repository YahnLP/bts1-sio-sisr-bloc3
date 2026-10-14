---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Stratégies de Sauvegarde · Types · Comparaison"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 4*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B1.7** | Assurer la disponibilité des services informatiques |

---

## PARTIE I — Pourquoi Sauvegarder ?

### I.A. Les 5 Causes de Perte de Données

```
   CAUSES DE PERTE DE DONNÉES (Statistiques 2023)
   ═══════════════════════════════════════════════════════════════
   
   ① PANNE MATÉRIELLE (40%)
   ──────────────────────────────────────────────────────────────
   • Disque dur qui casse (têtes de lecture, moteur)
   • SSD qui meurt (usure des cellules NAND)
   • Serveur qui grille (alimentation, surtension)
   
   Espérance de vie :
   • Disque dur (HDD) : 5-10 ans
   • SSD : 5-7 ans (selon usage)
   • Serveur : 5-8 ans
   
   ② RANSOMWARE / CYBERATTAQUE (30%)
   ──────────────────────────────────────────────────────────────
   • Fichiers chiffrés par ransomware (WannaCry, Ryuk...)
   • Serveurs détruits par malware
   • Base de données corrompue par attaque
   
   ③ ERREUR HUMAINE (20%)
   ──────────────────────────────────────────────────────────────
   • Suppression accidentelle (Shift+Delete)
   • Formatage du mauvais disque
   • Écrasement de fichiers
   • Mauvaise manipulation (DROP TABLE users;)
   
   ④ CATASTROPHE NATURELLE (8%)
   ──────────────────────────────────────────────────────────────
   • Incendie (bureau détruit)
   • Inondation (serveurs noyés)
   • Foudre (surtension, grillage matériel)
   
   ⑤ VOL / PERTE (2%)
   ──────────────────────────────────────────────────────────────
   • Ordinateur portable volé
   • Disque dur externe perdu
   • Serveur volé lors d'un cambriolage
```

**Conclusion :** Toutes les entreprises subiront **au moins une** de ces causes.

> *"Ce n'est pas SI vous perdrez des données, c'est QUAND."*

---

### I.B. Impact de la Perte de Données

```
   COÛT D'UNE PERTE DE DONNÉES (PME)
   ═══════════════════════════════════════════════════════════════
   
   FINANCIER
   ──────────────────────────────────────────────────────────────
   • Perte d'activité : 10 000-100 000 € par jour
   • Récupération données : 1 000-10 000 €
   • Reconstruction : 5 000-50 000 €
   
   RÉPUTATIONNEL
   ──────────────────────────────────────────────────────────────
   • Clients perdent confiance
   • Mauvaise publicité
   • Action en justice possible (RGPD)
   
   OPÉRATIONNEL
   ──────────────────────────────────────────────────────────────
   • Impossibilité de travailler
   • Retard dans les projets
   • Perte de productivité
   
   STATISTIQUE CHOC
   ──────────────────────────────────────────────────────────────
   60% des PME qui perdent leurs données
   FERMENT dans les 6 mois
   (Source : National Cyber Security Alliance, 2023)
```

---

## PARTIE II — Les 3 Types de Sauvegardes

### II.A. Sauvegarde Complète (Full Backup)

**Définition :** Copie **intégrale** de toutes les données, chaque fois.

```
   SAUVEGARDE COMPLÈTE
   ═══════════════════════════════════════════════════════════════
   
   LUNDI : Sauvegarde complète (100 Go)
   ──────────────────────────────────────────────────────────────
   Tous les fichiers : A, B, C, D, E, F, G, H, I, J
   Espace utilisé : 100 Go
   
   MARDI : Sauvegarde complète (100 Go)
   ──────────────────────────────────────────────────────────────
   Tous les fichiers : A, B, C, D, E, F, G, H, I, J
   (même si certains n'ont pas changé)
   Espace utilisé : 100 Go
   
   MERCREDI : Sauvegarde complète (100 Go)
   ──────────────────────────────────────────────────────────────
   Tous les fichiers : A, B, C, D, E, F, G, H, I, J
   Espace utilisé : 100 Go
   
   TOTAL ESPACE : 300 Go (3 × 100 Go)
```

**Avantages :**
- ✅ **Restauration simple et rapide** (1 seule sauvegarde à restaurer)
- ✅ **Fiabilité maximale** (chaque sauvegarde est autonome)
- ✅ **Facilité de gestion** (pas de dépendances entre sauvegardes)

**Inconvénients :**
- ❌ **Espace disque énorme** (copie tout à chaque fois)
- ❌ **Temps de sauvegarde long** (plusieurs heures pour To de données)
- ❌ **Bande passante réseau importante** (si sauvegarde distante)

**Usage typique :**
- Sauvegarde hebdomadaire (dimanche soir)
- PME avec peu de données (< 500 Go)
- Avant mise à jour majeure d'un système

---

### II.B. Sauvegarde Différentielle (Differential Backup)

**Définition :** Sauvegarde complète initiale, puis sauvegardes des fichiers **modifiés depuis la dernière complète**.

```
   SAUVEGARDE DIFFÉRENTIELLE
   ═══════════════════════════════════════════════════════════════
   
   LUNDI : Sauvegarde complète (100 Go)
   ──────────────────────────────────────────────────────────────
   Tous les fichiers : A, B, C, D, E, F, G, H, I, J
   Espace utilisé : 100 Go
   
   MARDI : Sauvegarde différentielle (5 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis LUNDI : B, E
   Espace utilisé : 5 Go
   
   MERCREDI : Sauvegarde différentielle (8 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis LUNDI : B, E, C
   Espace utilisé : 8 Go (5 + 3)
   ↑ Cumule les changements depuis la complète
   
   JEUDI : Sauvegarde différentielle (12 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis LUNDI : B, E, C, F
   Espace utilisé : 12 Go (5 + 3 + 4)
   ↑ Continue de cumuler
   
   TOTAL ESPACE : 125 Go (100 + 5 + 8 + 12)
```

**Caractéristique clé :** Chaque sauvegarde différentielle **cumule** tous les changements depuis la dernière complète.

**Avantages :**
- ✅ **Restauration simple** (2 sauvegardes : complète + dernière différentielle)
- ✅ **Espace modéré** (moins que complète, plus qu'incrémentielle)

**Inconvénients :**
- ❌ **Espace croissant** (chaque diff grossit jour après jour)
- ❌ **Nécessite complète récente** (si complète corrompue → toutes les diff inutiles)

**Usage typique :**
- Complète le dimanche, différentielle lundi-samedi
- PME avec sauvegarde quotidienne

---

### II.C. Sauvegarde Incrémentielle (Incremental Backup)

**Définition :** Sauvegarde complète initiale, puis sauvegardes des fichiers **modifiés depuis la dernière sauvegarde** (quelle qu'elle soit).

```
   SAUVEGARDE INCRÉMENTIELLE
   ═══════════════════════════════════════════════════════════════
   
   LUNDI : Sauvegarde complète (100 Go)
   ──────────────────────────────────────────────────────────────
   Tous les fichiers : A, B, C, D, E, F, G, H, I, J
   Espace utilisé : 100 Go
   
   MARDI : Sauvegarde incrémentielle (5 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis LUNDI : B, E
   Espace utilisé : 5 Go
   
   MERCREDI : Sauvegarde incrémentielle (3 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis MARDI : C
   Espace utilisé : 3 Go
   ↑ Seulement les nouveaux changements depuis hier
   
   JEUDI : Sauvegarde incrémentielle (4 Go)
   ──────────────────────────────────────────────────────────────
   Fichiers modifiés depuis MERCREDI : F
   Espace utilisé : 4 Go
   ↑ Seulement les nouveaux changements depuis hier
   
   TOTAL ESPACE : 112 Go (100 + 5 + 3 + 4)
```

**Caractéristique clé :** Chaque sauvegarde incrémentielle ne prend que les **nouveaux changements** depuis la veille.

**Avantages :**
- ✅ **Espace minimal** (le plus efficace en stockage)
- ✅ **Temps de sauvegarde rapide** (peu de données à copier)
- ✅ **Bande passante faible** (idéal pour sauvegarde distante)

**Inconvénients :**
- ❌ **Restauration complexe et lente** (besoin de TOUTES les sauvegardes)
  ```
  Pour restaurer jeudi :
  1. Restaurer complète lundi
  2. Restaurer incrémentielle mardi
  3. Restaurer incrémentielle mercredi
  4. Restaurer incrémentielle jeudi
  → 4 étapes
  ```
- ❌ **Risque accru** (si une incrémentielle est corrompue → chaîne brisée)

**Usage typique :**
- Grandes entreprises avec To de données
- Sauvegarde quotidienne + complète mensuelle
- Environnements avec sauvegarde continue (toutes les heures)

---

### II.D. Tableau Comparatif Récapitulatif

| **Critère** | **Complète** | **Différentielle** | **Incrémentielle** |
|---|---|---|---|
| **Espace disque** | ❌ Maximum | 🟡 Moyen (croissant) | ✅ Minimum |
| **Temps sauvegarde** | ❌ Long | 🟡 Moyen (croissant) | ✅ Court |
| **Temps restauration** | ✅ Rapide (1 étape) | 🟡 Moyen (2 étapes) | ❌ Lent (N étapes) |
| **Complexité** | ✅ Simple | 🟡 Moyenne | ❌ Complexe |
| **Fiabilité** | ✅ Maximum | 🟡 Bonne | 🟡 Moyenne (chaîne) |
| **Usage typique** | Hebdomadaire | Quotidienne | Horaire/Continue |

---

### II.E. Stratégie Combinée (Recommandée)

**Principe :** Combiner les 3 types pour optimiser espace ET restauration.

```
   STRATÉGIE GRAND-PÈRE-PÈRE-FILS (GFS)
   ═══════════════════════════════════════════════════════════════
   
   FILS (quotidien) : Incrémentielle
   ──────────────────────────────────────────────────────────────
   Lundi → Dimanche : Sauvegarde incrémentielle chaque soir
   Rétention : 7 jours (1 semaine)
   
   PÈRE (hebdomadaire) : Différentielle ou Complète
   ──────────────────────────────────────────────────────────────
   Chaque dimanche : Sauvegarde complète
   Rétention : 4 semaines (1 mois)
   
   GRAND-PÈRE (mensuel) : Complète
   ──────────────────────────────────────────────────────────────
   Premier dimanche du mois : Sauvegarde complète archivée
   Rétention : 12 mois (1 an) ou plus
   
   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Optimisation espace (incrémentielle quotidienne)
   ✅ Restauration rapide récente (complète hebdomadaire)
   ✅ Historique long terme (complète mensuelle)
```

---

## PARTIE III — La Règle 3-2-1 (Approfondie)

### III.A. Rappel de la Règle

```
   RÈGLE 3-2-1
   ═══════════════════════════════════════════════════════════════
   
   3 COPIES de vos données
   ├── 1 copie de production (données actives sur le serveur)
   ├── 1 copie de sauvegarde locale (disque externe, NAS)
   └── 1 copie de sauvegarde distante (cloud, site distant)
   
   2 SUPPORTS DIFFÉRENTS
   ├── Support 1 : Disque dur (local)
   └── Support 2 : Cloud / Bande magnétique / SSD (distant)
   
   1 COPIE HORS SITE (off-site)
   └── Cloud (AWS, Azure, Backblaze) OU datacenter distant
```

---

### III.B. Pourquoi 3 Copies ?

```
   SCÉNARIO : Incendie dans les locaux
   ═══════════════════════════════════════════════════════════════
   
   AVEC 1 SEULE COPIE (serveur)
   ──────────────────────────────────────────────────────────────
   Serveur détruit → Données PERDUES
   
   AVEC 2 COPIES (serveur + disque externe à côté)
   ──────────────────────────────────────────────────────────────
   Serveur détruit + disque externe détruit → Données PERDUES
   (même lieu = même risque)
   
   AVEC 3 COPIES (serveur + disque externe + cloud)
   ──────────────────────────────────────────────────────────────
   Serveur détruit + disque externe détruit
   → Cloud intact → Données SAUVÉES ✅
```

---

### III.C. Pourquoi 2 Supports Différents ?

**Risque de défaillance corrélée :**

Si vous utilisez 2 disques durs de **même marque** et **même modèle** achetés **en même temps** :
- Ils ont été fabriqués dans le **même lot**
- Ils ont les **mêmes défauts de fabrication**
- Ils mourront **en même temps** (espérance de vie similaire)

**Solution :** Diversifier les supports.

```
   EXEMPLES DE COMBINAISONS
   ═══════════════════════════════════════════════════════════════
   
   ✅ BONNE COMBINAISON
   ──────────────────────────────────────────────────────────────
   • Support 1 : Disque dur HDD (Seagate)
   • Support 2 : SSD (Samsung) + Cloud (Backblaze)
   
   ✅ BONNE COMBINAISON (entreprise)
   ──────────────────────────────────────────────────────────────
   • Support 1 : NAS local (RAID 5)
   • Support 2 : Bande magnétique (LTO) stockée hors site
   
   ❌ MAUVAISE COMBINAISON
   ──────────────────────────────────────────────────────────────
   • Support 1 : Disque dur WD Blue 2 To
   • Support 2 : Disque dur WD Blue 2 To (même modèle, même lot)
```

---

### III.D. Pourquoi 1 Copie Hors Site ?

**Protection contre les sinistres locaux :**

```
   SINISTRES LOCAUX
   ═══════════════════════════════════════════════════════════════
   
   • Incendie (bureau détruit)
   • Inondation (sous-sol inondé)
   • Cambriolage (serveur + disque externe volés)
   • Foudre (surtension grille tout le matériel)
   • Catastrophe naturelle (tremblement de terre, ouragan)
   
   → TOUTES les sauvegardes sur place sont PERDUES
   
   SOLUTION : Copie hors site (différent bâtiment, ville, pays)
```

**Options hors site :**

| **Option** | **Coût** | **Facilité** | **Sécurité** | **Usage** |
|---|---|---|---|---|
| **Cloud** (AWS, Azure, Backblaze) | 5-20 €/mois/To | ★★★★★ | ★★★★☆ | PME, particuliers |
| **Datacenter distant** | 100-500 €/mois | ★★☆☆☆ | ★★★★★ | Grandes entreprises |
| **Maison / Bureau distant** | Gratuit | ★★★☆☆ | ★★☆☆☆ | Petites structures |
| **Coffre-fort bancaire** | 50-200 €/an | ★★☆☆☆ | ★★★★★ | Sauvegardes critiques (bande, disque) |

---

## PARTIE IV — Politique de Sauvegarde

### IV.A. Fréquence de Sauvegarde

**Question clé :** *"Combien de temps de données êtes-vous prêt à perdre ?"*

```
   RPO (Recovery Point Objective)
   ═══════════════════════════════════════════════════════════════
   
   Objectif de Point de Restauration = Perte de données maximale
   acceptable
   
   EXEMPLES
   ──────────────────────────────────────────────────────────────
   RPO = 24 heures → Sauvegarde quotidienne
   (Perte max : 1 jour de données)
   
   RPO = 1 heure → Sauvegarde horaire
   (Perte max : 1 heure de données)
   
   RPO = 0 (zéro) → Réplication en temps réel
   (Aucune perte acceptable)
   
   SECTEURS ET RPO TYPIQUES
   ──────────────────────────────────────────────────────────────
   • PME bureautique : RPO = 24h (sauvegarde nocturne)
   • E-commerce : RPO = 1h (sauvegarde continue)
   • Banque : RPO = 0 (réplication synchrone)
   • Hôpital : RPO = 15 min (vies en jeu)
```

---

### IV.B. Rétention des Sauvegardes

**Question clé :** *"Pendant combien de temps garder les anciennes sauvegardes ?"*

```
   STRATÉGIE DE RÉTENTION TYPE
   ═══════════════════════════════════════════════════════════════
   
   QUOTIDIENNE : 7 jours (1 semaine)
   ──────────────────────────────────────────────────────────────
   Lundi, Mardi, Mercredi, Jeudi, Vendredi, Samedi, Dimanche
   → Après 7 jours, suppression de la plus ancienne
   
   HEBDOMADAIRE : 4 semaines (1 mois)
   ──────────────────────────────────────────────────────────────
   Semaine 1, Semaine 2, Semaine 3, Semaine 4
   → Après 1 mois, suppression de la plus ancienne
   
   MENSUELLE : 12 mois (1 an)
   ──────────────────────────────────────────────────────────────
   Janvier, Février, Mars... Décembre
   → Après 1 an, suppression de la plus ancienne
   
   ANNUELLE : 3-7 ans (selon obligations légales)
   ──────────────────────────────────────────────────────────────
   2024, 2023, 2022... (archives long terme)
   → Selon RGPD et obligations comptables
```

**Obligations légales (France) :**
- Comptabilité : **10 ans**
- Documents fiscaux : **6 ans**
- Contrats : **5 ans**
- Données personnelles (RGPD) : Durée nécessaire uniquement

---

### IV.C. Tests de Restauration

**Règle d'or :**
> *"Une sauvegarde jamais testée est une sauvegarde qui n'existe pas."*

```
   STATISTIQUE CHOC
   ═══════════════════════════════════════════════════════════════
   
   34% des entreprises découvrent que leurs sauvegardes
   ne fonctionnent PAS quand elles essaient de restaurer
   en situation de crise.
   
   (Source : Veeam Data Protection Report 2023)
```

**Plan de tests :**

| **Fréquence** | **Type de test** | **Objectif** |
|---|---|---|
| **Mensuel** | Restauration fichier | Vérifier intégrité fichiers |
| **Trimestriel** | Restauration complète VM | Vérifier restauration serveur |
| **Annuel** | Exercice PRA complet | Simulation catastrophe totale |

---

## V. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Sauvegarde complète** | Copie intégrale de toutes les données |
| **Sauvegarde différentielle** | Fichiers modifiés depuis la dernière complète |
| **Sauvegarde incrémentielle** | Fichiers modifiés depuis la dernière sauvegarde (quelle qu'elle soit) |
| **Règle 3-2-1** | 3 copies, 2 supports, 1 hors site |
| **RPO** | Recovery Point Objective — perte de données max acceptable |
| **RTO** | Recovery Time Objective — temps max de restauration acceptable |
| **GFS** | Grand-père Père Fils — stratégie combinée de sauvegarde |
| **Rétention** | Durée de conservation des sauvegardes |
| **Hors site (off-site)** | Sauvegarde stockée dans un lieu géographiquement distinct |

---

