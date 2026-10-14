# Aide-mémoire – Droits d'accès et privilèges

*BTS SIO SISR 1re année – Bloc 3 – S04*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Principes

| Principe | Idée |
|---|---|
| Moindre privilège | Le strict nécessaire, pour la durée nécessaire |
| Séparation des tâches | Deux personnes pour une action sensible |
| Besoin d'en connaître | N'accéder qu'à ce qui sert sa mission |
| Droits temporaires | Limités, validés, tracés, retirés |

## Modèles

| Modèle | Qui décide ? |
|---|---|
| DAC | Le propriétaire de la ressource |
| MAC | Une politique centrale |
| RBAC | L'administrateur, par rôles (groupes) |

**AGDLP (Windows)** : Comptes → groupes Globaux → groupes de Domaine Local → Permissions.

## Vie d'un compte

Arrivée (demande validée, compte nominatif) · changement de poste (retrait puis ajout) · accès temporaire (durée limitée) · **départ : désactivation le jour même**.

## Linux

| But | Commande |
|---|---|
| Créer un groupe | `sudo groupadd g_rh` |
| Utilisateur dans un groupe | `sudo useradd -m -s /bin/bash -G g_rh julie` |
| Groupe propriétaire | `sudo chgrp g_rh /srv/data/rh` |
| Droits + setgid | `sudo chmod 2770 /srv/data/rh` |
| ACL | `sudo setfacl -m g:g_compta:rx dossier` · `getfacl dossier` |
| ACL par défaut | `sudo setfacl -d -m g:g_compta:rx dossier` |
| Groupes d'un utilisateur | `id marc` |
| Tester comme un utilisateur | `sudo -u marc ls /srv/data/rh` |
| Désactiver un compte | `sudo usermod -L -e 1 marc` |

## Windows

| But | Commande |
|---|---|
| Voir l'ACL | `icacls dossier` · `Get-Acl dossier` |
| Donner un droit | `icacls dossier /grant "G_RH:(OI)(CI)M"` |
| Retirer l'héritage | `icacls dossier /inheritance:r` |
| Retirer « Tout le monde » | `icacls dossier /remove "*S-1-1-0"` |
| Groupe local | `net localgroup G_RH /add` |

Droits : `F` contrôle total · `M` modification · `RX` lecture et exécution · `R` lecture.
