# Cours – Sauvegarde, supports amovibles et restauration

*BTS SIO SISR 1re année – Bloc 3 – S05 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S01 (rançongiciel), S04 (droits) ; sauvegarde vue côté exploitation au bloc 2 (S16).
> - **Matériel :** VM Debian de laboratoire (paquets `restic` et `cryptsetup`) ; calculatrice ou tableur

## À la fin de ce cours tu sauras

- [ ] **Expliquer** les objectifs de reprise (RPO, RTO) et les plans associés (PCA, PRA) ;
- [ ] **Distinguer** sauvegarde complète, différentielle et incrémentielle, et **choisir** selon le besoin ;
- [ ] **Appliquer** la règle 3-2-1 et **justifier** qu'une copie hors ligne ou immuable protège d'un rançongiciel ;
- [ ] **Distinguer** une sauvegarde d'un RAID, d'un instantané ou d'une réplication ;
- [ ] **Sauvegarder, restaurer et vérifier** des données avec un outil chiffré et dédupliqué ;
- [ ] **Chiffrer** un support amovible et **rédiger** une règle d'usage des supports.

## I. Pourquoi sauvegarder ?

La sauvegarde est la **dernière ligne de défense** : quand la prévention a échoué, c'est elle qui permet de redémarrer. Elle protège la **disponibilité** et l'**intégrité** des données (S01).

| Cause de perte | Exemple |
|---|---|
| **Panne matérielle** | Disque en panne, serveur hors service |
| **Erreur humaine** | Suppression d'un dossier, mauvaise commande sur le mauvais serveur |
| **Malveillance** | Rançongiciel, employé en colère, intrusion qui détruit |
| **Sinistre** | Incendie, inondation, vol |
| **Défaut logiciel** | Mise à jour qui corrompt une base de données |

## II. Les objectifs de reprise

Deux questions guident toute stratégie de sauvegarde :

| Sigle | Question | Conséquence |
|---|---|---|
| **RPO** (*Recovery Point Objective*) | Quelle durée de données peut-on **perdre** au maximum ? | Il fixe la **fréquence** des sauvegardes |
| **RTO** (*Recovery Time Objective*) | Quelle durée d'**interruption** peut-on supporter au maximum ? | Il fixe la **vitesse de restauration** exigée et donc les moyens |

```mermaid
flowchart LR
    A["Dernière sauvegarde<br/>valide"] -->|"RPO : données perdues"| B["Incident"]
    B -->|"RTO : service indisponible"| C["Service rétabli"]
```

Ces valeurs viennent du **métier**, pas de l'informatique : on demande aux responsables ce que coûte une heure d'arrêt, et ce qu'ils peuvent se permettre de ressaisir.

Deux plans formalisent la réponse :

- **PCA** (plan de continuité d'activité) : comment **continuer** à travailler pendant l'incident ;
- **PRA** (plan de reprise d'activité) : comment **redémarrer** et restaurer après l'incident, dans quel ordre, par qui.

### Ce qui n'est pas une sauvegarde

| Mécanisme | Pourquoi ce n'en est pas une |
|---|---|
| **RAID** | Il protège d'une **panne de disque**, pas d'une suppression ni d'un rançongiciel : l'erreur est copiée sur tous les disques |
| **Instantané** (*snapshot*) | Il est conservé **sur le même stockage** : si le stockage est détruit ou chiffré, il disparaît avec lui |
| **Réplication** | Elle recopie **aussi** les suppressions et le chiffrement vers l'autre site |
| **Synchronisation** (type nuage) | Un fichier chiffré se synchronise comme un autre ; seule la **conservation de versions** aide |

## III. Les types de sauvegarde

| Type | Ce qu'elle copie | Espace | Temps de sauvegarde | Restauration |
|---|---|---|---|---|
| **Complète** | **Tout** | Important | Long | **Simple** : un seul jeu |
| **Différentielle** | Ce qui a changé **depuis la dernière complète** | Moyen, croît chaque jour | Moyen | La complète + la **dernière** différentielle |
| **Incrémentielle** | Ce qui a changé **depuis la dernière sauvegarde** (quelle qu'elle soit) | Faible | Court | La complète + **toutes** les incrémentielles (une perdue = chaîne rompue) |

Un schéma courant : une **complète par semaine** et des **incrémentielles** quotidiennes. Les outils modernes (par exemple restic, utilisé en TP) font de la **déduplication** : chaque morceau de données n'est stocké qu'une fois, ce qui rend chaque sauvegarde « complète » à la restauration mais peu coûteuse en espace.

**Je vérifie.** Une incrémentielle du mardi est illisible (support défectueux). Peut-on restaurer le jeudi ? Et avec une stratégie différentielle ?

<details markdown="1">
<summary>Voir la réponse</summary>

Avec des **incrémentielles** : non, la chaîne est rompue entre le lundi et le mercredi, les données du mardi manquent ; on restaure au mieux jusqu'au lundi. Avec des **différentielles** : oui, le jeudi se restaure avec la complète et la différentielle du jeudi seule, qui contient tout ce qui a changé depuis la complète.

</details>

## IV. La règle 3-2-1 et ses prolongements

> **3 copies** des données (l'original et deux sauvegardes), sur **2 supports différents**, dont **1 copie hors site**.

| Élément | Risque couvert |
|---|---|
| 3 copies | Une copie corrompue ou perdue ne suffit pas à tout perdre |
| 2 supports | Une même panne technologique n'emporte pas tout |
| 1 hors site | Incendie, vol, inondation du site principal |

Face aux rançongiciels, qui cherchent et détruisent les sauvegardes accessibles, on étend la règle (variante dite **3-2-1-1-0**) :

- **1 copie hors ligne ou immuable** : déconnectée, ou stockée de façon à ne pouvoir être ni modifiée ni supprimée pendant une durée fixée ;
- **0 erreur** : on **vérifie** les sauvegardes par une restauration d'essai.

**Cas réel : GitLab (31 janvier 2017).** Lors d'une opération de maintenance, un administrateur a supprimé par erreur le répertoire de données de la mauvaise base. Au moment de restaurer, plusieurs mécanismes de sauvegarde se sont révélés inutilisables ou périmés ; il a fallu restaurer depuis un instantané vieux d'environ six heures. L'entreprise a publié une analyse détaillée de l'incident. **Leçon : une sauvegarde qui n'a jamais été restaurée n'est qu'une hypothèse.**

## V. La politique de sauvegarde

Une politique écrite précise :

| Point | Question |
|---|---|
| **Périmètre** | Quelles données, quels serveurs, quels postes ? |
| **Fréquence** | Compatible avec le RPO ? |
| **Rétention** | Combien de temps garde-t-on chaque sauvegarde ? Un schéma courant garde 7 quotidiennes, 4 hebdomadaires, 12 mensuelles (principe « grand-père, père, fils ») |
| **Stockage** | Où ? Séparé du réseau de production ? |
| **Chiffrement** | Les sauvegardes sont-elles chiffrées ? Où est la clé ? |
| **Accès** | Qui peut **supprimer** une sauvegarde ? Compte de service dédié, MFA, journalisation |
| **Restauration** | Qui restaure, avec quelle procédure, en combien de temps ? |
| **Tests** | À quelle fréquence prouve-t-on qu'on sait restaurer ? |

> [!WARNING]
> **Les sauvegardes sont aussi des données personnelles.** Elles contiennent les mêmes informations que les systèmes de production : elles doivent être **protégées** et leur **durée de conservation** doit être justifiée (voir S06 à S08). Un droit à l'effacement se traite aussi dans les sauvegardes, selon un délai documenté.

Le **chiffrement** protège la confidentialité d'une sauvegarde volée, mais **crée un risque** : si la clé est perdue, la sauvegarde est inutilisable. La clé est donc elle-même **sauvegardée à part**.

## VI. Les supports amovibles

Clé USB, disque externe, NAS portable : pratiques, mais ils **sortent du périmètre de protection**.

| Risque | Exemple | Mesure |
|---|---|---|
| **Perte ou vol** | Clé oubliée dans un train avec des données de clients | **Chiffrement** du support |
| **Vecteur de malware** | Clé trouvée sur un parking, branchée par curiosité | Analyse antivirus automatique, **interdiction** de brancher un support inconnu |
| **Fuite volontaire** | Copie de fichiers sur un disque personnel | Limiter l'écriture sur supports amovibles (GPO), journaliser |
| **Panne** | Clé qui lâche | Un support amovible n'est **jamais** l'unique copie |

Les outils de chiffrement courants : **BitLocker To Go** (Windows), **LUKS** (Linux), **VeraCrypt** (multiplateforme). La **règle d'usage** précise : quels supports sont autorisés, qui les fournit, comment on les chiffre et on les efface, ce qu'on fait en cas de perte (alerte immédiate, et **notification** si des données personnelles sont concernées, voir S08).

## À retenir

- **RPO** = perte de données acceptable ; **RTO** = interruption acceptable. Ils viennent du **métier**.
- **RAID, instantané, réplication, synchronisation** ne sont pas des sauvegardes.
- **3-2-1**, avec une copie **hors ligne ou immuable** et des **restaurations testées**.
- Une sauvegarde est une **donnée sensible** : accès restreint, chiffrement, clé conservée à part.
- Un support amovible se **chiffre**, ne contient **jamais** l'unique copie et suit une **règle d'usage**.
