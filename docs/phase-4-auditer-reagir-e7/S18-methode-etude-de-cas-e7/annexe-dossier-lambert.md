# Annexe – Dossier documentaire Transports Lambert (fictif)

*Entreprise, personnes, chiffres et événements **inventés**.*

## Document 1 – Présentation

**Transports Lambert** est une entreprise de transport routier de marchandises de **65 salariés** : 40 chauffeurs, 15 personnes administratives et d'exploitation, 5 mécaniciens, 5 dirigeants et cadres. Elle compte un **siège** (bureaux et atelier) et une **plateforme logistique** à 30 km, reliés par une liaison Internet professionnelle chacun.

| Élément | Détail |
|---|---|
| Direction | M. Lambert (gérant) ; Mme Rey (responsable d'exploitation) |
| Informatique | **Un technicien** à temps plein (Amine) ; un prestataire pour les licences |
| Budget informatique annuel | 60 000 € (dont 25 000 € de licences et connexions) |
| Clients | 120 entreprises ; donnent leurs adresses de livraison et contacts |

## Document 2 – Système d'information

| Élément | Détail |
|---|---|
| Serveurs | 1 serveur Windows Server 2016 (Active Directory, fichiers) ; 1 serveur d'application « TransLog » (gestion des tournées, Linux) ; 1 NAS de sauvegarde |
| Postes | 25 PC Windows 10 ; 40 tablettes Android dans les camions (application TransLog) |
| Réseau | Un seul réseau plat au siège ; pas de VLAN ; un pare-feu opérateur basique ; Wi-Fi unique « Lambert » avec une clé commune partagée avec les chauffeurs |
| Accès distant | Les dirigeants se connectent à TransLog par une redirection de port RDP (port 3389 ouvert sur Internet) |
| Sauvegarde | Sauvegarde nocturne du serveur de fichiers vers le NAS (branché en permanence, accessible en écriture) ; jamais testée |
| Mots de passe | Politique : 8 caractères, pas de changement imposé ; mot de passe partagé pour le compte de l'atelier |
| Journaux | Non centralisés ; non consultés |

## Document 3 – Les données

| Traitement | Données | Observations |
|---|---|---|
| Gestion des chauffeurs | Identité, numéro de permis, **visite médicale** (aptitude), temps de conduite (chronotachygraphe), géolocalisation du véhicule en continu | Géolocalisation consultée aussi par l'exploitation ; aucune information donnée aux chauffeurs |
| Clients | Contacts, adresses de livraison | Fichier Excel partagé en lecture pour tous les postes |
| Paie | Identité, salaire, arrêts | Logiciel en ligne ; pas de contrat connu avec l'éditeur |
| Candidatures | CV reçus par courriel | Gardés dans une boîte partagée, sans limite de durée |

## Document 4 – L'incident

Mardi 6 h 30 : Amine constate que le serveur de fichiers est lent et que des dossiers contiennent des fichiers `.crypt`. Une note de rançon demande 8 000 € en cryptomonnaie. Les journaux du pare-feu opérateur montrent des tentatives de connexion RDP répétées depuis une même adresse étrangère depuis trois semaines, **suivies d'une connexion réussie** dimanche à 23 h 10 avec le compte d'une dirigeante (mot de passe : `Lambert2024`). Le NAS est également chiffré. M. Lambert veut payer « pour repartir vite ».

## Document 5 – Les besoins exprimés par la direction

1. Éviter qu'un tel incident se reproduise, avec un budget supplémentaire de **20 000 €** la première année.
2. Permettre aux chauffeurs de consulter leurs temps de conduite depuis leur téléphone personnel.
3. Respecter la loi : M. Lambert a entendu parler du RGPD mais « ne sait pas si cela concerne l'entreprise ».
4. Pouvoir répondre à un client qui veut savoir si ses données ont été volées.
