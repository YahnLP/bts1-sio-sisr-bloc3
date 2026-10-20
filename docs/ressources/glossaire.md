# Glossaire

Tous les mots techniques du bloc 3, expliqués simplement. Dans les pages du site, **passe la souris sur un sigle** (VLAN, DHCP, GPO…) : sa définition s'affiche.

> [!NOTE]
> Un terme suivi de la mention **notion technique** dépasse le socle de première année : tu peux le laisser de côté.

La colonne « Vu en » indique la séance où le mot apparaît pour la première fois dans le cours.

| Terme | Sigle | Anglais | Définition | Vu en |
|---|---|---|---|---|
| **Actif** |  | *asset* | Ce qu'il faut protéger : donnée, serveur, application, service. | S01 |
| **Advanced Encryption Standard** | AES | *advanced encryption standard* | Chiffrement symétrique par blocs de 128 bits, avec des clés de 128, 192 ou 256 bits. | S10 |
| **Agence nationale de la sécurité des systèmes d'information** | ANSSI |  | Autorité française de cybersécurité, qui publie guides, recommandations et alertes. | S01 |
| **Analyse d'impact relative à la protection des données** | AIPD | *data protection impact assessment (DPIA)* | Analyse des risques exigée avant un traitement susceptible d'engendrer un risque élevé. | S09 |
| **Anonymisation** |  | *anonymisation* | Rendre la ré-identification impossible : la donnée n'est plus personnelle. | S08 |
| **Audit de vulnérabilités** |  | *vulnerability assessment* | Recherche des failles d'un système, dans un cadre autorisé. | S16 |
| **Authentification** |  | *authentication* | Prouver que l'on est bien la personne que l'on prétend être. | S03 |
| **Authentification multifacteur** | MFA | *multi-factor authentication* | Authentification qui exige au moins deux facteurs de types différents. | S03 |
| **Authentification résistante à l'hameçonnage** | FIDO2 |  | Norme de clés de sécurité et de passkeys qui ne répondent qu'au site réel. | S03 |
| **Autorisation** |  | *authorization* | Décider de ce qu'une personne authentifiée a le droit de faire. | S03 |
| **Autorité de certification** | AC | *certificate authority (CA)* | Organisme qui émet et signe des certificats. | S11 |
| **Autorité nationale de la sécurité des systèmes d'information** | ANSSI |  | Agence française chargée de la cybersécurité de l'État et des opérateurs. | S09 |
| **Base légale** |  | *lawful basis* | Fondement juridique d'un traitement : consentement, contrat, obligation légale, intérêts vitaux, mission d'intérêt public, intérêt légitime. | S07 |
| **Bit setgid** |  | *setgid* | Sur un dossier Linux, fait hériter les nouveaux fichiers du groupe du dossier. | S04 |
| **Bourrage d'identifiants** |  | *credential stuffing* | Réessayer sur un service des identifiants volés sur un autre. | S03 |
| **Centre gouvernemental de veille, d'alerte et de réponse aux attaques** | CERT-FR | *computer emergency response team* | Équipe de l'ANSSI qui publie avis et alertes de sécurité. | S01 |
| **Certificat auto-signé** |  | *self-signed certificate* | Certificat signé par sa propre clé : non reconnu par défaut. | S12 |
| **Certificat X.509** |  | *X.509 certificate* | Document qui lie une identité à une clé publique, signé par une autorité de certification. | S11 |
| **Chaîne de confiance** |  | *chain of trust* | Suite de certificats qui remonte du serveur à une racine connue du système. | S11 |
| **Chaîne de possession** |  | *chain of custody* | Suivi de qui détient et manipule une preuve. | S17 |
| **Charte informatique** |  | *acceptable use policy* | Document signé par les utilisateurs qui fixe les règles d'usage du système d'information. | S01 |
| **Cheval de Troie** |  | *trojan* | Logiciel qui se présente comme utile pour se faire installer par l'utilisateur. | S02 |
| **Chiffrement asymétrique** |  | *asymmetric encryption* | Chiffrement à paire de clés : une publique, une privée. | S11 |
| **Chiffrement de disque de Windows** | BitLocker |  | Fonction de Windows qui chiffre un disque entier. | S02 |
| **Chiffrement de volume de Linux** | LUKS | *linux unified key setup* | Standard de chiffrement de disques et de volumes sous Linux. | S05 |
| **Chiffrement hybride** |  | *hybrid encryption* | On chiffre le message en symétrique et la clé de session en asymétrique. | S11 |
| **Chiffrement symétrique** |  | *symmetric encryption* | Chiffrement qui utilise la même clé pour chiffrer et déchiffrer. | S10 |
| **Clé privée** |  | *private key* | Clé secrète de son propriétaire : sert à déchiffrer et à signer. | S11 |
| **Clé publique** |  | *public key* | Clé que l'on peut diffuser : sert à chiffrer pour son propriétaire ou à vérifier sa signature. | S11 |
| **Code d'authentification de message à clé** | HMAC | *hash-based message authentication code* | Empreinte calculée avec une clé secrète : garantit intégrité et authenticité. | S10 |
| **Commission nationale de l'informatique et des libertés** | CNIL |  | Autorité française de protection des données personnelles. | S03 |
| **Commission nationale de l'informatique et des libertés** | CNIL |  | Autorité française de protection des données personnelles. | S06 |
| **Common Vulnerabilities and Exposures** | CVE | *CVE* | Identifiant unique d'une vulnérabilité connue (CVE-année-numéro). | S16 |
| **Common Vulnerability Scoring System** | CVSS | *CVSS* | Score de gravité technique d'une vulnérabilité, de 0 à 10. | S16 |
| **Confidentialité** |  | *confidentiality* | Seules les personnes autorisées peuvent lire l'information. | S01 |
| **Confidentialité persistante** |  | *forward secrecy* | Propriété qui protège les sessions passées même si une clé privée est volée plus tard. | S11 |
| **Consentement** |  | *consent* | Accord libre, spécifique, éclairé et univoque de la personne. | S07 |
| **Contrôle d'accès discrétionnaire** | DAC | *discretionary access control* | Le propriétaire d'une ressource décide qui y accède. | S04 |
| **Contrôle d'accès obligatoire** | MAC | *mandatory access control* | Une politique centrale fixe les accès, que l'utilisateur ne peut pas modifier. | S04 |
| **Contrôle d'accès par rôles** | RBAC | *role-based access control* | Les droits sont donnés à des rôles, auxquels on affecte des utilisateurs. | S04 |
| **Cookie** |  | *cookie* | Petit fichier déposé par un site dans le navigateur. | S07 |
| **Correctif** |  | *patch* | Mise à jour qui corrige une faille ou un défaut. | S02 |
| **Cryptographie** |  | *cryptography* | Science des secrets et de la preuve : chiffrement, hachage, signature. | S10 |
| **Cybersécurité** |  | *cybersecurity* | Ensemble des moyens qui protègent un système d'information et ses données. | S01 |
| **Déduplication** |  | *deduplication* | Technique qui ne stocke qu'une fois chaque morceau de données identique. | S05 |
| **Défense en profondeur** |  | *defense in depth* | Empilement de protections : si l'une est contournée, les autres restent. | S02 |
| **Défense en profondeur** |  | *defense in depth* | Plusieurs couches de protection superposées. | S14 |
| **Délégué à la protection des données** | DPO | *data protection officer* | Personne chargée de conseiller et de contrôler la conformité au RGPD. | S06 |
| **Demande de signature de certificat** | CSR | *certificate signing request* | Demande envoyée à l'AC : contient le nom et la clé publique du demandeur. | S12 |
| **Démarrage sécurisé** |  | *secure boot* | Chaque élément du démarrage vérifie la signature du suivant avant de lui donner la main. | S02 |
| **Détection et réponse sur les terminaux** | EDR | *endpoint detection and response* | Outil qui surveille le comportement des postes et permet de réagir à distance. | S02 |
| **Disponibilité** |  | *availability* | Le service et les données sont accessibles quand on en a besoin. | S01 |
| **Domain-based Message Authentication, Reporting and Conformance** | DMARC | *dmarc* | Politique qui dit quoi faire des messages qui échouent à SPF ou DKIM. | S09 |
| **DomainKeys Identified Mail** | DKIM | *domainkeys identified mail* | Signature cryptographique des courriels sortants d'un domaine. | S09 |
| **Donnée à caractère personnel** |  | *personal data* | Information qui permet d'identifier une personne, directement ou indirectement. | S06 |
| **Donnée sensible** |  | *special category data* | Santé, origine, opinions, religion, syndicat, génétique, biométrie, vie sexuelle : traitement interdit sauf exception. | S06 |
| **Dossier documentaire** |  | *documentary file* | Ensemble des documents qui présentent le contexte de l'étude de cas. | S18 |
| **Double extorsion** |  | *double extortion* | Les données sont volées avant d'être chiffrées, et l'attaquant menace de les publier. | S01 |
| **Droit à l'effacement** |  | *right to erasure* | Droit de faire supprimer ses données, sauf obligation légale de les conserver. | S07 |
| **Droit d'accès** |  | *right of access* | Droit d'obtenir une copie des données détenues sur soi. | S07 |
| **Durcissement** |  | *hardening* | Réduction de la surface d'attaque d'un système par sa configuration. | S14 |
| **Durée de conservation** |  | *retention period* | Durée pendant laquelle des données sont gardées, fixée selon la finalité. | S08 |
| **Échange de clés de Diffie-Hellman** | DH | *Diffie-Hellman key exchange* | Permet à deux interlocuteurs de fabriquer un secret commun sur un canal observable. | S11 |
| **Empreinte** |  | *hash* | Résultat d'un calcul à sens unique sur un contenu : même contenu, même empreinte ; un octet change, tout change. | S02 |
| **Empreinte** |  | *hash, digest* | Résultat d'une fonction de hachage ; change entièrement si les données changent. | S10 |
| **Enregistreur de frappe** |  | *keylogger* | Logiciel espion qui enregistre ce que l'on tape au clavier. | S02 |
| **Entropie** |  | *entropy* | Mesure en bits de la difficulté de deviner un secret : chaque bit double le nombre d'essais. | S03 |
| **Environnement automatique de gestion de certificats** | ACME | *automatic certificate management environment* | Protocole d'obtention et de renouvellement automatiques de certificats (Let's Encrypt). | S12 |
| **Équipement personnel utilisé au travail** | BYOD | *bring your own device* | Pratique où l'agent utilise son propre téléphone ou ordinateur pour son travail ; elle demande une charte et des mesures de séparation pro / perso. | S13 |
| **Étude de cas** |  | *case study* | Épreuve écrite fondée sur un dossier documentaire. | S18 |
| **Faux positif** |  | *false positive* | Alerte déclenchée par un comportement légitime. | S15 |
| **Fin de support** | EOL | *end of life* | Date à partir de laquelle l'éditeur ne publie plus de correctifs. | S02 |
| **Finalité** |  | *purpose* | Objectif précis et légitime pour lequel des données sont collectées. | S06 |
| **Fonction de dérivation de clé** | PBKDF2 | *password-based key derivation function 2* | Calcule une clé de chiffrement à partir d'un mot de passe, de façon lente et salée. | S10 |
| **Fonction de hachage** |  | *hash function* | Fonction à sens unique qui transforme des données en empreinte de longueur fixe. | S10 |
| **Force brute** |  | *brute force* | Essayer toutes les combinaisons possibles. | S03 |
| **Force brute** |  | *brute force* | Attaque qui essaie de nombreux mots de passe ou identifiants. | S15 |
| **Fraude au président** |  | *CEO fraud* | Faux ordre de virement attribué à un dirigeant, urgent et confidentiel. | S01 |
| **Gestion des informations et des événements de sécurité** | SIEM | *security information and event management* | Plateforme qui centralise et corrèle les journaux et déclenche des alertes. | S15 |
| **Gestionnaire de mots de passe** |  | *password manager* | Application qui génère, stocke et remplit des mots de passe dans une base chiffrée. | S03 |
| **Grappe de disques** | RAID | *redundant array of independent disks* | Plusieurs disques utilisés ensemble pour résister à la panne d'un disque. Ce n'est pas une sauvegarde. | S05 |
| **Hameçonnage** |  | *phishing* | Message frauduleux qui se fait passer pour un tiers de confiance pour obtenir une information ou une action. | S01 |
| **Hameçonnage ciblé de domaine** |  | *typosquatting* | Enregistrement d'un nom de domaine très proche d'un nom connu pour tromper les visiteurs. | S09 |
| **Harponnage** |  | *spear phishing* | Hameçonnage personnalisé pour une cible précise. | S01 |
| **HTTP Strict Transport Security** | HSTS | *HTTP strict transport security* | En-tête qui impose à un navigateur de n'utiliser que HTTPS pour un site. | S12 |
| **Hygiène numérique** |  | *cyber hygiene* | Gestes simples et réguliers qui préviennent la plupart des incidents. | S01 |
| **Identifiant de vulnérabilité** | CVE | *common vulnerabilities and exposures* | Identifiant unique d'une vulnérabilité publique, par exemple CVE-2017-0144. | S02 |
| **Identité numérique** |  | *digital identity* | Ensemble de ce qui représente une personne ou une organisation en ligne. | S09 |
| **Incident de sécurité** |  | *security incident* | Événement qui compromet ou menace la sécurité d'un système ou de données. | S17 |
| **Infrastructure à clés publiques** | PKI | *public key infrastructure* | Ensemble des acteurs et règles qui émettent, distribuent et révoquent les certificats. | S11 |
| **Ingénierie sociale** |  | *social engineering* | Techniques qui manipulent la confiance, la peur ou l'urgence d'une personne. | S01 |
| **Instantané** |  | *snapshot* | État d'un stockage à un instant donné, conservé sur le même stockage : ce n'est pas une sauvegarde. | S05 |
| **Intégrité** |  | *integrity* | Les données sont exactes et n'ont pas été modifiées à l'insu de leur propriétaire. | S01 |
| **Internet Protocol Security** | IPsec | *IPsec* | Suite de protocoles de sécurisation du protocole IP, très utilisée pour les VPN site à site. | S13 |
| **Journal d'événements** |  | *log* | Enregistrement horodaté d'événements d'un système. | S15 |
| **Liste de contrôle d'accès** | ACL | *access control list* | Liste des utilisateurs et groupes autorisés (ou refusés) sur une ressource, avec leurs droits. | S04 |
| **Liste de révocation de certificats** | CRL | *certificate revocation list* | Liste signée des certificats révoqués, publiée par l'AC. | S12 |
| **Logiciel espion** |  | *spyware* | Logiciel qui collecte discrètement des informations sur l'utilisateur. | S02 |
| **Logiciel malveillant** |  | *malware* | Logiciel conçu pour nuire : voler, détruire, espionner, extorquer. | S02 |
| **Main courante** |  | *incident log* | Journal horodaté de ce qui est constaté et décidé pendant une crise. | S17 |
| **Matrice de droits** |  | *access matrix* | Tableau croisant groupes et ressources avec le niveau d'accès de chacun. | S04 |
| **Matrice de flux** |  | *flow matrix* | Tableau des flux autorisés entre zones, avec les ports ; tout le reste est refusé. | S14 |
| **Menace** |  | *threat* | Ce qui peut causer un dommage : attaquant, logiciel malveillant, erreur, sinistre. | S01 |
| **Micrologiciel de démarrage moderne** | UEFI | *unified extensible firmware interface* | Remplaçant moderne du BIOS ; permet le démarrage sécurisé. | S02 |
| **Minimisation** |  | *data minimisation* | Ne collecter que les données nécessaires à la finalité. | S06 |
| **Mode opératoire** |  | *mode of operation* | Manière d'enchaîner les blocs d'un chiffrement par blocs (ECB, CBC, CTR, GCM). | S10 |
| **Module de plateforme sécurisée** | TPM | *trusted platform module* | Puce qui stocke des clés et mesure l'état du démarrage. | S02 |
| **Moindre privilège** |  | *least privilege* | Ne donner que les droits strictement nécessaires, pour la durée nécessaire. | S04 |
| **Mot de passe à usage unique basé sur l'heure** | TOTP | *time-based one-time password* | Code à 6 chiffres calculé à partir d'un secret partagé et de l'heure, renouvelé toutes les 30 secondes. | S03 |
| **Noms alternatifs du sujet** | SAN | *subject alternative name* | Champ du certificat qui liste les noms de domaine valables. | S11 |
| **Non-répudiation** |  | *non-repudiation* | L'auteur d'un acte ne peut pas nier en être l'auteur. | S11 |
| **Notification à la CNIL** |  | *breach notification* | Déclaration d'une violation à la CNIL, sous 72 heures en cas de risque. | S08 |
| **Objectif de point de reprise** | RPO | *recovery point objective* | Durée maximale de données que l'on accepte de perdre. | S05 |
| **Objectif de temps de reprise** | RTO | *recovery time objective* | Durée maximale d'interruption que l'on accepte. | S05 |
| **Onduleur** | UPS | *uninterruptible power supply* | Batterie qui alimente les équipements quelques minutes lors d'une coupure de courant. | S01 |
| **Ordre de volatilité** |  | *order of volatility* | Ordre de collecte des preuves, du plus éphémère au plus durable. | S17 |
| **Pare-feu** |  | *firewall* | Dispositif qui filtre les flux selon des règles. | S14 |
| **Plan de continuité d'activité** | PCA | *business continuity plan* | Comment continuer à travailler pendant un incident. | S05 |
| **Plan de reprise d'activité** | PRA | *disaster recovery plan* | Comment redémarrer et restaurer après un incident. | S05 |
| **Portabilité** |  | *data portability* | Droit de récupérer ses données dans un format structuré et lisible par une machine. | S07 |
| **Porte dérobée** |  | *backdoor* | Accès caché laissé par un attaquant pour revenir sur la machine. | S02 |
| **Preuve** |  | *non-repudiation* | Capacité de démontrer qui a fait quoi, et quand. | S01 |
| **Protocole d'état des certificats en ligne** | OCSP | *online certificate status protocol* | Interrogation en ligne de l'état de révocation d'un certificat. | S12 |
| **Pseudonymisation** |  | *pseudonymisation* | Remplacement de l'identité par un code : la donnée reste personnelle. | S08 |
| **Rançongiciel** |  | *ransomware* | Logiciel malveillant qui chiffre les fichiers et réclame une rançon. | S01 |
| **Rançongiciel** |  | *ransomware* | Logiciel malveillant qui chiffre les données et exige une rançon. | S17 |
| **Registre des traitements** |  | *record of processing activities* | Document qui recense les traitements de données personnelles (article 30). | S06 |
| **Règlement général sur la protection des données** | RGPD | *general data protection regulation (GDPR)* | Règlement européen qui encadre le traitement des données personnelles. | S06 |
| **Réseau de machines zombies** |  | *botnet* | Ensemble de machines compromises pilotées à distance par un attaquant. | S02 |
| **Réseau local virtuel** | VLAN | *virtual LAN* | Découpage logique d'un réseau en segments isolés. | S14 |
| **Réseau privé virtuel** | VPN | *virtual private network* | Tunnel chiffré et authentifié à travers un réseau non sûr. | S13 |
| **Responsable de traitement** |  | *data controller* | Organisme qui décide des finalités et des moyens d'un traitement. | S06 |
| **Retour d'expérience** | REX | *lessons learned* | Analyse d'un incident pour en tirer des actions d'amélioration. | S17 |
| **Risque** |  | *risk* | Possibilité qu'une menace exploite une vulnérabilité, mesurée par sa gravité et sa vraisemblance. | S01 |
| **Rivest-Shamir-Adleman** | RSA | *RSA* | Algorithme asymétrique de chiffrement et de signature. | S11 |
| **Rootkit** |  | *rootkit* | Logiciel qui masque sa présence et celle d'autres codes malveillants au système. | S02 |
| **Rotation des journaux** |  | *log rotation* | Archivage et suppression périodiques des fichiers de journaux. | S08 |
| **Sauvegarde complète** |  | *full backup* | Copie de toutes les données. | S05 |
| **Sauvegarde différentielle** |  | *differential backup* | Copie de ce qui a changé depuis la dernière sauvegarde complète. | S05 |
| **Sauvegarde incrémentielle** |  | *incremental backup* | Copie de ce qui a changé depuis la dernière sauvegarde, quelle qu'elle soit. | S05 |
| **Scan de ports** |  | *port scan* | Test des ports ouverts d'une machine. | S16 |
| **Secure Shell** | SSH | *secure shell* | Protocole d'administration à distance chiffré. | S14 |
| **Sel** |  | *salt* | Valeur aléatoire ajoutée à un mot de passe avant hachage, propre à chaque utilisateur. | S03 |
| **Sender Policy Framework** | SPF | *sender policy framework* | Enregistrement DNS qui déclare les serveurs autorisés à envoyer du courrier pour un domaine. | S09 |
| **Séparation des tâches** |  | *separation of duties* | Une action sensible exige l'intervention de deux personnes. | S04 |
| **Serveur de mises à jour de Windows** | WSUS | *windows server update services* | Service qui distribue et contrôle les mises à jour dans un domaine. | S02 |
| **Signature électronique** |  | *electronic signature* | Procédé qui identifie un signataire et manifeste son consentement. | S09 |
| **Signature numérique** |  | *digital signature* | Empreinte signée avec la clé privée : garantit intégrité, authenticité et non-répudiation. | S11 |
| **Sous-traitant** |  | *data processor* | Organisme qui traite des données pour le compte du responsable, sous contrat. | S06 |
| **Sûreté** |  | *safety* | Protection contre les événements non intentionnels : panne, incendie, dégât des eaux, coupure électrique. | S01 |
| **Surface d'attaque** |  | *attack surface* | Ensemble des points par lesquels un attaquant peut tenter d'entrer. | S14 |
| **Système de détection d'intrusion** | IDS | *intrusion detection system* | Observe le trafic ou une machine et émet des alertes. | S15 |
| **Système de notation des vulnérabilités** | CVSS | *common vulnerability scoring system* | Note de gravité d'une vulnérabilité de 0 à 10. | S02 |
| **Système de prévention d'intrusion** | IPS | *intrusion prevention system* | Comme un IDS, mais bloque le trafic suspect. | S15 |
| **Tâche planifiée** | cron | *scheduled job* | Mécanisme Unix qui exécute une commande à heure fixe. | S08 |
| **Test d'intrusion** |  | *penetration test* | Exploitation contrôlée des failles pour mesurer l'impact réel. | S16 |
| **Traceur** |  | *tracker* | Dispositif qui permet de suivre un utilisateur (cookie, pixel, identifiant d'appareil). | S07 |
| **Transport Layer Security** | TLS | *transport layer security* | Protocole de sécurisation des échanges, utilisé par HTTPS. | S11 |
| **Tunnel complet** |  | *full tunnel* | Tout le trafic du client passe par le VPN. | S13 |
| **Tunnel partiel** |  | *split tunnel* | Seul le trafic vers le réseau d'entreprise passe par le VPN. | S13 |
| **Tunnelisation** |  | *tunneling* | Encapsulation de paquets dans d'autres paquets, après chiffrement. | S13 |
| **Vecteur d'initialisation** | IV | *initialization vector* | Valeur non secrète, imprévisible ou unique, qui démarre un chiffrement. | S10 |
| **Ver** |  | *worm* | Logiciel malveillant autonome qui se propage de machine en machine par le réseau. | S02 |
| **Violation de données** |  | *data breach* | Atteinte à la sécurité qui détruit, perd, altère ou divulgue des données personnelles. | S08 |
| **Virus** |  | *virus* | Code qui s'attache à un fichier hôte et se propage quand on ouvre ce fichier. | S02 |
| **VPN nomade** |  | *remote access VPN* | Un utilisateur se connecte au réseau de l'entreprise depuis l'extérieur. | S13 |
| **VPN site à site** |  | *site-to-site VPN* | Deux réseaux sont reliés en permanence par un tunnel. | S13 |
| **Vulnérabilité** |  | *vulnerability* | Faiblesse qu'une menace peut exploiter. | S01 |
| **Vulnérabilité** |  | *vulnerability* | Faiblesse d'un système qui peut être exploitée. | S16 |
| **WireGuard** |  | *WireGuard* | Protocole de VPN moderne, simple, fondé sur une paire de clés par machine. | S13 |
| **Zone démilitarisée** | DMZ | *demilitarized zone* | Zone réseau qui héberge les services exposés à Internet, isolée du réseau interne. | S14 |
