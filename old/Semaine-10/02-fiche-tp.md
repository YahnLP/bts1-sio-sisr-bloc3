---
author: YLP
title: 🖥️ FICHE DE TP
---

# 🖥️ TP — CONSTRUIRE LA MATRICE DE DROITS D'UNE PME

## ANNEXE 2 et 3 — Cas PME InnoTech

*Durée : 20 minutes — Individuel*

---

### Contexte

**InnoTech SARL** — PME de services numériques, 30 salariés.

**Structure des dossiers partagés (\\SERVEUR\Data) :**

```
\\SERVEUR\Data\
├── Clients\         (contrats, fiches clients, devis)
├── Projets\         (code source, documentation technique)
├── RH\              (contrats salariés, bulletins paie, évaluations)
├── Comptabilite\    (bilans, factures, relevés bancaires)
├── Direction\       (PV de CA, plans stratégiques, budgets)
├── IT\              (configs réseau, mots de passe serveurs, scripts)
└── Archives\        (documents > 5 ans, lecture seule)
```

**Postes et besoins métier :**

| **Groupe** | **Missions** | **Besoins d'accès** |
|---|---|---|
| **G_Commercial** (5 pers.) | Relation clients, devis, contrats | Clients, Archives |
| **G_Comptable** (2 pers.) | Facturation, paie, bilan | Comptabilité, Clients (lect.), RH (paie seulement) |
| **G_DRH** (1 pers.) | Gestion du personnel | RH complet |
| **G_Dev** (8 pers.) | Développement logiciel | Projets |
| **G_Chef_Projet** (3 pers.) | Pilotage, clients, technique | Clients, Projets, Archives |
| **G_Direction** (2 pers.) | Stratégie, validation globale | Lecture sur tout |
| **G_Admin_IT** (2 pers.) | Infra, sécurité, maintenance | IT complet, logs |
| **G_Stagiaire** (2 pers.) | Aide au développement | Projets (lecture) |

---

### Travail à Réaliser

**Remplir la matrice de droits complète :**

```
MATRICE DE DROITS — INNOTECH SARL
═══════════════════════════════════════════════════════════════
LÉGENDE : — = Aucun  L = Lecture  L+E = Lecture+Écriture
          L+E+S = Lecture+Écriture+Suppression  A = Admin

                  │Clients│Projets│  RH  │Compta│Direct│  IT  │Archiv
──────────────────┼───────┼───────┼──────┼──────┼──────┼──────┼──────
G_Commercial      │       │       │      │      │      │      │
G_Comptable       │       │       │      │      │      │      │
G_DRH             │       │       │      │      │      │      │
G_Dev             │       │       │      │      │      │      │
G_Chef_Projet     │       │       │      │      │      │      │
G_Direction       │       │       │      │      │      │      │
G_Admin_IT        │       │       │      │      │      │      │
G_Stagiaire       │       │       │      │      │      │      │
──────────────────┴───────┴───────┴──────┴──────┴──────┴──────┴──────
```

**Questions de réflexion :**

```
1. Pourquoi G_Admin_IT ne devrait-il PAS avoir accès à /RH/ ?
──────────────────────────────────────────────────────────────
_______________________________________________________________

2. Un développeur trouve un bug dans le module de facturation.
   Il a besoin d'accéder temporairement à /Comptabilite/ pour
   le corriger. Comment gérer cela de façon conforme au
   moindre privilège ?
──────────────────────────────────────────────────────────────
_______________________________________________________________
_______________________________________________________________

3. Rédigez la commande PowerShell AD pour ajouter
   Marie Durand (m.durand) au groupe G_Commercial :
──────────────────────────────────────────────────────────────
_______________________________________________________________

4. Marie Durand quitte l'entreprise vendredi.
   Rédigez la commande PowerShell pour désactiver son compte :
──────────────────────────────────────────────────────────────
_______________________________________________________________
```

---

### Corrigé (Enseignant)

```
MATRICE DE DROITS — CORRIGÉ
═══════════════════════════════════════════════════════════════

                  │Clients│Projets│  RH  │Compta│Direct│  IT  │Archiv
──────────────────┼───────┼───────┼──────┼──────┼──────┼──────┼──────
G_Commercial      │ L+E+S │   —   │   —  │   —  │   —  │   —  │   L
G_Comptable       │   L   │   —   │   L  │ L+E+S│   —  │   —  │   L
G_DRH             │   —   │   —   │ L+E+S│   L  │   —  │   —  │   L
G_Dev             │   —   │ L+E+S │   —  │   —  │   —  │   —  │   L
G_Chef_Projet     │  L+E  │ L+E+S │   —  │   —  │   —  │   —  │   L
G_Direction       │   L   │   L   │   L  │   L  │ L+E+S│   —  │   L
G_Admin_IT        │   —   │   —   │   —  │   —  │   —  │   A  │   —
G_Stagiaire       │   —   │   L   │   —  │   —  │   —  │   —  │   —
──────────────────┴───────┴───────┴──────┴──────┴──────┴──────┴──────

NOTES SUR LE CORRIGÉ :
──────────────────────────────────────────────────────────────
→ G_Comptable a L sur /RH/ (pour accéder aux données paie)
  mais PAS L+E (ne modifie pas les contrats ou évaluations)
→ G_DRH a L sur /Compta/ (pour vérifier fiches de paie)
  mais PAS L+E (ne modifie pas la comptabilité)
→ G_Admin_IT : ZÉRO accès aux données métier
  (Sécurité par séparation stricte IT/Métier)
→ G_Stagiaire : L seule sur Projets (pas d'écriture)
→ Archives : L pour tous ceux qui ont besoin d'historique

RÉPONSES AUX QUESTIONS
──────────────────────────────────────────────────────────────
Q1 : Séparation des tâches — Le technicien IT gère l'infra
     mais ne doit pas avoir accès aux données confidentielles
     des salariés (confidentialité RGPD + risque interne)

Q2 : Accès temporaire documenté :
     → Demande formelle du développeur + validation direction
     → Accès accordé en lecture uniquement, pour durée définie
     → Révocable dès la correction validée
     → Traçabilité (log de l'accès, incident documenté)

Q3 : Add-ADGroupMember -Identity "G_Commercial" -Members "m.durand"

Q4 : Disable-ADAccount -Identity "m.durand"
     (+ Move vers OU Comptes_Desactives)
═══════════════════════════════════════════════════════════════
```

---
