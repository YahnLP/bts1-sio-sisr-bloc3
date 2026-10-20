# S04 – Droits d'accès et moindre privilège

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S04 (séance 4 sur 19) – Phase 1 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Droits et moindre privilège : prérequis de S05, S06 et S14. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S03 (authentification) ; comptes, groupes et permissions NTFS (bloc 2, S02 et S10) ; permissions Linux (bloc 2, S06). |
| **Matériel** | VM Debian de laboratoire (paquet `acl`) ; VM Windows de laboratoire |
| **Compétences travaillées** | B3.3 · B3.4 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment donner à chacun exactement l'accès dont il a besoin, et pas un de plus ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Expliquer** le principe du moindre privilège et la séparation des tâches ;
2. **Comparer** les modèles de contrôle d'accès DAC, MAC et RBAC et **situer** leur usage ;
3. **Construire** une matrice de droits à partir des besoins métier ;
4. **Appliquer** cette matrice avec des groupes et des permissions (Linux : groupes, `chmod`, ACL ; Windows : NTFS, `icacls`) ;
5. **Organiser** la vie des comptes : arrivée, changement de poste, départ, accès temporaire, comptes à privilèges ;
6. **Vérifier** les droits réellement en place et **détecter** un écart.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Droits d'accès, privilèges et moindre privilège](01-cours.md) | Cours |
| [TP – Construire une matrice de droits et l'appliquer sous Linux et Windows](02-tp.md) | TP |
| [Aide-mémoire – Droits d'accès et privilèges](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Cas InnoTech (fictif) : dossiers, groupes et besoins](annexe-cas-innotech.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** (S03) : authentifier, autoriser | Oral |
| 0 h 20 – 1 h 20 | **Cours** : moindre privilège, modèles d'accès, matrice, vie des comptes | Cours et questions |
| 1 h 20 – 1 h 50 | **TP partie A** : construire la matrice de droits | Binôme |
| 1 h 50 – 2 h 50 | **TP partie B** : appliquer la matrice sous Linux | Binôme |
| 2 h 50 – 3 h 30 | **TP partie C** : auditer des droits sous Windows, traiter un départ | Binôme |
| 3 h 30 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Matrice de droits, tableau de tests et réponses du TP, nommés `RENDU-B3-S04-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Le cas InnoTech est **fictif**.
- La matrice du corrigé est **une** solution défendable : plusieurs répartitions sont acceptables si elles sont justifiées par les besoins (par exemple l'accès en lecture de la direction aux dossiers RH est discutable et fait l'objet d'une question).

</details>
