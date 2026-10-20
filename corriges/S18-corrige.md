# Corrigé S18 (Transports Lambert)

## Fiche de repérage (éléments clés)

- Entreprise : 65 salariés, 2 sites, **1 technicien**, budget 60 000 € + 20 000 € ​supplémentaires.
- Failles : réseau plat ; Wi-Fi à clé commune partagée avec les chauffeurs ; **RDP exposé sur Internet** ; mot de passe de 8 caractères sans MFA, `Lambert2024` (prévisible) ; compte partagé de l'atelier ; **NAS accessible en écriture** en permanence ; sauvegarde **jamais testée** ; journaux ni centralisés ni consultés ; Windows Server 2016 (cycle de vie à ​surveiller) ; tablettes sans gestion ; fichier clients Excel ouvert à tous ; candidatures conservées sans durée.
- Cadre : RGPD (géolocalisation des chauffeurs, santé, paie), sous-traitance (éditeur de paie), violation de données (72 h), preuve, plainte.

## Question 1

Rançongiciel après **intrusion par RDP exposé** (force brute puis accès avec un mot de passe ​faible) : atteinte à la **disponibilité** (fichiers et sauvegarde chiffrés) et, selon la possibilité d'exfiltration, à la **confidentialité** ; vecteur : RDP + mot de passe prévisible. Preuves à conserver : journaux du pare-feu (tentatives, connexion de dimanche 23 h 10), journaux de connexion Windows (événements 4624/4625), note de rançon, échantillons de fichiers chiffrés, état des machines (copies), main ​courante horodatée ; empreintes des pièces.

## Question 2

Ne pas payer d'emblée : aucune garantie de déchiffrement ou de non-divulgation ; finance les attaquants et peut inciter à de nouvelles attaques ; les autorités le déconseillent. Plan 48 h : (1) **isoler** serveur et postes touchés, fermer la redirection RDP et ​changer les accès ; (2) prévenir la direction, l'assureur, le DPO/responsable des données ; (3) **collecter les preuves**, déposer plainte ; (4) évaluer l'exfiltration, déclencher la procédure de violation de données ; (5) chercher une sauvegarde saine (la seule copie, le NAS, est chiffrée : vérifier d'autres copies, le prestataire, les postes) ; (6) **éradiquer** (réinitialiser les mots de passe, reconstruire) ​avant de restaurer ; (7) communiquer aux clients et salariés.

## Question 3

a. Oui : toute entreprise qui traite des données personnelles est concernée. Problèmes : **géolocalisation** continue sans information des chauffeurs (finalité, information, durée) ; **données de santé** (aptitude) : traitement strictement ​encadré ; **fichier clients** partagé à tous (minimisation, droits) ; **paie** sans contrat de sous-traitance (article 28) ; **candidatures** sans durée de conservation ; pas de registre.
b. Oui, si des données personnelles ont été chiffrées ou copiées : violation de **disponibilité** au moins (et de confidentialité si exfiltration). Obligations : documenter dans le registre des violations ; notifier la CNIL **sous 72 h** si risque ; informer les ​personnes si risque **élevé** ; prévenir les clients dont l'entreprise est sous-traitante.
c. Répondre avec exactitude, dans la mesure où les faits sont établis : incident en cours d'analyse, pas encore de preuve d'exfiltration (ou le contraire), mesures prises ; ne pas minimiser ni dramatiser ; engager à informer dès que l'analyse est terminée.

## Question 4 (exemple de plan)

| Priorité | ​Mesure | Risque | Justification | Limite | Coût indicatif (à valider) |
|---|---|---|---|---|---|
| 1 | Supprimer l'exposition RDP, accès par **VPN avec MFA** | Force brute / prise de compte | Supprime le vecteur de l'incident | Gestion des comptes VPN | quelques milliers d'euros |
| 2 | **Mots de passe** : 12 ​caractères mini, interdiction des mots de passe faibles, comptes nominatifs, MFA pour les administrateurs | Mot de passe prévisible, compte partagé | S03/S04 | Accompagnement des utilisateurs | faible |
| 3 | **Sauvegarde 3-2-1-1-0** : copie hors ligne/immuable, test de restauration | Perte totale | S05, PRA | Stockage externe | ​environ 3 000 à 6 000 € |
| 4 | **Segmentation** : VLAN postes / serveurs / Wi-Fi chauffeurs / Wi-Fi invités ; pare-feu réel | Propagation | S14 | Un pare-feu à choisir et administrer | environ 3 000 à 5 000 € |
| 5 | **Supervision** : journaux centralisés, alertes sur échecs RDP/VPN | Détection tardive | S15 | Temps de lecture | faible à moyen |
| 6 | Gestion des **tablettes** et mises à jour | Compromission ​mobile | S02 | Licences | moyen |

(Les montants sont des ordres de grandeur d'exercice.)

## Question 5

Comparaison : **application web en HTTPS avec authentification forte** (limite l'accès aux seules données de temps de conduite, pas de tunnel vers le réseau interne) ; **VPN** sur téléphone personnel (donne un accès réseau : trop large pour un appareil non ​maîtrisé). Recommander l'application web, publiée en DMZ ou en service externalisé, avec TLS (S11-S12), MFA et droits minimaux (S04). Cadre juridique : RGPD (information des chauffeurs, finalité, données de géolocalisation), charte pour l'usage de téléphones personnels (BYOD), respect de la vie privée de l'employé.
