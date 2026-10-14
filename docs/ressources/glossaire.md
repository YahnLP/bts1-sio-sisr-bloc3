# Glossaire

Tous les mots techniques du bloc 3, expliqués simplement. Dans les pages du site, **passe la souris sur un sigle** (VLAN, DHCP, GPO…) : sa définition s'affiche.

> [!NOTE]
> Un terme suivi de la mention **notion technique** dépasse le socle de première année : tu peux le laisser de côté.

La colonne « Vu en » indique la séance où le mot apparaît pour la première fois dans le cours.

| Terme | Sigle | Anglais | Définition | Vu en |
|---|---|---|---|---|
| **Actif** |  | *asset* | Ce qu'il faut protéger : donnée, serveur, application, service. | S01 |
| **Agence nationale de la sécurité des systèmes d'information** | ANSSI |  | Autorité française de cybersécurité, qui publie guides, recommandations et alertes. | S01 |
| **Authentification** |  | *authentication* | Prouver que l'on est bien la personne que l'on prétend être. | S03 |
| **Authentification multifacteur** | MFA | *multi-factor authentication* | Authentification qui exige au moins deux facteurs de types différents. | S03 |
| **Authentification résistante à l'hameçonnage** | FIDO2 |  | Norme de clés de sécurité et de passkeys qui ne répondent qu'au site réel. | S03 |
| **Autorisation** |  | *authorization* | Décider de ce qu'une personne authentifiée a le droit de faire. | S03 |
| **Bit setgid** |  | *setgid* | Sur un dossier Linux, fait hériter les nouveaux fichiers du groupe du dossier. | S04 |
| **Bourrage d'identifiants** |  | *credential stuffing* | Réessayer sur un service des identifiants volés sur un autre. | S03 |
| **Centre gouvernemental de veille, d'alerte et de réponse aux attaques** | CERT-FR | *computer emergency response team* | Équipe de l'ANSSI qui publie avis et alertes de sécurité. | S01 |
| **Charte informatique** |  | *acceptable use policy* | Document signé par les utilisateurs qui fixe les règles d'usage du système d'information. | S01 |
| **Cheval de Troie** |  | *trojan* | Logiciel qui se présente comme utile pour se faire installer par l'utilisateur. | S02 |
| **Chiffrement de disque de Windows** | BitLocker |  | Fonction de Windows qui chiffre un disque entier. | S02 |
| **Chiffrement de volume de Linux** | LUKS | *linux unified key setup* | Standard de chiffrement de disques et de volumes sous Linux. | S05 |
| **Commission nationale de l'informatique et des libertés** | CNIL |  | Autorité française de protection des données personnelles. | S03 |
| **Confidentialité** |  | *confidentiality* | Seules les personnes autorisées peuvent lire l'information. | S01 |
| **Contrôle d'accès discrétionnaire** | DAC | *discretionary access control* | Le propriétaire d'une ressource décide qui y accède. | S04 |
| **Contrôle d'accès obligatoire** | MAC | *mandatory access control* | Une politique centrale fixe les accès, que l'utilisateur ne peut pas modifier. | S04 |
| **Contrôle d'accès par rôles** | RBAC | *role-based access control* | Les droits sont donnés à des rôles, auxquels on affecte des utilisateurs. | S04 |
| **Correctif** |  | *patch* | Mise à jour qui corrige une faille ou un défaut. | S02 |
| **Cybersécurité** |  | *cybersecurity* | Ensemble des moyens qui protègent un système d'information et ses données. | S01 |
| **Déduplication** |  | *deduplication* | Technique qui ne stocke qu'une fois chaque morceau de données identique. | S05 |
| **Défense en profondeur** |  | *defense in depth* | Empilement de protections : si l'une est contournée, les autres restent. | S02 |
| **Démarrage sécurisé** |  | *secure boot* | Chaque élément du démarrage vérifie la signature du suivant avant de lui donner la main. | S02 |
| **Détection et réponse sur les terminaux** | EDR | *endpoint detection and response* | Outil qui surveille le comportement des postes et permet de réagir à distance. | S02 |
| **Disponibilité** |  | *availability* | Le service et les données sont accessibles quand on en a besoin. | S01 |
| **Double extorsion** |  | *double extortion* | Les données sont volées avant d'être chiffrées, et l'attaquant menace de les publier. | S01 |
| **Empreinte** |  | *hash* | Résultat d'un calcul à sens unique sur un contenu : même contenu, même empreinte ; un octet change, tout change. | S02 |
| **Enregistreur de frappe** |  | *keylogger* | Logiciel espion qui enregistre ce que l'on tape au clavier. | S02 |
| **Entropie** |  | *entropy* | Mesure en bits de la difficulté de deviner un secret : chaque bit double le nombre d'essais. | S03 |
| **Fin de support** | EOL | *end of life* | Date à partir de laquelle l'éditeur ne publie plus de correctifs. | S02 |
| **Force brute** |  | *brute force* | Essayer toutes les combinaisons possibles. | S03 |
| **Fraude au président** |  | *CEO fraud* | Faux ordre de virement attribué à un dirigeant, urgent et confidentiel. | S01 |
| **Gestionnaire de mots de passe** |  | *password manager* | Application qui génère, stocke et remplit des mots de passe dans une base chiffrée. | S03 |
| **Grappe de disques** | RAID | *redundant array of independent disks* | Plusieurs disques utilisés ensemble pour résister à la panne d'un disque. Ce n'est pas une sauvegarde. | S05 |
| **Hameçonnage** |  | *phishing* | Message frauduleux qui se fait passer pour un tiers de confiance pour obtenir une information ou une action. | S01 |
| **Harponnage** |  | *spear phishing* | Hameçonnage personnalisé pour une cible précise. | S01 |
| **Hygiène numérique** |  | *cyber hygiene* | Gestes simples et réguliers qui préviennent la plupart des incidents. | S01 |
| **Identifiant de vulnérabilité** | CVE | *common vulnerabilities and exposures* | Identifiant unique d'une vulnérabilité publique, par exemple CVE-2017-0144. | S02 |
| **Ingénierie sociale** |  | *social engineering* | Techniques qui manipulent la confiance, la peur ou l'urgence d'une personne. | S01 |
| **Instantané** |  | *snapshot* | État d'un stockage à un instant donné, conservé sur le même stockage : ce n'est pas une sauvegarde. | S05 |
| **Intégrité** |  | *integrity* | Les données sont exactes et n'ont pas été modifiées à l'insu de leur propriétaire. | S01 |
| **Liste de contrôle d'accès** | ACL | *access control list* | Liste des utilisateurs et groupes autorisés (ou refusés) sur une ressource, avec leurs droits. | S04 |
| **Logiciel espion** |  | *spyware* | Logiciel qui collecte discrètement des informations sur l'utilisateur. | S02 |
| **Logiciel malveillant** |  | *malware* | Logiciel conçu pour nuire : voler, détruire, espionner, extorquer. | S02 |
| **Matrice de droits** |  | *access matrix* | Tableau croisant groupes et ressources avec le niveau d'accès de chacun. | S04 |
| **Menace** |  | *threat* | Ce qui peut causer un dommage : attaquant, logiciel malveillant, erreur, sinistre. | S01 |
| **Micrologiciel de démarrage moderne** | UEFI | *unified extensible firmware interface* | Remplaçant moderne du BIOS ; permet le démarrage sécurisé. | S02 |
| **Module de plateforme sécurisée** | TPM | *trusted platform module* | Puce qui stocke des clés et mesure l'état du démarrage. | S02 |
| **Moindre privilège** |  | *least privilege* | Ne donner que les droits strictement nécessaires, pour la durée nécessaire. | S04 |
| **Mot de passe à usage unique basé sur l'heure** | TOTP | *time-based one-time password* | Code à 6 chiffres calculé à partir d'un secret partagé et de l'heure, renouvelé toutes les 30 secondes. | S03 |
| **Objectif de point de reprise** | RPO | *recovery point objective* | Durée maximale de données que l'on accepte de perdre. | S05 |
| **Objectif de temps de reprise** | RTO | *recovery time objective* | Durée maximale d'interruption que l'on accepte. | S05 |
| **Plan de continuité d'activité** | PCA | *business continuity plan* | Comment continuer à travailler pendant un incident. | S05 |
| **Plan de reprise d'activité** | PRA | *disaster recovery plan* | Comment redémarrer et restaurer après un incident. | S05 |
| **Porte dérobée** |  | *backdoor* | Accès caché laissé par un attaquant pour revenir sur la machine. | S02 |
| **Preuve** |  | *non-repudiation* | Capacité de démontrer qui a fait quoi, et quand. | S01 |
| **Rançongiciel** |  | *ransomware* | Logiciel malveillant qui chiffre les fichiers et réclame une rançon. | S01 |
| **Réseau de machines zombies** |  | *botnet* | Ensemble de machines compromises pilotées à distance par un attaquant. | S02 |
| **Risque** |  | *risk* | Possibilité qu'une menace exploite une vulnérabilité, mesurée par sa gravité et sa vraisemblance. | S01 |
| **Rootkit** |  | *rootkit* | Logiciel qui masque sa présence et celle d'autres codes malveillants au système. | S02 |
| **Sauvegarde complète** |  | *full backup* | Copie de toutes les données. | S05 |
| **Sauvegarde différentielle** |  | *differential backup* | Copie de ce qui a changé depuis la dernière sauvegarde complète. | S05 |
| **Sauvegarde incrémentielle** |  | *incremental backup* | Copie de ce qui a changé depuis la dernière sauvegarde, quelle qu'elle soit. | S05 |
| **Sel** |  | *salt* | Valeur aléatoire ajoutée à un mot de passe avant hachage, propre à chaque utilisateur. | S03 |
| **Séparation des tâches** |  | *separation of duties* | Une action sensible exige l'intervention de deux personnes. | S04 |
| **Serveur de mises à jour de Windows** | WSUS | *windows server update services* | Service qui distribue et contrôle les mises à jour dans un domaine. | S02 |
| **Système de notation des vulnérabilités** | CVSS | *common vulnerability scoring system* | Note de gravité d'une vulnérabilité de 0 à 10. | S02 |
| **Ver** |  | *worm* | Logiciel malveillant autonome qui se propage de machine en machine par le réseau. | S02 |
| **Virus** |  | *virus* | Code qui s'attache à un fichier hôte et se propage quand on ouvre ce fichier. | S02 |
| **Vulnérabilité** |  | *vulnerability* | Faiblesse qu'une menace peut exploiter. | S01 |
