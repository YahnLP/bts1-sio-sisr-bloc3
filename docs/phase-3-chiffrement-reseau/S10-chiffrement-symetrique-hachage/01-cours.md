# Cours – Chiffrement symétrique, hachage et intégrité

*BTS SIO SISR 1re année – Bloc 3 – S10 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S03 (empreintes de mots de passe) et S05 (chiffrement d'un volume).
> - **Matériel :** VM Debian de laboratoire (`openssl`, `gpg`, `coreutils`)

## À la fin de ce cours tu sauras

- [ ] **Distinguer** confidentialité, intégrité, authenticité et non-répudiation, et le moyen cryptographique de chacune ;
- [ ] **Expliquer** le chiffrement symétrique, AES et le rôle du mode opératoire (ECB, CBC, GCM) ;
- [ ] **Calculer** et **vérifier** une empreinte (SHA-256) et un code d'authentification (HMAC) ;
- [ ] **Chiffrer** et **déchiffrer** un fichier avec OpenSSL et GnuPG ;
- [ ] **Constater** qu'un chiffrement sans contrôle d'intégrité n'empêche pas la falsification.

## I. À quoi sert la cryptographie ?

La **cryptographie** est la science des secrets et de la preuve. Elle répond à quatre besoins :

| Besoin | Question | Moyen principal |
|---|---|---|
| **Confidentialité** | Seul le destinataire peut-il lire ? | **Chiffrement** |
| **Intégrité** | Le message a-t-il été modifié ? | **Hachage**, code d'authentification (HMAC), signature |
| **Authenticité** | Qui l'a vraiment envoyé ? | **Signature** numérique, certificat (S11) |
| **Non-répudiation** | L'auteur peut-il nier l'avoir envoyé ? | **Signature** numérique avec clé privée |

### Vocabulaire

| Terme | Sens |
|---|---|
| **Chiffrer** | Transformer un message clair en message illisible avec une clé |
| **Déchiffrer** | Retrouver le clair **avec** la clé |
| **Décrypter** | Retrouver le clair **sans** la clé (casser le chiffrement) |
| **Clé** | Secret qui paramètre l'algorithme |
| **Algorithme** | Procédé de chiffrement, **public** |

> [!NOTE]
> **Principe de Kerckhoffs** : la sécurité d'un système ne doit reposer que sur le **secret de la clé**, jamais sur le secret de l'algorithme. On n'invente pas son propre algorithme : on utilise ceux qui ont été éprouvés publiquement (AES, SHA-256…).

## II. Le chiffrement symétrique

### Principe

On utilise **la même clé** pour chiffrer et déchiffrer.

```mermaid
flowchart LR
    A["Message clair"] -->|"chiffrement<br/>avec la clé K"| B["Message chiffré"]
    B -->|"déchiffrement<br/>avec la <b>même</b> clé K"| C["Message clair"]
```

| Avantage | Limite |
|---|---|
| **Rapide**, adapté aux gros volumes (disque, fichier, flux réseau) | Il faut **partager la clé** de façon sûre |
| Mathématiquement robuste avec des clés longues | Avec *n* personnes qui échangent deux à deux, il faut *n(n−1)/2* clés : 10 personnes → 45 clés |

La limite de l'échange de clé est résolue par la cryptographie **asymétrique** (S11).

### AES

**AES** (*Advanced Encryption Standard*) est le chiffrement symétrique de référence, adopté comme standard américain en 2001. Il traite des **blocs de 128 bits** avec une clé de **128, 192 ou 256 bits**. À ce jour, aucune attaque pratique ne casse AES : les attaques réussissent sur les **mots de passe faibles** et les **mauvais usages**, pas sur l'algorithme. Un chiffrement par blocs se complète d'un **mode opératoire**, qui précise comment enchaîner les blocs.

### Les modes opératoires

| Mode | Principe | À retenir |
|---|---|---|
| **ECB** | Chaque bloc est chiffré **indépendamment** | **À proscrire** : deux blocs identiques donnent deux blocs chiffrés identiques, les motifs du clair restent visibles |
| **CBC** | Chaque bloc est mélangé au bloc chiffré précédent ; un **vecteur d'initialisation** (IV) aléatoire démarre la chaîne | Correct, mais **sans contrôle d'intégrité** |
| **CTR** | Transforme AES en chiffrement de flux avec un compteur et un **nonce** | Rapide ; **jamais** deux messages avec le même couple clé/nonce |
| **GCM** | CTR + **authentification** du message | Chiffre **et** détecte les modifications : à préférer pour les nouveaux usages (TLS, VPN) |

L'**IV** ou le **nonce** n'est pas secret, mais il doit être **unique** (ou aléatoire) à chaque chiffrement.

### De la clé au mot de passe

Un utilisateur retient un **mot de passe**, pas 256 bits aléatoires. On dérive la clé du mot de passe avec une fonction **lente et salée** (PBKDF2, scrypt, Argon2). L'option `-pbkdf2` d'OpenSSL applique PBKDF2 avec un nombre d'itérations. Comme en S03, la **force du chiffrement** est limitée par celle du **mot de passe**.

## III. Le hachage

Une **fonction de hachage** transforme n'importe quelle donnée en une **empreinte** de longueur fixe.

| Propriété | Signification |
|---|---|
| **Déterministe** | Même entrée, même empreinte |
| **Longueur fixe** | SHA-256 : 256 bits (64 caractères hexadécimaux) |
| **Effet d'avalanche** | Un seul bit modifié change l'empreinte en entier |
| **À sens unique** | On ne retrouve pas l'entrée à partir de l'empreinte |
| **Résistante aux collisions** | Impossible (en pratique) de trouver deux entrées de même empreinte |

| Algorithme | État |
|---|---|
| **MD5**, **SHA-1** | **Cassés** pour les collisions : à ne plus utiliser pour la sécurité |
| **SHA-2** (SHA-256, SHA-512) | Standard actuel |
| **SHA-3** | Standard alternatif |

### Usages

1. **Intégrité d'un fichier** : on compare l'empreinte publiée par l'éditeur avec celle du fichier téléchargé.
2. **Stockage de mots de passe** : on stocke l'empreinte **salée** et **lente**, jamais le mot de passe (S03).
3. **Preuve** : l'empreinte d'un journal ou d'un fichier prouve qu'il n'a pas changé (S09).

> [!WARNING]
> Une empreinte **seule** prouve que le fichier n'a pas été **altéré par erreur**, pas qu'il n'a pas été **remplacé par un attaquant** : si l'attaquant modifie le fichier **et** l'empreinte posée à côté, rien n'est détecté. Il faut une empreinte obtenue par un **canal sûr** (site officiel en HTTPS), un **HMAC** ou une **signature**.

### HMAC

Un **HMAC** calcule une empreinte à partir du message **et d'une clé secrète** partagée. Seul qui connaît la clé peut produire un HMAC valide : il garantit l'**intégrité** et l'**authenticité** (vis-à-vis de ceux qui détiennent la clé).

| | Hachage simple | HMAC | Signature (S11) |
|---|---|---|---|
| Clé | Aucune | Secrète partagée | Privée / publique |
| Intégrité | Oui | Oui | Oui |
| Authenticité | Non | Oui (entre porteurs de la clé) | Oui |
| Non-répudiation | Non | Non (la clé est partagée) | **Oui** |

## IV. Le chiffrement ne suffit pas

Chiffrer cache le contenu, mais **n'interdit pas de le modifier**. Avec un mode sans authentification (CBC), un attaquant qui change un bit du fichier chiffré provoque un bloc illisible et un changement **prévisible** dans le bloc suivant, **sans erreur au déchiffrement**. C'est pour cela qu'on utilise des modes **authentifiés** (GCM) ou un **HMAC** en plus du chiffrement : « *chiffrer, puis authentifier* ».

## V. Chiffrer en pratique

| Besoin | Outil |
|---|---|
| Chiffrer un disque ou une partition | **LUKS** (Linux), **BitLocker** (Windows) – voir S05 |
| Chiffrer un fichier avec un mot de passe | `openssl enc`, `gpg --symmetric`, 7-Zip (AES-256) |
| Chiffrer une sauvegarde | `restic` (chiffre par défaut, S05) |
| Protéger le trafic réseau | **TLS**, **VPN** (S11 à S13) |

## À retenir

- Quatre besoins : **confidentialité** (chiffrement), **intégrité** (hachage), **authenticité** et **non-répudiation** (signature).
- Symétrique = **même clé** des deux côtés : rapide, mais il faut partager la clé.
- **AES** est sûr ; le **mode** compte : **ECB** proscrit, **GCM** recommandé.
- Hachage = empreinte **à sens unique** ; **MD5 et SHA-1** sont cassés ; **SHA-256** est le standard.
- Une empreinte seule ne prouve pas l'**authenticité** ; le chiffrement seul ne prouve pas l'**intégrité**.
