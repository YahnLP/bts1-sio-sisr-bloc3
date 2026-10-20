# S11 – Chiffrement asymétrique, signature et certificats

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S11 (séance 11 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Cœur** – Asymétrique, signature, certificats : prérequis de S13 et de S14 ; couvre la chaîne de confiance. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S10 (chiffrement symétrique, hachage, HMAC). |
| **Matériel** | VM Debian de laboratoire (`openssl`, `gpg`) ; navigateur web |
| **Compétences travaillées** | B3.2 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment échanger un secret avec quelqu'un qu'on n'a jamais rencontré, et comment être sûr de sa véritable identité ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Expliquer** le principe d'une paire de clés (publique / privée) et ses deux usages : chiffrer et signer ;
2. **Décrire** le chiffrement hybride et l'échange de clés Diffie-Hellman ;
3. **Générer** une paire de clés, **chiffrer** une clé de session, **signer** et **vérifier** un fichier avec OpenSSL ;
4. **Lire** un certificat X.509 et en citer les champs essentiels ;
5. **Décrire** les acteurs d'une PKI, la chaîne de confiance et le cycle de vie d'un certificat.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Chiffrement asymétrique, signature numérique, certificats et PKI](01-cours.md) | Cours |
| [TP – Générer des clés, chiffrer, signer et lire un certificat](02-tp.md) | TP |
| [Aide-mémoire – Asymétrique, signature, certificats](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S10) : limite de l'échange de clé symétrique | Oral |
| 0 h 15 – 1 h 20 | **Cours** : paires de clés, hybride, Diffie-Hellman, signature, certificats, PKI | Cours et questions |
| 1 h 20 – 2 h 10 | **TP partie A** : paire de clés et chiffrement hybride | Binôme |
| 2 h 10 – 2 h 50 | **TP partie B** : signature et vérification | Binôme |
| 2 h 50 – 3 h 40 | **TP parties C et D** : échange de clés, lecture d'un certificat | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Réponses aux questions et traces des commandes, nommées `RENDU-B3-S11-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)).
- Tailles de clés et algorithmes : recommandations de l'ANSSI et du NIST **à vérifier** avant diffusion ; elles évoluent.
- Toutes les commandes OpenSSL du TP ont été testées avec OpenSSL 3.0 (RSA 3072 bits, OAEP, signature SHA-256, X25519).
- La partie D utilise le navigateur sur un site public (consultation du certificat) : aucune donnée personnelle saisie.

</details>
