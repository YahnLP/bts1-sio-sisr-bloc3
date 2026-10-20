# S10 – Chiffrement symétrique, hachage et intégrité

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S10 (séance 10 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Chiffrement symétrique et hachage : prérequis de S11 et S13. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S03 (empreintes de mots de passe) et S05 (chiffrement d'un volume). |
| **Matériel** | VM Debian de laboratoire (`openssl`, `gpg`, `coreutils`) |
| **Compétences travaillées** | B3.2 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment garder un fichier secret, et comment être sûr qu'il n'a pas été modifié ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Distinguer** confidentialité, intégrité, authenticité et non-répudiation, et le moyen cryptographique de chacune ;
2. **Expliquer** le chiffrement symétrique, AES et le rôle du mode opératoire (ECB, CBC, GCM) ;
3. **Calculer** et **vérifier** une empreinte (SHA-256) et un code d'authentification (HMAC) ;
4. **Chiffrer** et **déchiffrer** un fichier avec OpenSSL et GnuPG ;
5. **Constater** qu'un chiffrement sans contrôle d'intégrité n'empêche pas la falsification.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Chiffrement symétrique, hachage et intégrité](01-cours.md) | Cours |
| [TP – Chiffrer un fichier, vérifier une empreinte et constater les limites d'un mauvais mode](02-tp.md) | TP |
| [Aide-mémoire – Chiffrement symétrique et hachage](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 20 | **Rappel d'amorçage** (S03, S05) : empreinte d'un mot de passe, volume chiffré | Oral |
| 0 h 20 – 1 h 20 | **Cours** : objectifs, symétrique, AES et modes, hachage, HMAC | Cours et questions |
| 1 h 20 – 2 h 00 | **TP partie A** : empreintes et vérification d'intégrité | Binôme |
| 2 h 00 – 2 h 50 | **TP partie B** : chiffrement AES avec OpenSSL et GnuPG | Binôme |
| 2 h 50 – 3 h 40 | **TP parties C et D** : modes opératoires, falsification, HMAC | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Réponses aux questions et traces des commandes (copies d'écran), nommées `RENDU-B3-S10-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Les paramètres d'OpenSSL (`-pbkdf2 -iter 600000`) sont des valeurs de confort pour le laboratoire ; à ajuster à la version installée et aux recommandations ANSSI et OWASP en vigueur.
- L'expérience de falsification (partie D) a été **testée** : un bit modifié dans un fichier CBC se déchiffre **sans erreur**, avec un bloc illisible et un bit changé dans le bloc suivant.
- `openssl enc` ne gère pas les modes authentifiés (GCM) : on cite GCM dans le cours sans le manipuler ici.

</details>
