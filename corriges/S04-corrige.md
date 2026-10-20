# Corrigé S04

## Matrice de droits InnoTech (une solution défendable)

| Groupe | Clients | Projets | RH | Compta | ​Direction | IT | Archives |
|---|---|---|---|---|---|---|---|
| `G_Commercial` | L+E+S | — | — | — | — | — | L |
| `G_Comptable` | L | — | L (données de paie seulement) | L+E+S | — | — | L |
| `G_DRH` | — | — | L+E+S | L (fiches de paie) | — | — | L |
| `G_Dev` | — | L+E+S | — | — | — | — | L |
| `G_Chef_Projet` | L+E | L+E+S | — | — | — | — | L |
| `G_Direction` | L | L | à discuter (voir question 2) | L | L+E+S | — | L |
| `G_Admin_IT` | — | — | — | — | — | A | — (sauvegarde par compte de service) |
| `G_Stagiaire` | — | L | — | — | — | — | — |

## Réponses de la partie A

1. Accès **temporaire**, demandé par écrit, validé par le responsable des données, en **lecture seule**, limité en durée, tracé (journal), retiré à l'échéance. Variante : ​fournir un **jeu de données anonymisé**.
2. Le besoin de « tout lire » n'est pas démontré pour les évaluations et dossiers individuels : proposer une lecture **agrégée** (indicateurs) plutôt que le dossier nominatif.
3. L'accès large au dossier RH par la direction, et la lecture des données de paie par la comptabilité : à limiter à ce qui est **nécessaire** (principe de minimisation, S06).

## Partie B : résultats attendus

| ​Utilisateur | Action | Résultat |
|---|---|---|
| sophie | Créer un fichier dans `clients` | Réussit |
| sophie | Lister `rh` | **Permission refusée** |
| marc | Lister `clients` | Réussit (ACL de lecture) |
| marc | Créer un fichier dans `clients` | **Permission refusée** (lecture seule) |
| julie | Lister `compta` | **Permission refusée** (la matrice demande une ​lecture des fiches de paie : ajouter `setfacl -m g:g_rh:rx /srv/data/compta` si besoin) |
| paul | Lister `direction` | Réussit |

Question 1 : le test de `julie` sur `compta` échoue alors que la matrice donne **L** au DRH : il faut une ACL.

## Partie C

1. **Non**, elle est toujours là : `/inheritance:r` retire seulement les droits **hérités** du dossier parent, alors que l'entrée « Tout le monde » avait été ajoutée **explicitement**. Il faut la ​retirer avec `icacls C:\Data\RH /remove "*S-1-1-0"` puis relire l'ACL. C'est volontairement un **piège** : on vérifie le résultat réel avec `icacls`, on ne se contente pas d'avoir tapé les commandes.
2. Les administrateurs sont conservés pour l'**exploitation** (sauvegarde, dépannage) ; `M` autorise lecture, écriture et suppression mais **pas** le changement des permissions.
3. Un groupe se gère en **un point** : l'arrivée ou le départ d'un ​salarié se traduit par un changement de groupe, sans retoucher le dossier.
