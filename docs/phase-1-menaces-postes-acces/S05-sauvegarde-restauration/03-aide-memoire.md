# Aide-mémoire – Sauvegarde et restauration

*BTS SIO SISR 1re année – Bloc 3 – S05*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Objectifs de reprise

| Sigle | Sens |
|---|---|
| **RPO** | Perte de données maximale acceptable → fréquence |
| **RTO** | Interruption maximale acceptable → vitesse de restauration |
| **PCA** | Continuer à travailler pendant l'incident |
| **PRA** | Redémarrer après l'incident |

**Ce n'est pas une sauvegarde :** RAID · instantané sur le même stockage · réplication · synchronisation.

## Types

| Type | Copie | Restauration |
|---|---|---|
| Complète | Tout | 1 jeu |
| Différentielle | Depuis la dernière complète | Complète + dernière différentielle |
| Incrémentielle | Depuis la dernière sauvegarde | Complète + toutes les incrémentielles |

## 3-2-1 (et 3-2-1-1-0)

**3** copies · **2** supports · **1** hors site · **1** hors ligne ou immuable · **0** erreur (restauration testée).

## Commandes restic

| But | Commande |
|---|---|
| Créer le dépôt | `restic init --repo ~/depot` |
| Sauvegarder | `restic -r ~/depot backup ~/donnees` |
| Lister | `restic -r ~/depot snapshots` |
| Restaurer | `restic -r ~/depot restore latest --target ~/restauration` |
| Vérifier | `restic -r ~/depot check` |
| Rétention (simulation) | `restic -r ~/depot forget --keep-daily 7 --keep-weekly 4 --dry-run` |

## Chiffrer un support (LUKS)

```text
sudo cryptsetup luksFormat support.img
sudo cryptsetup open support.img coffre
sudo mkfs.ext4 /dev/mapper/coffre
sudo mount /dev/mapper/coffre /mnt/coffre
sudo umount /mnt/coffre && sudo cryptsetup close coffre
```

> [!WARNING]
> Une sauvegarde **jamais restaurée** n'est qu'une hypothèse. Clé de chiffrement perdue = données perdues : conserve-la **à part**.
