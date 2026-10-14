# Aide-mémoire – Authentification et mots de passe

*BTS SIO SISR 1re année – Bloc 3 – S03*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les trois facteurs

| Facteur | Exemples |
|---|---|
| Ce que je **sais** | Mot de passe, PIN |
| Ce que je **possède** | Téléphone, clé de sécurité, carte |
| Ce que je **suis** | Empreinte, visage |

**MFA** = au moins **deux facteurs de types différents**.

## Entropie

- **Entropie (bits) = L × log₂(N)**, pour un tirage **aléatoire**. Un bit de plus double le nombre d'essais.
- CNIL (à relire sur cnil.fr) : **80 bits** pour un mot de passe seul, **50 bits** avec restriction d'accès.
- Exemples cités : 12 caractères de 4 types, 14 caractères de 3 types, ou phrase de passe de 7 mots.
- Pas de renouvellement périodique pour les comptes standards ; blocage ou temporisation après échecs.

## Attaques et parades

| Attaque | Parade |
|---|---|
| Force brute | Longueur, blocage après échecs |
| Dictionnaire | Pas de mot courant, refuser les mots de passe compromis |
| Bourrage d'identifiants | **Un mot de passe par service**, MFA |
| Pulvérisation | Détection dans les journaux, MFA |
| Hameçonnage | Sensibilisation, clé FIDO2 |

## Stockage

**Empreinte + sel aléatoire + fonction lente (Argon2, scrypt, bcrypt).** Jamais en clair.

## Second facteur

| Type | À retenir |
|---|---|
| SMS | Mieux que rien, interceptable |
| TOTP | Code de 6 chiffres, 30 s, secret partagé |
| Notification | Risque de lassitude |
| FIDO2 / passkey | Résiste à l'hameçonnage |

## Commandes du TP

| But | Commande |
|---|---|
| Entropie | `python3 -c "import math; print(12*math.log2(95))"` |
| Empreinte MD5 sans sel | `echo -n texte \| md5sum` |
| Empreinte salée | `openssl passwd -6 texte` |
| Casser des MD5 faibles (labo) | `john --format=raw-md5 --wordlist=dico.txt empreintes.txt` |
| Code TOTP | `oathtool --totp -b SECRET` |
| Politique locale Windows | `net accounts` |
