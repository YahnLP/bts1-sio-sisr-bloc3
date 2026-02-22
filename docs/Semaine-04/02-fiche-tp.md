---
author: YLP
title: 🖥️ FICHE TP
---

# 🖥️ TP PARTIE 1 — STRATÉGIE DE SAUVEGARDE PME

*Durée : 45 minutes — Individuel ou binôme*

---

## Cas Pratique : SimTech SARL

**Contexte :**
- PME de 25 employés (développement logiciel)
- Serveur principal : Windows Server 2022
  - 500 Go de données (code source, documents, bases de données)
  - Modifications quotidiennes : 5-10 Go/jour
- Budget sauvegarde : 500 € (matériel) + 50 €/mois (cloud)
- Contrainte : Sauvegarde nocturne (22h-6h)

---

## ÉTAPE 1 — Analyser le Besoin (15 min)

**Répondre aux questions suivantes :**

```
1. RPO (Recovery Point Objective)
──────────────────────────────────────────────────────────────
Combien de temps de données l'entreprise peut-elle perdre ?

☐ 24 heures (sauvegarde quotidienne)
☐ 1 heure (sauvegarde horaire)
☐ 15 minutes (sauvegarde continue)

Justification : _______________________________________________

2. RTO (Recovery Time Objective)
──────────────────────────────────────────────────────────────
Combien de temps max pour restaurer après incident ?

☐ 1 heure
☐ 4 heures
☐ 24 heures

Justification : _______________________________________________

3. Rétention
──────────────────────────────────────────────────────────────
Combien de temps garder les sauvegardes ?

Quotidiennes : _____ jours
Hebdomadaires : _____ semaines
Mensuelles : _____ mois
Annuelles : _____ ans

Justification : _______________________________________________
```

---

## ÉTAPE 2 — Concevoir la Stratégie (20 min)

**Remplir le tableau de stratégie :**

```
┌─────────────────────────────────────────────────────────────┐
│ STRATÉGIE DE SAUVEGARDE SIMTECH SARL                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ TYPE DE SAUVEGARDE                                          │
│ ──────────────────────────────────────────────────────────  │
│ Quotidienne :                                               │
│ ☐ Complète  ☐ Différentielle  ☐ Incrémentielle             │
│                                                             │
│ Hebdomadaire :                                              │
│ ☐ Complète  ☐ Différentielle  ☐ Incrémentielle             │
│                                                             │
│ Justification : ________________________________________    │
│ ____________________________________________________________ │
│                                                             │
│ RÈGLE 3-2-1                                                 │
│ ──────────────────────────────────────────────────────────  │
│ Copie 1 (production) :                                      │
│ Serveur Windows (500 Go)                                    │
│                                                             │
│ Copie 2 (locale) :                                          │
│ Support : ☐ Disque externe  ☐ NAS  ☐ SSD                   │
│ Capacité : _______ To                                       │
│ Coût : _______ €                                            │
│                                                             │
│ Copie 3 (hors site) :                                       │
│ Support : ☐ Cloud (AWS/Azure/Backblaze)  ☐ Datacenter      │
│ Capacité : _______ To                                       │
│ Coût : _______ €/mois                                       │
│                                                             │
│ TOTAL COÛT                                                  │
│ ──────────────────────────────────────────────────────────  │
│ Matériel (one-time) : _______ €                             │
│ Abonnement (mensuel) : _______ €/mois                       │
│                                                             │
│ Budget disponible : 500 € + 50 €/mois                       │
│ Budget respecté ? ☐ Oui  ☐ Non                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## ÉTAPE 3 — Plan de Tests (10 min)

**Définir le plan de tests de restauration :**

```
PLAN DE TESTS DE RESTAURATION
═══════════════════════════════════════════════════════════════

TEST MENSUEL
──────────────────────────────────────────────────────────────
Quoi : Restaurer 5 fichiers aléatoires
Qui : Technicien IT
Durée estimée : 30 minutes
Documentation : Rapport mensuel

TEST TRIMESTRIEL
──────────────────────────────────────────────────────────────
Quoi : Restaurer un dossier complet (ex : projet client)
Qui : Responsable IT + 1 développeur
Durée estimée : 2 heures
Documentation : Rapport trimestriel

TEST ANNUEL
──────────────────────────────────────────────────────────────
Quoi : Simulation catastrophe (restauration serveur complet)
Qui : Toute l'équipe IT
Durée estimée : 1 journée
Documentation : Rapport annuel + mise à jour PRA
```

---

---

# 🖥️ TP PARTIE 2 — CHIFFREMENT CLÉ USB

*Durée : 30 minutes — Individuel*

---

## Prérequis

- Clé USB (4 Go minimum)
- VeraCrypt installé (https://veracrypt.fr)

---

## ÉTAPE 1 — Installer VeraCrypt (5 min)

Si pas déjà installé :
1. Télécharger depuis https://veracrypt.fr
2. Installer avec paramètres par défaut
3. Lancer VeraCrypt

---

## ÉTAPE 2 — Créer un Volume Chiffré (15 min)

1. Brancher la clé USB
2. Lancer VeraCrypt
3. Cliquer "Create Volume"
4. Sélectionner "Create an encrypted file container" → Next
5. Sélectionner "Standard VeraCrypt volume" → Next
6. **Volume Location** :
   - Cliquer "Select File..."
   - Naviguer vers la clé USB (ex : E:\)
   - Nom : `coffre-fort` (pas d'extension)
   - Save
7. **Encryption Options** :
   - Encryption Algorithm : AES
   - Hash Algorithm : SHA-512
   - Next
8. **Volume Size** :
   - Taille : 500 MB (ou selon espace dispo)
   - Next
9. **Volume Password** :
   - Mot de passe : Utiliser phrase de passe créée en S3
   - Confirm
   - ⚠️ Cocher "Use PIM" (optionnel mais recommandé)
   - Next
10. **Large Files** : No → Next
11. **Volume Format** :
    - Filesystem : FAT (compatible tous OS)
    - Bouger la souris aléatoirement (génération clé)
    - Cliquer "Format"
12. **Volume Created** → OK

---

## ÉTAPE 3 — Monter et Utiliser le Volume (10 min)

**Monter (ouvrir) le volume :**

1. Dans VeraCrypt, sélectionner une lettre de lecteur (ex : Z:)
2. Cliquer "Select File..." → Choisir `coffre-fort` sur la clé USB
3. Cliquer "Mount"
4. Saisir le mot de passe
5. OK

**Le volume chiffré apparaît comme un disque Z:**

**Utiliser :**
1. Ouvrir l'Explorateur Windows
2. Aller sur Z:
3. Copier des fichiers dedans (ex : documents personnels)
4. Les fichiers sont **automatiquement chiffrés**

**Démonter (fermer) :**
1. Dans VeraCrypt, sélectionner Z:
2. Cliquer "Dismount"
3. Le disque Z: disparaît
4. Les fichiers sont maintenant **illisibles** sans le mot de passe

---

