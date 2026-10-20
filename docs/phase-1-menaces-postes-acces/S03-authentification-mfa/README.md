# S03 – Authentification : mots de passe et MFA

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S03 (séance 3 sur 19) – Phase 1 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Authentification et MFA : prérequis de S04, S10 (empreintes) et S15 (force brute). Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S01 (menaces), S02 (empreinte, défense en profondeur) ; notions de comptes Windows et Linux (bloc 2, S02). |
| **Matériel** | VM Debian de laboratoire (paquets `john` et `oathtool`) ; VM Windows de laboratoire ; gestionnaire de mots de passe (KeePass ou équivalent libre) |
| **Compétences travaillées** | B3.3 (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment s'assurer que celui qui se connecte est bien celui qu'il prétend être, même quand un mot de passe fuite ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Distinguer** identification, authentification et autorisation ;
2. **Calculer** l'entropie d'un mot de passe et **comparer** longueur, complexité et phrase de passe ;
3. **Décrire** les attaques sur les mots de passe (force brute, dictionnaire, réutilisation, hameçonnage) et leurs parades ;
4. **Expliquer** comment un mot de passe doit être stocké (empreinte salée, fonction lente) ;
5. **Comparer** les facteurs d'authentification (SMS, application TOTP, clé FIDO2) et **justifier** un choix ;
6. **Rédiger** une politique de mots de passe argumentée avec les recommandations de la CNIL.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Authentification : mots de passe et authentification multifacteur](01-cours.md) | Cours |
| [TP – Mesurer la force d'un mot de passe, casser des empreintes faibles et mettre en place un second facteur](02-tp.md) | TP |
| [Aide-mémoire – Authentification et mots de passe](03-aide-memoire.md) | Aide-mémoire |
| [Annexe – Fichiers du laboratoire (empreintes et dictionnaire)](annexe-labo-empreintes.md) | Support du TP |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** : comment un attaquant obtient-il un mot de passe ? (recueil des idées) | Oral |
| 0 h 20 – 1 h 20 | **Cours** : authentification, entropie, attaques, stockage, MFA | Cours et questions |
| 1 h 20 – 1 h 50 | **TP partie A** : calculs d'entropie | Individuel |
| 1 h 50 – 2 h 40 | **TP partie B** : casser des empreintes faibles, constater l'effet du sel | Binôme |
| 2 h 40 – 3 h 20 | **TP parties C et D** : second facteur TOTP, politique de mots de passe | Binôme |
| 3 h 20 – 4 h 00 | **Gestionnaire de mots de passe** et **bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Compte rendu du TP (calculs, captures, politique de mots de passe argumentée), nommé `RENDU-B3-S03-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Les seuils chiffrés viennent de la page de la CNIL « Mots de passe : recommandations pour maîtriser sa sécurité » (relue en octobre 2026). Les relire avant diffusion : la CNIL peut les faire évoluer.
- Les empreintes du laboratoire sont calculées en MD5 **volontairement** (format faible, pour que l'attaque aboutisse vite) ; en production on utilise des fonctions lentes et salées.
- Hypothèse de calcul du cours : 10 milliards d'essais par seconde pour une attaque hors ligne sur un format rapide ; c'est un ordre de grandeur, pas une mesure.

</details>
