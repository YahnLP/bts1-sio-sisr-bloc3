# Corrigé S12

## Partie A

1. 10 ans (3650 jours). Remplacer la racine oblige à la **redéployer sur tous les clients** : on la fait donc durer longtemps et on garde sa clé hors ligne. Un certificat de serveur, plus exposé, dure **peu** (90 jours dans le TP).
2. `private/ca.key`. Quiconque la copie peut **émettre des certificats valides pour n'importe quel nom**, acceptés par tous les clients qui font confiance à l'AC.
3. `CA:TRUE` : le certificat peut signer d'autres certificats. `CA:FALSE` : non (certificat « feuille »).

## Partie B

4. De « serveur » vers « AC » : la **CSR** (`www.csr`), qui contient la clé publique et les noms. La clé privée `www.key` ne sort jamais du serveur.
5. `OK` : la chaîne se vérifie jusqu'à l'AC fournie. Sans `-CAfile`, OpenSSL ne connaît pas l'AC (elle n'est pas dans son magasin), donc ne peut pas vérifier.
6. Une ligne par certificat émis (état `V` valide, date d'expiration, numéro de série, sujet) : un **inventaire** minimal avec les dates d'expiration.
7. Uniquement `www.lab.local` (SAN). Il **ne** serait **pas** valable pour `lab.local`.

## Partie C

8. `301 Moved Permanently` vers `https://www.lab.local/`.
9. Normalement `TLSv1.3` avec `TLS_AES_256_GCM_SHA384` (selon la version du serveur et du client).
10. `--cacert` : confiance limitée à **une** commande. `update-ca-certificates` : confiance pour **tout le système** : c'est le plus risqué.
11. Les deux fonctionnent si le serveur accepte TLS 1.2 et 1.3. Un client qui ne parle que TLS 1.0 ne peut **pas** se connecter : c'est voulu (versions obsolètes).

## Partie D

| Cas | Message | Cause | Correction |
|---|---|---|---|
| D1 | `Verification error: hostname mismatch` | Le nom demandé n'est pas dans le SAN | Utiliser le bon nom, ou émettre un certificat avec ce nom |
| D2 | `certificate has expired` | Dates hors validité | Renouveler ; surveiller les dates |
| D3 | `unable to get local issuer certificate` / certificat non vérifié | AC absente du magasin | Installer l'AC (si légitime) ou envoyer la chaîne complète |

12. `-checkend N` renvoie un code de sortie qui indique si le certificat expire dans les N secondes. Un script `cron` peut tester chaque nuit et alerter (courriel, supervision) si le code est non nul.
13. Réponse : ne pas continuer sans comprendre ; chercher l'erreur exacte et la corriger. Côté technique : vérifier nom, date, chaîne ; corriger le certificat ou déployer l'AC. Apprendre aux utilisateurs à ignorer les alertes les expose aux attaques réelles.
14. L'**horloge** du poste (ou du serveur) incorrecte : un poste dont la date est fausse voit des certificats « expirés » ou « pas encore valables ». Synchroniser avec NTP.

## Partie E

15. `R` : le certificat est **révoqué** (`V` pour valide, `E` pour expiré).
16. `error 23 … certificate revoked`.
17. Le certificat révoqué reste cryptographiquement valide : c'est **le client** qui consulte la CRL ou OCSP et refuse. Un client qui ne vérifie pas accepte encore le certificat volé.
18. Révoquer ; générer une nouvelle paire de clés ; émettre un nouveau certificat ; déployer ; publier la CRL ; chercher **comment la clé a fuité** ; rechercher des usages frauduleux dans les journaux ; documenter l'incident (S17).
19. Sinon la VM continue de faire confiance à une AC dont la clé privée est dans un dossier de TP, sans protection : un attaquant qui la récupérerait pourrait émettre des certificats acceptés par cette machine.
