# S08 – Conservation, sécurité, sous-traitance et violations de données

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S08 (séance 8 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Prérequis** | S06 (principes, registre) et S07 (droits, effacement). |
| **Matériel** | VM Debian de laboratoire (paquets `sqlite3`, `cron`) ; éditeur de texte |
| **Compétences travaillées** | B3.1 · B3.4 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Combien de temps garder les données, comment les protéger, à qui les confier, et que faire quand elles fuient ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Définir** une durée de conservation et les trois phases de vie d'une donnée (base active, archive, suppression) ;
2. **Écrire** une purge automatique d'une base de données et d'un dossier de journaux ;
3. **Distinguer** pseudonymisation et anonymisation ;
4. **Citer** les mesures de sécurité de l'article 32 et les mentions d'un contrat de sous-traitance (article 28) ;
5. **Qualifier** une violation de données et **préparer** la notification à la CNIL dans le délai de 72 heures.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Conservation, sécurité du traitement, sous-traitance et violations de données](01-cours.md) | Cours |
| [TP – Purger des données, pseudonymiser et notifier une violation](02-tp.md) | TP |
| [Aide-mémoire – Conservation, sécurité et violations](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Cas de violation MédiaGroup (fictif)](annexe-cas-mediagroup.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** (S07) : droits des personnes | Oral |
| 0 h 20 – 1 h 20 | **Cours** : conservation, sécurité, sous-traitance, violations | Cours et questions |
| 1 h 20 – 2 h 20 | **TP partie A** : purge d'une base et de journaux | Binôme |
| 2 h 20 – 2 h 50 | **TP partie B** : pseudonymisation | Binôme |
| 2 h 50 – 3 h 40 | **TP partie C** : cas de violation, notification à la CNIL | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Scripts de purge, réponses sur la pseudonymisation et projet de notification, nommés `RENDU-B3-S08-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- **Corrigé :** dans `corriges/` à la racine du dépôt (hors du site publié).
- Les durées de conservation du cours sont des **ordres de grandeur** tirés de textes et de recommandations ; **à faire relire avant diffusion** (elles évoluent). Les statistiques et montants de l'ancienne version ont été retirés faute de source.
- Le cas MédiaGroup est **fictif**. La vidéosurveillance et le RGPD au travail (ancienne séance 8) sont déplacés vers le dépôt CEJMA, où ils s'insèrent dans le droit du travail.
- Vérifier sur le site de la CNIL le formulaire de notification et le délai de 72 heures avant de s'entraîner.

</details>
