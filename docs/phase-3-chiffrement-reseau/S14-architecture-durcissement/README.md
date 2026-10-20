# S14 – Architecture sécurisée et durcissement des systèmes

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S14 (séance 14 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Architecture et durcissement : prérequis de S15 et S16. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S04 (droits), S11 à S13 (TLS, VPN) ; notions d'adressage IP et de pare-feu. |
| **Matériel** | Deux VM Debian de laboratoire (`openssh-server`, `ufw`, `lynis`) ; éditeur de schémas ou papier |
| **Compétences travaillées** | B3.3 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment organiser un réseau et configurer un serveur pour qu'une intrusion soit difficile, et ses conséquences limitées ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Appliquer** les principes de défense en profondeur et de cloisonnement à un réseau d'entreprise ;
2. **Concevoir** des zones (LAN, DMZ, administration) et **écrire** la matrice de flux autorisés ;
3. **Durcir** un serveur Linux : services, SSH par clés, pare-feu, mises à jour ;
4. **Mesurer** le durcissement avec un outil d'audit (Lynis) avant et après ;
5. **Citer** les référentiels de bonnes pratiques (ANSSI, CIS) et leur usage.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Architecture réseau sécurisée et durcissement](01-cours.md) | Cours |
| [TP – Segmenter un réseau, filtrer et durcir un serveur Linux](02-tp.md) | TP |
| [Aide-mémoire – Architecture et durcissement](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S13) : le VPN est une porte d'entrée, que met-on derrière ? | Oral |
| 0 h 15 – 1 h 10 | **Cours** : défense en profondeur, zones, flux, durcissement, référentiels | Cours et questions |
| 1 h 10 – 2 h 00 | **TP partie A** : concevoir l'architecture d'une PME | Binôme |
| 2 h 00 – 3 h 40 | **TP parties B et C** : durcir un serveur Linux (audit, SSH, pare-feu, mises à jour) | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Schéma et matrice de flux, comparaison des scores d'audit et fichiers de configuration, nommés `RENDU-B3-S14-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Les commandes (`ufw`, `sshd`, `lynis`, `unattended-upgrades`) sont standard sous Debian mais **non exécutées** pendant la rédaction : à tester sur la VM. Le score Lynis dépend de la version et de la VM : on compare avant/après, on n'attend pas une valeur précise.
- Rappeler le risque de se **couper l'accès SSH** en configurant le pare-feu ; travailler avec une console de la VM ouverte.
- La mise en œuvre Windows (stratégies de groupe) pourrait faire l'objet d'un atelier du dépôt dédié (à décider) ; la matrice de flux du TP s'applique aux deux familles de systèmes.

</details>
