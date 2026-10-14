# Corrigé S11

## Partie A

1. La clé **publique** (`alice.pub`) se publie ; la clé **privée** (`alice.key`) ne quitte jamais son propriétaire.
2. Lecture et écriture pour le propriétaire seul ; aucun droit pour le groupe et les autres.
3. `msg.rsa` fait **384 octets** : la taille du module RSA 3072 bits. Quel que soit le message court, le chiffré a la taille de la clé.
4. `data too large for key size` : le message dépasse ce que la clé peut chiffrer en une opération.
5. La **clé de session** chiffrée avec la clé publique d'Alice. On supprime `session.key` pour qu'il ne reste que la version chiffrée : sinon n'importe qui lirait la clé en clair.
6. **Non** : `alice.pub` ne permet que de **chiffrer** pour Alice. Seule la clé privée déchiffre `session.key.rsa`, donc `gros.enc`.
7. AES chiffre le gros fichier (rapide, taille quelconque) ; RSA chiffre la clé (petite taille, pas besoin de secret partagé). Les deux combinent **vitesse** et **échange sans secret préalable**.
8. TLS, GnuPG/OpenPGP, S/MIME, SSH, WireGuard (échange de clés puis chiffrement symétrique).

## Partie B

9. Seule la détentrice de la clé **privée** produit la signature ; **tout le monde** peut la vérifier avec la clé publique.
10. La **non-répudiation** (la clé privée n'est détenue que par le signataire, contrairement à une clé partagée) et la vérification par des tiers sans partager de secret.
11. Si l'attaquant fournit sa propre clé publique en disant « c'est celle d'Alice », la vérification réussit pour **sa** signature. Il faut un moyen de **lier** la clé à une identité : le certificat.
12. **Non** : le document reste lisible. Pour la confidentialité, il faut le chiffrer.

## Partie C

13. Oui, les deux secrets sont identiques. Chacun a utilisé **sa** clé privée et la clé **publique** de l'autre : aucune clé privée n'a été partagée.
14. **Non** : en pratique, impossible de retrouver le secret à partir des seules valeurs publiques (problème mathématique difficile).
15. Rien ne prouve que `b.pub` vient réellement de Bob : un attaquant peut s'intercaler (**homme du milieu**) et mener un échange avec chacun. Il faut **signer** les valeurs (certificat).
16. Les clés sont **générées pour une session** puis jetées. Si la clé de longue durée du serveur est volée plus tard, les sessions passées enregistrées restent indéchiffrables : c'est la **confidentialité persistante**.

## Partie D

17. Réponses variables. La racine est installée dans le **magasin de certificats** du système ou du navigateur (affichable dans les paramètres de sécurité).
18. Souvent de quelques mois ou moins. Les durées courtes limitent la fenêtre d'abus d'une clé volée et incitent à **automatiser** le renouvellement.
19. **Identiques** : le certificat est signé par lui-même (auto-signé). Personne d'autre ne garantit l'identité.
20. **Non** : l'émetteur n'est pas dans son magasin de confiance ; le navigateur affiche un avertissement.
21. `CA:TRUE` signifie que le certificat peut **signer d'autres certificats** : c'est un défaut pour un certificat de serveur (principe du moindre privilège). Un certificat de serveur doit avoir `CA:FALSE`.
22. L'**empreinte** permet de comparer le certificat avec une valeur communiquée par un canal différent (par exemple par téléphone) ; c'est un moyen de s'assurer qu'on n'a pas reçu un certificat de remplacement.

## Synthèse

| Situation | Outil | Ce qui est utilisé |
|---|---|---|
| Gros fichier confidentiel à Alice | Chiffrement hybride | Clé de session AES + clé **publique** d'Alice |
| Prouver que j'ai écrit un document | Signature | Ma clé **privée** (vérifiée avec ma publique) |
| Secret commun à distance | Diffie-Hellman (X25519) | Valeurs publiques échangées, clés privées gardées |
| Lier une clé publique à Alice | Certificat X.509 | Signature d'une AC de confiance |
