# Corrigé S10

## Partie A

1. SHA-256 : **64** caractères hexadécimaux = 256 bits. MD5 : **32** = 128 bits.
2. Avant l'ajout : `rapport.txt: OK`. Après : `rapport.txt: FAILED` (et un ​message indiquant que 1 somme ne correspond pas).
3. **Non** : l'attaquant remplace les deux. L'empreinte doit venir d'un **canal sûr** et distinct du fichier (site officiel en HTTPS, publication séparée), ou être **signée** (S11).
4. Sur la page officielle de téléchargement de l'éditeur, en HTTPS (fichier `SHA256SUMS`, souvent signé). Un site non fiable pourrait publier l'empreinte d'un fichier piégé.

## Partie B

5. Les 8 premiers octets sont la chaîne `Salted__`, les 8 ​suivants le **sel**. Le sel n'est pas secret : il sert à rendre la dérivation de clé **unique** à chaque chiffrement et à empêcher le calcul à l'avance de tables ; la sécurité repose sur le mot de passe.
6. Message `bad decrypt` : le déchiffrement échoue (le remplissage final est invalide). Dans certains cas rares, le déchiffrement « ​réussit » avec des données incohérentes : c'est pour cela que l'on ajoute un contrôle d'intégrité.
7. **Non** : le sel est tiré au hasard à chaque fois, donc la clé dérivée et les fichiers diffèrent. Cela empêche de repérer que deux fichiers ont le même contenu.
8. Le mot de passe se retrouve dans l'historique du shell (`history`) et dans la liste des processus (`ps`). On utilise `-pass stdin`, `-pass file:chemin` (fichier en droits 600) ou la saisie ​interactive.
9. **AES256** en mode CFB ; dérivation **S2K itérée et salée** (`s2k 3`) avec une fonction de hachage SHA-512 (selon la version).
10. **GnuPG/OpenPGP** est un format normalisé, lisible par de nombreux outils, avec en-tête structuré ; le format `openssl enc` est propre à ​OpenSSL et rudimentaire (pas d'authentification).

## Partie C

11. ECB : **4 blocs identiques** (les A) puis **2 blocs identiques** (les B). CBC : **aucun** bloc identique.
12. Les répétitions révèlent la **structure** : une image reste reconnaissable, des enregistrements identiques se repèrent, on peut déduire des informations sans la clé.
13. Si le IV était réutilisé, deux messages ​commençant pareil auraient le même début chiffré : l'attaquant en déduit des informations. Il doit être **imprévisible** (CBC) ou **unique** (CTR, GCM), mais pas secret.

## Partie D

14. L'espace du deuxième bloc de clair est devenu un point d'exclamation (`tiel!: budget 2027` au lieu de `tiel : budget 2027`). Sur un virement ou un ​fichier de configuration, l'attaquant peut changer une valeur **sans connaître la clé** et sans erreur au déchiffrement.
15. Non : ils diffèrent. Le destinataire qui recalcule le HMAC constate qu'il ne correspond pas à celui reçu et **rejette** le fichier **avant** de le déchiffrer.
16. Non : il lui faudrait la **clé du HMAC**. Il peut modifier le fichier mais pas produire le HMAC correspondant.
17. Pour ne pas ​mélanger les rôles : la compromission d'une clé ne doit pas compromettre l'autre (bonne pratique : une clé par usage).
18. **AES-GCM** (chiffrement authentifié). Il est utilisé dans **TLS 1.2 et 1.3**, dans **IPsec** et **WireGuard** (ChaCha20-Poly1305 pour ce dernier, de la même famille de chiffrement authentifié).

## Synthèse

| Besoin | Outil | Limite |
|---|---|---|
| Confidentialité | `openssl enc` AES-256-CBC, `gpg --symmetric` | Dépend du mot de passe ; pas d'intégrité |
| Intégrité ​simple | `sha256sum` | N'authentifie pas : l'attaquant remplace fichier et empreinte |
| Intégrité + authenticité | HMAC | Clé partagée : pas de non-répudiation |
