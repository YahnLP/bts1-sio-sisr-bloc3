# S16 – Audit de vulnérabilités

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S16 (séance 16 sur 19) – Phase 4 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Audit de vulnérabilités : seule séance sur ce point (B3.4, B3.5A). Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S09 (infractions, autorisation), S14 (durcissement), S15 (journaux, détection). |
| **Matériel** | VM Debian `adm` (`nmap`) et VM Debian cible `srv` (`nginx`, `vsftpd`) sur un réseau interne isolé |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment trouver les failles d'un système avant un attaquant, dans le cadre de la loi, et décider quoi corriger en premier ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Rédiger** une autorisation d'audit précisant périmètre, dates et règles ;
2. **Distinguer** découverte, scan de ports, détection de services et scan de vulnérabilités ;
3. **Utiliser** Nmap pour découvrir les machines, les ports ouverts et les versions de services ;
4. **Interpréter** une référence CVE et un score CVSS, et **prioriser** les corrections ;
5. **Rédiger** une fiche d'audit et un plan de remédiation.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Audit de vulnérabilités : cadre, scans, CVE et CVSS](01-cours.md) | Cours |
| [TP – Scanner un réseau de laboratoire, interpréter les résultats et rédiger une fiche d'audit](02-tp.md) | TP |
| [Aide-mémoire – Audit de vulnérabilités](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Résultat de scan du réseau de la société Brumaire (fictif)](annexe-rapport-nmap.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S09) : quand un scan devient-il une infraction ? | Oral |
| 0 h 15 – 1 h 10 | **Cours** : cadre, types d'audit, Nmap, CVE et CVSS, rapport | Cours et questions |
| 1 h 10 – 1 h 30 | **TP partie A** : autorisation d'audit | Binôme |
| 1 h 30 – 2 h 40 | **TP partie B** : scan du réseau de laboratoire | Binôme |
| 2 h 40 – 3 h 40 | **TP parties C et D** : interprétation, priorisation, fiche d'audit | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Autorisation, sorties Nmap, fiche d'audit et plan de remédiation, nommés `RENDU-B3-S16-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Les scans ne se font **que** sur le réseau de laboratoire isolé, avec l'accord de l'enseignant. **Jamais** sur Internet ni sur le réseau de l'établissement.
- Les commandes Nmap sont standard mais **non exécutées** pendant la rédaction (Nmap absent du bac à sable) ; à tester. Les scores CVSS cités (CVE-2017-0144, CVE-2011-2523, CVE-2021-44228) sont des valeurs courantes de la base NVD : **à vérifier** avant diffusion.
- L'annexe est un résultat de scan **inventé**.

</details>
