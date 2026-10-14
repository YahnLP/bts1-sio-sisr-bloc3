# Aide-mémoire – Mini-PKI et HTTPS

*BTS SIO SISR 1re année – Bloc 3 – S12*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Circuit d'un certificat de serveur

1. Le serveur génère **clé privée** + **CSR** (nom, clé publique).
2. L'AC **vérifie** puis **signe** → certificat.
3. Le serveur installe **certificat + clé privée**.
4. Le client fait confiance à l'AC (racine dans son magasin).

La clé privée du serveur **ne bouge pas**.

## Contrôler un certificat

| Contrôle | Commande |
|---|---|
| Sujet, émetteur, dates | `openssl x509 -in c.crt -noout -subject -issuer -dates` |
| Noms (SAN) et type | `openssl x509 -in c.crt -noout -ext subjectAltName,basicConstraints` |
| Chaîne | `openssl verify -CAfile ca.crt c.crt` |
| Expire dans 30 jours ? | `openssl x509 -in c.crt -noout -checkend $((86400*30))` |
| Ce que sert un serveur | `openssl s_client -connect hote:443 -servername hote -showcerts` |
| Nom contrôlé | `openssl s_client … -verify_hostname hote` |
| Version de TLS | `openssl s_client … -tls1_2` ou `-tls1_3` |

## Erreurs courantes

| Erreur | Cause | Vérifier |
|---|---|---|
| Nom ne correspond pas | Nom absent du **SAN** | SAN |
| Expiré | Date dépassée ou **horloge fausse** | `-dates`, `date` |
| Autorité inconnue | AC absente du magasin ; **chaîne incomplète** | `s_client -showcerts` |
| Révoqué | Dans la **CRL** | `verify -crl_check` |

## nginx

```nginx
listen 443 ssl;
ssl_certificate     /chemin/www.crt;
ssl_certificate_key /chemin/www.key;
ssl_protocols       TLSv1.2 TLSv1.3;
```

`sudo nginx -t` avant `sudo systemctl reload nginx`. Redirection : `return 301 https://$host$request_uri;`.

## AC interne

| Bonne pratique | |
|---|---|
| Clé de l'AC **hors ligne**, protégée | Intermédiaire pour le quotidien |
| Certificats **courts**, renouvellement **automatisé** | Surveiller les expirations |
| `CA:FALSE` pour les serveurs | Moindre privilège |
| Installer une AC = lui faire **confiance pour tout** | Retirer les AC de laboratoire |
