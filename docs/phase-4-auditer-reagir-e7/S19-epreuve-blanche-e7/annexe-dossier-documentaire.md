# Annexe – Dossier documentaire : Clinique du Val-Vert (fictif)

*Établissement, personnes, adresses et événements **inventés**. Document à lire avant de répondre aux questions.*

## Document 1 – Présentation de l'établissement

La **Clinique du Val-Vert** est un établissement de santé privé de **120 lits**. Elle emploie **180 salariés** et accueille environ **25 médecins libéraux** qui y exercent. Elle réalise des interventions chirurgicales, de la médecine, et des consultations externes. Un projet d'**extension** prévoit l'ouverture, dans 18 mois, d'un **centre de consultations** à 15 km, relié à la clinique.

| Élément | Détail |
|---|---|
| Direction | M. Brun, directeur ; Mme Salah, directrice des soins ; Dr Leroy, président de la commission médicale |
| Service informatique | **4 personnes** : 1 responsable (Mme Ito), 2 techniciens, 1 apprenti ; sous-traitance de l'infogérance des serveurs d'imagerie |
| Délégué à la protection des données | Mme Noël, à 20 % de son temps ; **aucun registre à jour** |
| Budget informatique | 450 000 € par an en fonctionnement ; 120 000 € disponibles pour les projets de sécurité de l'année |
| Contraintes | Continuité des soins 24 h sur 24 ; exigences réglementaires de santé |

## Document 2 – Système d'information

| Domaine | Description |
|---|---|
| Serveurs | 2 salles serveurs au sous-sol de la clinique : dossier patient informatisé (DPI) sur 2 serveurs (Windows Server 2016), serveur d'imagerie (PACS), annuaire Active Directory, serveur de fichiers, serveur de messagerie interne |
| Hébergement | Le DPI est hébergé **sur place** ; l'application de **prise de rendez-vous en ligne** est un service externe (éditeur « RdvSanté », fictif), qui reçoit les nom, prénom, téléphone, courriel et motif de consultation des patients |
| Postes | 320 postes Windows 10 (dont 60 postes partagés en soins, avec session ouverte en continu) ; 40 tablettes pour les infirmiers ; les médecins libéraux utilisent aussi leur **ordinateur personnel** sur le Wi-Fi de la clinique |
| Réseau | Un **réseau unique** (pas de VLAN) pour les postes, les serveurs, les imprimantes et le Wi-Fi des visiteurs ; un pare-feu de périmètre ; les équipements biomédicaux (scanner, automates) sont sur le même réseau ; connexion Internet unique |
| Accès distant | Un **VPN** SSL pour les médecins et l'astreinte ; authentification par identifiant et mot de passe seulement |
| Sauvegarde | Sauvegarde quotidienne des serveurs vers un NAS **dans la même salle serveurs** ; copie hebdomadaire sur bande, **stockée dans la même salle** ; dernière restauration testée il y a plus de deux ans |
| Comptes | 40 comptes « génériques » partagés (par service) pour les postes de soins ; mots de passe de 8 caractères, changés tous les 90 jours |
| Journaux | Journaux du pare-feu conservés 7 jours ; journaux des serveurs non centralisés ; pas de supervision de sécurité |
| Sécurité des postes | Antivirus géré centralement ; mises à jour Windows appliquées « quand le service informatique en a le temps » ; clés USB autorisées sans restriction |

## Document 3 – Les traitements de données

| Traitement | Données | Observations |
|---|---|---|
| Dossier patient | Identité, numéro de sécurité sociale, antécédents, diagnostics, ordonnances, résultats | Conservé « sans limite » dans le DPI |
| Imagerie | Images et comptes rendus | Accès par tous les médecins de la clinique |
| Prise de rendez-vous en ligne | Identité, contact, motif | Service externe ; contrat à retrouver |
| Personnel | Identité, paie, arrêts, évaluations | Service RH ; tableur sur le serveur de fichiers, accès à tous les cadres |
| Vidéosurveillance | Images des parkings et des accueils | Conservées 3 mois ; sans affichage d'information |

## Document 4 – Incident signalé le 12 mars

Un médecin libéral a **perdu une clé USB** dans un train. Elle contenait un tableau de **410 patients** (nom, prénom, date de naissance, pathologie, date de la dernière consultation). Elle **n'était pas chiffrée** ni protégée par un mot de passe. Le médecin a prévenu la clinique le 14 mars. Mme Ito a informé le directeur le 15 mars à 9 h.

## Document 5 – Alertes de l'équipe informatique

1. Une patiente indique qu'elle a pris rendez-vous sur un site `clinique-val-vert.example` alors que le site officiel est `cliniqueduvalvert.example`. Le faux site reproduit la page d'accueil et la page de rendez-vous, et demande un acompte de 30 € par carte bancaire.
2. Des courriels signés « Direction de la clinique » demandent aux patients de confirmer leur numéro de sécurité sociale et leur IBAN pour un « remboursement ».
3. La messagerie de la clinique n'a aucun enregistrement SPF/DKIM/DMARC sur le domaine officiel.
4. Le compte d'un réseau social au nom de la clinique, créé par un ancien stagiaire, n'a plus de responsable : le mot de passe est inconnu.

## Document 6 – Extrait des journaux du pare-feu et du VPN (semaine du 3 au 9 avril)

| Date | Événement |
|---|---|
| 3 avril, 02 h 14 à 02 h 51 | 1 350 échecs de connexion VPN, comptes tentés : `admin`, `medecin`, `leroy`, `astreinte`, `test` ; adresse source unique (hors France) |
| 4 avril, 02 h 55 | **Connexion VPN réussie** du compte `astreinte` depuis la même adresse |
| 4 avril, 03 h 10 à 03 h 40 | Connexions SMB depuis le poste `astreinte` vers le serveur d'imagerie et le serveur de fichiers ; 4,2 Go sortants vers l'adresse externe |
| 6 avril, 08 h | Le serveur de fichiers affiche des fichiers au suffixe `.vault` ; message de rançon dans chaque dossier |
| 6 avril, 08 h 15 | Le NAS de sauvegarde est également chiffré ; la bande de la semaine précédente est intacte mais stockée dans la salle serveurs |
| 6 avril, 09 h 00 | Le DPI reste utilisable, mais l'imagerie est inaccessible |

## Document 7 – Le projet de centre de consultations

Le centre de consultations (15 postes, 10 médecins, un secrétariat) devra accéder au dossier patient de la clinique, partager l'imagerie, et héberger un service de **téléconsultation**. La direction demande une architecture « sécurisée et simple à administrer » avec un budget de 120 000 € comprenant la liaison, le pare-feu, les postes et la sécurisation des accès.
