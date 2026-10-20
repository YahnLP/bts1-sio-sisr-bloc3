# S17 – Gérer un incident de sécurité et préserver les preuves

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S17 (séance 17 sur 19) – Phase 4 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Incident et preuves : réutilise S05, S08, S09 et S15 ; prépare l'étude de cas. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S05 (sauvegardes), S08 (violations), S09 (preuve, plainte), S15 (journaux). |
| **Matériel** | VM Debian de laboratoire ; fiches papier ou traitement de texte |
| **Compétences travaillées** | B3.2 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Quand une attaque a réussi, que faire dans l'ordre, qui prévenir, et comment garder des preuves utilisables ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Décrire** les phases d'une réponse à incident (préparation, détection, qualification, confinement, éradication, restauration, retour d'expérience) ;
2. **Qualifier** un incident et décider des premières actions dans l'ordre ;
3. **Identifier** qui prévenir (direction, DPO, CNIL, assureur, police, clients) et dans quel délai ;
4. **Collecter** des informations volatiles avec un script et en garantir l'intégrité par une empreinte ;
5. **Rédiger** une main courante et un retour d'expérience.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Réponse à incident : méthode, communication et preuves](01-cours.md) | Cours |
| [TP – Gérer un rançongiciel (exercice de crise) et collecter des preuves](02-tp.md) | TP |
| [Aide-mémoire – Réponse à incident et preuves](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Cas du cabinet Delmas (fictif) : déroulé de la crise](annexe-cas-delmas.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S08) : violation de données, quels délais ? | Oral |
| 0 h 15 – 1 h 15 | **Cours** : méthode, rôles, communication, preuves | Cours et questions |
| 1 h 15 – 2 h 50 | **TP partie A** : exercice de crise « Delmas » (injects successifs) | Groupes de 3 ou 4 |
| 2 h 50 – 3 h 30 | **TP partie B** : collecte de preuves sur une VM | Binôme |
| 3 h 30 – 3 h 40 | **TP partie C** : retour d'expérience | Collectif |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Main courante de l'exercice, fiche de décisions, dossier de preuves (empreintes) et retour d'expérience, nommés `RENDU-B3-S17-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- L'exercice est conçu en **injects** : l'enseignant (ou un élève) distribue les éléments de l'annexe un par un, pour simuler le temps réel. Ne pas distribuer l'annexe entière dès le début.
- Les conseils de communication sont à confirmer avec les recommandations en vigueur de l'ANSSI, de Cybermalveillance.gouv.fr et de la CNIL.
- Le script de collecte a été **testé** sur une VM Linux (sans la partie `journalctl` selon le système). Le cas Delmas est **fictif**. Le cas de violation MédiaGroup de la séance S08 sert de comparaison.

</details>
