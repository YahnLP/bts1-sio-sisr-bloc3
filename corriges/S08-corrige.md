# Corrigé S08

## Partie A

1. Pour **vérifier** l'effet de la règle (trois lignes attendues) et éviter une suppression massive par ​erreur (seuil mal écrit, mauvaise table).
2. Parce que la trace est elle-même une donnée : y recopier des noms **recréerait** la donnée que l'on vient de supprimer. On ne trace que la date et le nombre.
3. Dans les **sauvegardes** (jusqu'à expiration de leur rétention), les exports, les copies de travail, les fichiers temporaires, les courriels.
4. Le seuil `date('now','-3 years')` devient `date('now','-2 years')`, dans le `COUNT` et dans le `DELETE`.
5. Supprimés : `acces-1.log` et `acces-2.log` (400 jours). Restent : `acces-3.log` (200 ​jours) et `acces-4.log` (récent).
6. Pour **voir** ce qui sera supprimé avant de le faire : un `-delete` mal placé ou un motif trop large détruit des fichiers utiles.
7. Oui : une adresse IP est une donnée personnelle. On vise une durée **limitée et justifiée** (un an pour les journaux de connexion des hébergeurs, à confirmer ​selon le cas).
8. `monthly` + `rotate 12` : on garde **12 fichiers** mensuels, soit **environ un an** de journaux ; au 13ᵉ le plus ancien est supprimé.

## Partie B

9. L'attaque retrouve `blanc@example.org` et `faure@example.net`, parce que l'espace des adresses plausibles est petit : on calcule les empreintes et on compare.
10. Sans sel, l'attaquant ne peut pas reproduire l'empreinte : le calcul dépend d'un secret.
11. Non : c'est de la **pseudonymisation**. L'entreprise, qui détient le sel et le fichier de départ, peut ré-identifier ; la donnée ​reste personnelle.
12. Fournir des **statistiques agrégées** (par tranche, par commune) sans identifiant individuel, ou un jeu de données dont les identifiants sont de simples numéros sans table de correspondance chez le prestataire.

## Partie C

1. Atteinte à la **confidentialité** (accès non autorisé, extraction), par injection SQL ; la perte d'intégrité n'est pas démontrée.
2. Le ​délai part quand l'entreprise **en a eu connaissance** : au plus tôt lundi 10 h 15 (constat de l'administrateur). Échéance : **jeudi 10 h 15** environ. En cas de doute, on retient l'heure la plus tôt.
3. Nature : identité, courriel, adresse, naissance et **hachage MD5 sans sel** des mots de passe (très facile à ​casser, voir S03) → réutilisation sur d'autres services ; volume : **12 000** personnes ; facilité d'exploitation : données **en clair**, entre les mains d'un tiers. Risque **élevé** (hameçonnage ciblé, usurpation, prise de comptes).
4. **Oui** pour la CNIL (risque). **Oui** pour les personnes (risque élevé : données exploitables, mots de passe faibles) : les inviter à changer leur mot de passe partout où il est ​réutilisé et à se méfier des messages frauduleux.
5. Exemple : « Le [date], MédiaGroup a constaté l'extraction de la table des abonnés (environ 12 000 personnes : nom, prénom, courriel, adresse, date de naissance, mot de passe haché en MD5). La cause est une ​injection SQL présente depuis [date]. Le compte exploité a été désactivé à 10 h 40. Conséquences probables : hameçonnage, usurpation, compromission de comptes. Mesures : correction de la faille, réinitialisation des mots de ​passe, information des abonnés, passage à un hachage salé adapté. Contact : [DPO]. »
6. Faits (date, nature), personnes et données concernées, conséquences, mesures prises, ​décision de notification et de communication, avec ses **justifications**.
7. Requêtes paramétrées et validation des entrées ; compte applicatif en **moindres privilèges** (lecture seule, pas d'export massif) ; **hachage salé** de type `bcrypt`/`argon2` ; **pare-feu applicatif** ; **alertes** sur exportations anormales ; **chiffrement** des champs sensibles ; revue de code et **tests** avant mise en production.
8. Contenir (compte désactivé, accès coupé), **préserver les preuves** (copie des ​journaux, horodatage), identifier la cause et le périmètre, alerter le DPO et la direction, ne pas supprimer les traces, prévoir la restauration depuis la sauvegarde saine.
