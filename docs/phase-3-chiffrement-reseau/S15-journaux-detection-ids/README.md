# S15 – Journaux, détection et réaction automatique

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S15 (séance 15 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Journaux et détection : prérequis de S16 et S17. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S03 (force brute), S14 (architecture, pare-feu) ; lecture de commandes shell (`grep`, `awk`). |
| **Matériel** | Deux VM Debian de laboratoire (`fail2ban`, `suricata`, `nmap`, `rsyslog`) ; VM Windows de laboratoire pour l'observateur d'événements |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment savoir qu'une attaque est en cours, et comment réagir automatiquement ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Identifier** les journaux utiles (système, authentification, pare-feu, applications) et les événements Windows à surveiller ;
2. **Extraire** d'un journal les indices d'une force brute avec `grep`, `awk` et `sort` ;
3. **Configurer** Fail2ban pour bannir automatiquement une adresse qui multiplie les échecs ;
4. **Distinguer** IDS et IPS, détection par signatures et par comportement ;
5. **Écrire** une règle Suricata simple et **vérifier** qu'elle déclenche une alerte.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Journalisation, détection d'intrusion (IDS/IPS) et réaction](01-cours.md) | Cours |
| [TP – Analyser des journaux, bloquer une force brute avec Fail2ban et détecter un scan avec Suricata](02-tp.md) | TP |
| [Aide-mémoire – Journaux et détection](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S14) : que voit-on d'une attaque quand on n'a pas de journaux ? | Oral |
| 0 h 15 – 1 h 10 | **Cours** : journaux, centralisation, détection, IDS/IPS, réaction | Cours et questions |
| 1 h 10 – 2 h 00 | **TP partie A** : analyse d'un journal d'authentification | Binôme |
| 2 h 00 – 2 h 50 | **TP partie B** : Fail2ban | Binôme |
| 2 h 50 – 3 h 40 | **TP partie C** : Suricata et événements Windows | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Résultats d'analyse, configuration Fail2ban et règle Suricata avec captures, nommés `RENDU-B3-S15-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- L'analyse de la partie A est **testée** (script de génération du journal et commandes `grep`/`awk`). Fail2ban et Suricata sont standard sous Debian mais **non exécutés** pendant la rédaction : à tester sur les VM (noms d'interface, chemins des règles à adapter à la version).
- Les adresses du journal généré sont des adresses réservées à la documentation (`192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`).
- Faire attention à **ne jamais bannir l'adresse du poste d'administration** pendant les tests (ajouter `ignoreip`).
- Les identifiants d'événements Windows cités sont à confirmer sur la documentation de Microsoft pour la version utilisée.

</details>
