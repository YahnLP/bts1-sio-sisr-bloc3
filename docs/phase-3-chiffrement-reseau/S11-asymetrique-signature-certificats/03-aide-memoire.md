# Aide-mémoire – Asymétrique, signature, certificats

*BTS SIO SISR 1re année – Bloc 3 – S11*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Qui utilise quelle clé ?

| Opération | Clé utilisée | Qui peut |
|---|---|---|
| **Chiffrer** pour Alice | Clé **publique** d'Alice | Tout le monde |
| **Déchiffrer** | Clé **privée** d'Alice | Alice seule |
| **Signer** | Clé **privée** de l'émetteur | L'émetteur seul |
| **Vérifier** | Clé **publique** de l'émetteur | Tout le monde |

## Algorithmes

| Besoin | Algorithme |
|---|---|
| Chiffrement et signature | RSA (2048 mini, 3072 conseillé) |
| Signature moderne | ECDSA, Ed25519 |
| Échange de clés | ECDH, X25519, versions **éphémères** (ECDHE) |

## Hybride

Message → **AES** avec une clé de session. Clé de session → **RSA** (clé publique du destinataire). On envoie les deux.

## Certificat X.509

**Sujet · Émetteur · Validité · Clé publique · SAN · Usage · Série · Signature de l'AC.**

Chaîne : **racine** (magasin de confiance) → **intermédiaire** → **serveur**.

## PKI

AC · AE · titulaire · utilisateur · révocation (**CRL**, **OCSP**). Cycle : CSR → émission → déploiement → surveillance → renouvellement / révocation.

## Commandes OpenSSL

| But | Commande |
|---|---|
| Clé privée RSA | `openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:3072 -out k.key` |
| Clé publique | `openssl pkey -in k.key -pubout -out k.pub` |
| Chiffrer (petit message) | `openssl pkeyutl -encrypt -pubin -inkey k.pub -pkeyopt rsa_padding_mode:oaep -in m -out m.rsa` |
| Déchiffrer | `openssl pkeyutl -decrypt -inkey k.key -pkeyopt rsa_padding_mode:oaep -in m.rsa` |
| Signer | `openssl dgst -sha256 -sign k.key -out f.sig f` |
| Vérifier | `openssl dgst -sha256 -verify k.pub -signature f.sig f` |
| Certificat auto-signé | `openssl req -x509 -newkey rsa:2048 -nodes -keyout s.key -out s.crt -days 30 -subj "/CN=nom" -addext "subjectAltName=DNS:nom"` |
| Lire un certificat | `openssl x509 -in s.crt -noout -subject -issuer -dates -ext subjectAltName` |

> [!WARNING]
> `chmod 600` sur toute clé privée. Une clé privée dans un dépôt Git, un courriel ou un partage est une clé **compromise** : on la révoque et on la remplace.
