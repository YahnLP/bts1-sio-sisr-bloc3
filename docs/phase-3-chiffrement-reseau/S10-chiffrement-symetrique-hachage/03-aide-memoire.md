# Aide-mémoire – Chiffrement symétrique et hachage

*BTS SIO SISR 1re année – Bloc 3 – S10*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les quatre besoins

| Besoin | Moyen |
|---|---|
| Confidentialité | Chiffrement (AES) |
| Intégrité | Hachage (SHA-256), HMAC, signature |
| Authenticité | HMAC (clé partagée), signature (S11) |
| Non-répudiation | Signature |

## Symétrique et modes

| Mode | Verdict |
|---|---|
| **ECB** | À proscrire (motifs visibles) |
| **CBC** | Correct, **sans** contrôle d'intégrité |
| **CTR** | Rapide ; nonce **jamais** réutilisé |
| **GCM** | Chiffre **et** authentifie : recommandé |

**AES** : blocs de 128 bits ; clés de 128, 192 ou 256 bits. Clé dérivée d'un mot de passe : **PBKDF2**, scrypt ou Argon2 (lent, salé).

## Hachage

| Algorithme | Verdict |
|---|---|
| MD5, SHA-1 | Cassés (collisions) |
| **SHA-256** (SHA-2), SHA-3 | Standards |

## Commandes

| But | Commande |
|---|---|
| Empreinte | `sha256sum fichier` ou `openssl dgst -sha256 fichier` |
| Vérifier une liste | `sha256sum -c SHA256SUMS` |
| Chiffrer | `openssl enc -aes-256-cbc -pbkdf2 -iter 600000 -salt -in clair -out chiffre` |
| Déchiffrer | `openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in chiffre` |
| GnuPG symétrique | `gpg --symmetric --cipher-algo AES256 -o fichier.gpg fichier` |
| HMAC | `openssl dgst -sha256 -hmac "cle" fichier` |
| Octets en hexadécimal, un bloc par ligne | `od -v -An -tx1 -w16 fichier` |

> [!WARNING]
> `-pass pass:…` écrit le mot de passe dans l'**historique** de commandes et la liste des processus : à réserver au laboratoire. Utilise `-pass stdin`, `-pass file:…` ou la saisie interactive.
