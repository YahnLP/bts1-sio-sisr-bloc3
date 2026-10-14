# Annexe – Cas InnoTech (fictif) : dossiers, groupes et besoins

*BTS SIO SISR 1re année – Bloc 3 – S04 – support du [TP](02-tp.md)*

> [!NOTE]
> **InnoTech SARL** est une entreprise **fictive** : PME de services numériques de 30 salariés. Toute ressemblance avec une organisation réelle est fortuite.

## Les dossiers du serveur de fichiers

```text
\\SERVEUR\Data\
├── Clients\        contrats, fiches clients, devis
├── Projets\        code source, documentation technique
├── RH\             contrats des salariés, bulletins de paie, évaluations
├── Comptabilite\   bilans, factures, relevés bancaires
├── Direction\      procès-verbaux, plans stratégiques, budgets
├── IT\             configurations réseau, scripts, documentation d'infrastructure
└── Archives\       documents de plus de 5 ans, en lecture seule
```

## Les groupes et leurs besoins métier

| Groupe | Effectif | Missions | Besoins d'accès exprimés |
|---|---|---|---|
| `G_Commercial` | 5 | Relation clients, devis, contrats | Clients, Archives |
| `G_Comptable` | 2 | Facturation, paie, bilan | Comptabilité ; Clients (consultation) ; RH (données de paie seulement) |
| `G_DRH` | 1 | Gestion du personnel | RH |
| `G_Dev` | 8 | Développement logiciel | Projets |
| `G_Chef_Projet` | 3 | Pilotage, clients, technique | Clients, Projets, Archives |
| `G_Direction` | 2 | Stratégie, validation globale | Direction ; consultation des autres dossiers de gestion |
| `G_Admin_IT` | 2 | Infrastructure, sécurité, maintenance | IT ; journaux ; **sauvegarde** de l'ensemble |
| `G_Stagiaire` | 2 | Aide au développement | Projets (consultation) |

> [!WARNING]
> Les besoins « exprimés » sont **ceux que les équipes disent avoir**. Le travail d'un administrateur consiste aussi à les **questionner** : est-ce un besoin ou une habitude ?
