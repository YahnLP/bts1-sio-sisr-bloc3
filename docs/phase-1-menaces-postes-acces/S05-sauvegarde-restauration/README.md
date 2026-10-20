# S05 – Sauvegarde, supports amovibles et restauration

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S05 (séance 5 sur 19) – Phase 1 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Sauvegarde et restauration : prérequis de S10 et S17 ; seule séance sur ce point. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S01 (rançongiciel), S04 (droits) ; sauvegarde vue côté exploitation au bloc 2 (S16). |
| **Matériel** | VM Debian de laboratoire (paquets `restic` et `cryptsetup`) ; calculatrice ou tableur |
| **Compétences travaillées** | B3.4 · B3.3 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Quand tout est chiffré ou détruit, que reste-t-il, et en combien de temps peut-on redémarrer ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Expliquer** les objectifs de reprise (RPO, RTO) et les plans associés (PCA, PRA) ;
2. **Distinguer** sauvegarde complète, différentielle et incrémentielle, et **choisir** selon le besoin ;
3. **Appliquer** la règle 3-2-1 et **justifier** qu'une copie hors ligne ou immuable protège d'un rançongiciel ;
4. **Distinguer** une sauvegarde d'un RAID, d'un instantané ou d'une réplication ;
5. **Sauvegarder, restaurer et vérifier** des données avec un outil chiffré et dédupliqué ;
6. **Chiffrer** un support amovible et **rédiger** une règle d'usage des supports.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Sauvegarde, supports amovibles et restauration](01-cours.md) | Cours |
| [TP – Concevoir une stratégie de sauvegarde, la tester et chiffrer un support](02-tp.md) | TP |
| [Aide-mémoire – Sauvegarde et restauration](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Cas SimTech (fictif)](annexe-cas-simtech.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** (S01) : que reste-t-il après un rançongiciel ? | Oral |
| 0 h 20 – 1 h 20 | **Cours** : objectifs de reprise, types, règle 3-2-1, politique, supports amovibles | Cours et questions |
| 1 h 20 – 1 h 50 | **TP partie A** : analyser le besoin de SimTech (RPO, RTO, rétention, budget) | Binôme |
| 1 h 50 – 2 h 50 | **TP partie B** : sauvegarder, détruire, restaurer, vérifier | Binôme |
| 2 h 50 – 3 h 20 | **TP partie C** : volume chiffré | Binôme |
| 3 h 20 – 4 h 00 | **TP partie D** : plan de tests et règle d'usage des supports, **bilan de compétences** | Binôme puis individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Stratégie de sauvegarde de SimTech, preuves de la restauration (captures datées), règle d'usage des supports, nommés `RENDU-B3-S05-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Cette séance traite la sauvegarde sous l'angle **sécurité** (rançongiciel, chiffrement, restauration prouvée). L'exploitation (planification, outils d'entreprise) est vue au bloc 2 (S16).
- Le cas GitLab (31 janvier 2017) est documenté dans la publication d'analyse de l'éditeur ; les détails sont à vérifier sur ce document avant de les citer à la classe.
- Les commandes `restic` et `cryptsetup` sont à tester sur la VM de la classe avant la séance (versions des paquets).

</details>
