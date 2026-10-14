# Corrigé S05

## Partie A (une solution défendable)

| Donnée | RPO | RTO | Rétention |
|---|---|---|---|
| Code source | 24 h (sauvegarde quotidienne, voire plus fréquente si poussée sur un dépôt Git) | 1 journée | 30 quotidiennes, 12 mensuelles |
| Base de facturation | 24 h maximum, journaux de transactions si la direction veut moins | 4 h (« demi-journée ») | 12 mensuelles, **10 ans** pour les pièces comptables (à confirmer) |
| Documents administratifs | 24 h | quelques jours | 12 mois |

Budget : un NAS (copie locale) + un disque externe **tournant et débranché** (copie hors ligne) restent dans 500 € ; le stockage en ligne chiffré sert de copie hors site. Un seul support en réseau permanent ne résiste pas à un rançongiciel.

## Partie B

- Le fichier `contrat1.txt` contient l'avenant après restauration.
- `check` renvoie « no errors were found ».
- Après `rm -rf ~/depot-sauvegarde`, seule la copie `/mnt/copie-hors-ligne/depot` répond.
- La copie dans `/mnt/...` est sur **la même machine** : pas hors site, ni un autre support. En vrai : disque débranché ou stockage distant immuable.

## Partie C

- Perte de la phrase de passe = **perte définitive** des données (sauf copie des en-têtes LUKS et de la clé).
- Conserver une copie de la phrase de passe **dans un coffre ou un gestionnaire de mots de passe de l'entreprise**, accessible à deux personnes, **pas** sur le même support.
