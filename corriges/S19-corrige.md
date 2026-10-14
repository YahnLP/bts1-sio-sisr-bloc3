# Corrigé S19 – Épreuve blanche E7 (Clinique du Val-Vert)

> Corrigé **à ne pas diffuser** avant la fin de l'année. Barème indicatif à comparer avec la grille nationale.

## Dossier A (20 pts)

**A1 (3).** Dossier patient (antécédents, diagnostics, ordonnances, numéro de sécurité sociale), imagerie, arrêts maladie du personnel (santé), éventuellement motif de consultation du rendez-vous en ligne. **Données de santé** = données sensibles (article 9) : interdites sauf exception, exigent des mesures renforcées, hébergement par un hébergeur de données de santé certifié si externalisé, **AIPD** fréquente. (1 pt identification, 2 pts justification.)

**A2 (4).** Oui : **violation de confidentialité** (perte d'un support non chiffré) ; 410 patients ; nom, prénom, date de naissance, **pathologie** (donnée de santé) ; gravité **élevée** : données sensibles, support en clair, perte hors des locaux, risque d'accès par un tiers. (1 + 1 + 2.)

**A3 (4).** Documenter dans le registre des violations ; notifier la CNIL **sous 72 h** après avoir eu connaissance si risque ; informer les personnes si risque **élevé**. Point de départ : la clinique a eu connaissance le **14 mars** (appel du médecin) → échéance **17 mars** à la même heure ; la date du 15 mars (information du directeur) n'est pas le point de départ. Incertitude : le médecin libéral peut être lui-même responsable de traitement pour son fichier ; qui notifie ? Dans le doute, se coordonner et notifier. (2 + 1 + 1.)

**A4 (4).** Exemples : conservation **sans limite** (définir des durées) ; **aucun registre** à jour (tenir le registre) ; accès à l'imagerie pour tous les médecins (moindre privilège) ; **tableur RH** accessible à tous les cadres (restreindre) ; vidéosurveillance sans information (affichage) ; **rendez-vous en ligne** sans contrat retrouvé (contrat de sous-traitance, article 28) ; DPO à 20 % (moyens). (1 point par manquement avec mesure.)

**A5 (5).** Oui : au moins deux critères : données sensibles (santé), grande échelle, personnes vulnérables (patients), usage innovant (téléconsultation), éventuellement surveillance. Méthode : décrire le traitement ; nécessité et proportionnalité (base légale, droits, sous-traitance) ; risques (accès illégitime, modification non désirée, disparition) cotés vraisemblance × gravité avec mesures ; validation (plan d'action, avis du DPO, consultation de la CNIL si risque résiduel élevé). (2 + 3.)

## Dossier B (15 pts)

**B1 (4).** 1 : **typosquatting** et faux site (escroquerie, usurpation d'identité numérique 226-4-1, éventuellement collecte frauduleuse) ; 2 : **hameçonnage** (usurpation d'identité de la direction) pour obtenir données personnelles et bancaires ; 3 : absence de **SPF/DKIM/DMARC** = vulnérabilité qui permet l'usurpation d'expéditeur. (1 point par menace + 1 pour les infractions.)

**B2 (4).** Publier des enregistrements **SPF** (serveurs autorisés), signer avec **DKIM**, politique **DMARC** (rejet/quarantaine + rapports) ; verrou et MFA sur le compte du registrar ; enregistrer des variantes du domaine ; surveillance des domaines proches. (2 + 2.)

**B3 (3).** Risque : publication au nom de la clinique, prise de contrôle par un tiers, perte de contrôle de l'image. Actions : retrouver le propriétaire du compte, utiliser la procédure de récupération de la plateforme avec justificatifs, désigner un responsable, activer le MFA, tenir un inventaire des comptes officiels. (1.5 + 1.5.)

**B4 (4).** Captures datées, URL, relevé whois/DNS, copies du courriel avec en-têtes ; empreintes SHA-256 des pièces ; constat de commissaire de justice pour un litige sérieux ; horodatage ; chaîne de possession. Signalements : bureau d'enregistrement et hébergeur du faux site, plateforme de signalement des escroqueries (Thésée), Pharos si contenu illicite, plainte, Cybermalveillance.gouv.fr. (2 + 2.)

## Dossier C (20 pts)

**C1 (4).** Comptes génériques partagés (pas de traçabilité) ; postes partagés avec session ouverte (accès au DPI par n'importe qui) ; mots de passe de 8 caractères ; clés USB libres ; matériel personnel des médecins sur le Wi-Fi ; mises à jour irrégulières ; réseau plat ; VPN sans MFA. (0,5 par risque pertinent, max 4.)

**C2 (5).** Comptes **nominatifs** (traçabilité) ; **authentification par badge** ou carte sur les postes partagés (ouverture rapide, verrouillage automatique à l'éloignement) ; MFA pour accès distant et comptes privilégiés ; mots de passe longs (phrases de passe) sans changement périodique forcé mais sur suspicion ; **procédure de bris de glace** pour l'urgence, tracée ; revue des comptes. Compromis : les soins ne doivent pas être ralentis ; badge plutôt que mot de passe long à chaque ouverture. (2 + 2 + 1.)

**C3 (4).** Solution 1 : **bloquer** les clés non autorisées par stratégie de groupe et fournir des clés **chiffrées** gérées ; solution 2 : supprimer le besoin (partage sécurisé, messagerie santé sécurisée, échange via le DPI). Comparaison : coût, usage, risque résiduel. (1 + 1 + 2.)

**C4 (4).** Risques : poste non maîtrisé (logiciels malveillants, absence de mises à jour), fuite de données, propagation vers le réseau de la clinique. Solutions : Wi-Fi **isolé** (VLAN) avec accès limité aux seuls services nécessaires ; accès par **bureau virtuel** ou application web avec MFA ; charte BYOD ; contrôle de conformité du poste. (1 + 3.)

**C5 (3).** Exemples : verrouiller la session en quittant le poste ; ne jamais partager son badge ou mot de passe ; ne pas utiliser de clé USB personnelle ; signaler sans attendre un message suspect ou une perte de matériel. (0,75 par règle.)

## Dossier D (25 pts)

**D1 (4).** Force brute VPN (3 avril) → accès avec le compte `astreinte` (4 avril 02 h 55, mot de passe faible, pas de MFA) → exploration des serveurs, **exfiltration** de 4,2 Go (4 avril 03 h 10-03 h 40) → chiffrement (6 avril 08 h) du serveur de fichiers et du NAS. Vecteur : **VPN sans MFA** et compte d'astreinte faible. (2 + 2.)

**D2 (4).** Pas de MFA ; mots de passe faibles ; comptes génériques ; réseau plat (le poste VPN atteint imagerie et fichiers) ; **NAS dans la même salle**, accessible en écriture ; bande dans la salle serveurs ; sauvegarde jamais testée récemment ; journaux conservés 7 jours seulement et non supervisés (exfiltration non détectée) ; mises à jour irrégulières. (0,5 par élément pertinent, max 4.)

**D3 (6).** Ordre : **isoler** les serveurs touchés et couper l'accès VPN ; déclarer la **cellule de crise** (direction, DPO, informatique, soins) ; activer les **procédures dégradées** de soins (DPI utilisable, imagerie indisponible → procédures papier, communication aux soignants) ; **protéger** la bande intacte (la sortir de la salle, la mettre hors réseau) ; collecter et préserver les **preuves** (journaux du pare-feu et du VPN, copie des machines) ; déposer **plainte**, prévenir l'assureur ; informer le **DPO** et la direction pour la violation ; prévenir les autorités sanitaires si exigé par le cadre applicable ; éradiquer (changer les mots de passe, fermer l'accès) ; restaurer depuis une sauvegarde saine ; communiquer aux patients et personnels. Rôles : directeur (décision), responsable informatique (pilote), DPO (violation), directrice des soins (continuité). (3 pour l'ordre et les actions, 1 rôles, 2 destinataires.)

**D4 (4).** Oui : l'**exfiltration** de 4,2 Go change la qualification : violation de **confidentialité** en plus de la **disponibilité**. Obligations : documenter, **notifier la CNIL sous 72 h** (risque élevé : données de santé) à compter du constat (6 avril 08 h, ou dès la découverte de l'exfiltration), **informer les patients** concernés, coordonner avec l'hébergeur/éditeur, plainte. (2 + 2.)

**D5 (4).** Exemples : DPI : RPO de **quelques minutes à 1 heure** (réplication ou sauvegarde fréquente), RTO de **quelques heures** (continuité des soins 24 h/24) ; imagerie : RPO de 24 h, RTO de quelques heures à 24 h avec mode dégradé. Stratégie : **3-2-1-1-0** : sauvegarde locale rapide, copie **hors site** et copie **hors ligne/immuable**, sauvegardes **chiffrées**, test de restauration mensuel, PRA écrit ; estimation de budget (par exemple appliance ou stockage immuable 30 000 à 50 000 €, hébergement hors site, bandes en coffre externe, tests). (2 + 2.)

**D6 (3).** 1) **MFA** sur le VPN et mots de passe forts ; 2) **sauvegarde hors ligne/immuable** ; 3) **segmentation** (VLAN, filtrage entre zones) ; 4) **journaux centralisés** avec alertes (échecs en rafale, volumes sortants). (0,75 chacune.)

## Dossier E (20 pts)

**E1 (6).** Zones au centre : postes, secrétariat, imprimantes, **Wi-Fi invités** isolé, **téléconsultation** (DMZ), équipements biomédicaux dans un VLAN dédié ; pare-feu avec **refus par défaut** ; liaison au siège par **VPN site à site** (IPsec) vers le pare-feu de la clinique ; accès au DPI par flux autorisés uniquement (ports précis, depuis les postes) ; administration séparée. Schéma et matrice de flux valorisés. (3 schéma, 3 flux et dispositifs.)

**E2 (4).** Site à site : permanent, transparent pour les utilisateurs, géré par les pare-feu, adapté à une liaison fixe entre deux sites ; nomade : par utilisateur, à la demande, adapté aux télétravailleurs. Recommandation : **site à site** pour le centre (IPsec, clés/certificats, MFA non applicable), complété par un VPN nomade avec **MFA** pour l'astreinte. (2 + 2.)

**E3 (4).** Un certificat lie le nom de domaine à la clé publique du serveur, signé par une AC reconnue des navigateurs : **identité**, **chiffrement TLS**. Obtention : certificat d'une AC publique (par exemple par ACME) pour un service exposé ; **renouvellement automatisé**, surveillance des dates d'expiration (`-checkend`), inventaire. (2 + 2.)

**E4 (3).** Journaux : authentification (VPN, AD), pare-feu, serveurs critiques (DPI, imagerie), événements Windows 4625, 4720, 4732, 1102. Alertes : rafale d'échecs de connexion, connexion VPN hors horaires, volume sortant anormal, création de compte. Durée : à justifier (un an en pratique pour les journaux de sécurité, avec minimisation des données personnelles, S08). (1.5 + 1.5.)

**E5 (3).** Désinstaller les services inutiles, SSH/RDP restreints et MFA, pare-feu local refus par défaut, mises à jour de sécurité, droits minimaux, journalisation, chiffrement des disques ; vérification régulière par **audit** (Lynis, scan de vulnérabilités) et suivi des écarts. (2 + 1.)

## Lecture du score

| Score | Lecture |
|---|---|
| ≥ 70 | Bonne maîtrise : consolider les dossiers les plus faibles |
| 50 à 69 | Maîtrise partielle : reprendre les séances indiquées dans la grille |
| < 50 | À reprendre sérieusement : séances de rattrapage, refaire les TP |
