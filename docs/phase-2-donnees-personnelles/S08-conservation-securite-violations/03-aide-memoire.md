# Aide-mémoire – Conservation, sécurité et violations

*BTS SIO SISR 1re année – Bloc 3 – S08*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Conservation

| Phase | Contenu |
|---|---|
| Base active | Finalité en cours |
| Archive intermédiaire | Obligation légale ou litige ; accès restreint |
| Suppression ou anonymisation | Plus de justification |

> [!WARNING]
> Les durées sont à **confirmer** (juridique, CNIL, Légifrance) : factures 10 ans, candidatures non retenues 2 ans au plus, prospects 3 ans après le dernier contact, journaux de connexion 1 an, vidéosurveillance un mois au plus en pratique.

## Pseudonymisation ou anonymisation

| | Pseudonymisation | Anonymisation |
|---|---|---|
| Ré-identification | Possible avec une info à part | Impossible |
| Donnée personnelle ? | **Oui** | Non |

Un hachage **sans sel** de petit espace de valeurs se retrouve par essais.

## Commandes de purge

| But | Commande |
|---|---|
| Compter avant de supprimer | `sqlite3 base.db "SELECT COUNT(*) FROM t WHERE date < date('now','-3 years');"` |
| Supprimer | `sqlite3 base.db "DELETE FROM t WHERE date < date('now','-3 years');"` |
| Fichiers de plus d'un an (essai) | `find dossier -name '*.log' -mtime +365 -print` |
| Les supprimer | `find dossier -name '*.log' -mtime +365 -delete` |
| Planifier à 2 h chaque nuit | `0 2 * * * /chemin/script.sh` (dans `crontab -e`) |
| Tester la rotation | `sudo logrotate -d /etc/logrotate.conf` |
| Empreinte salée | `printf '%s' 'valeur' \| openssl dgst -sha256 -hmac "$SEL"` |

## Sous-traitance (article 28)

Contrat : **objet et durée · données et personnes · instructions documentées · confidentialité · sécurité · sous-traitants ultérieurs · aide aux droits et aux violations · sort des données · audit**.

## Violation de données

1. **Contenir** et préserver les preuves.
2. **Documenter** dans le registre des violations (toujours).
3. **Évaluer** le risque : nature des données, volume et personnes, facilité d'exploitation.
4. **Notifier la CNIL** sous **72 h** si risque.
5. **Informer les personnes** si risque **élevé**.

La notification : nature, catégories et nombre, contact, conséquences probables, mesures.
