# S07 – Collecte, consentement et droits des personnes

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S07 (séance 7 sur 19) – Phase 2 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Consentement et droits des personnes : seule séance sur ce point (B3.1) ; prérequis de S08. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S06 (notions, principes, registre). |
| **Matériel** | VM Debian de laboratoire (paquet `sqlite3`) ; navigateur web avec outils de développement |
| **Compétences travaillées** | B3.1 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Sur quel fondement collecter des données, comment en informer les personnes, et que répondre quand elles exercent leurs droits ? »*

> [!NOTE]
> **Recoupement avec d'autres séances.** Le consentement, les droits et les cookies sont aussi vus en [CEJM 1re année, S14 – RGPD : droits des personnes, cookies et prospection](https://yahnlp.github.io/bts1-sio-sisr-cejma/phase-3-numerique-et-droit/S14-rgpd-droits/). Selon l'ordre de vos séances, la première pose les bases et la seconde les reprend en rappel (15 à 20 minutes). Ici, garder la mise en œuvre technique (collecte, demande d'accès).

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Choisir** une base légale adaptée à un traitement (les six bases de l'article 6) ;
2. **Reconnaître** un consentement valide (libre, spécifique, éclairé, univoque) et un consentement non conforme ;
3. **Rédiger** les mentions d'information d'un formulaire de collecte ;
4. **Analyser** le comportement d'un site vis-à-vis des cookies et traceurs ;
5. **Citer** les droits des personnes et les délais de réponse ;
6. **Traiter** techniquement une demande d'accès et une demande d'effacement sur une base de données.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Collecte, base légale, consentement et droits des personnes](01-cours.md) | Cours |
| [TP – Traiter une demande d'accès, rédiger les mentions d'information et analyser une bannière de cookies](02-tp.md) | TP |
| [Aide-mémoire – Collecte, consentement et droits](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** (S06) : principes de l'article 5 | Oral |
| 0 h 20 – 1 h 20 | **Cours** : bases légales, consentement, information, cookies, droits | Cours et questions |
| 1 h 20 – 2 h 30 | **TP partie A** : demande d'accès et demande d'effacement sur une base de données | Binôme |
| 2 h 30 – 3 h 00 | **TP partie B** : mentions d'information et case de consentement | Binôme |
| 3 h 00 – 3 h 40 | **TP partie C** : analyse d'une bannière de cookies | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Réponse à la demande d'accès, mentions d'information et fiche d'analyse de bannière, nommées `RENDU-B3-S07-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Pour les cookies et traceurs, vérifier les lignes directrices et recommandations de la CNIL en vigueur (durée de conservation du choix, exemptions de consentement) : elles évoluent.
- Les cas CycloShop et les données sont **fictifs**. La partie C se fait sur des sites publics en **navigation privée**, sans saisir de donnée personnelle.
- Un point de vigilance pour la correction : la réponse à une demande d'accès ne doit contenir que les données de la personne **et d'elle seule**.

</details>
