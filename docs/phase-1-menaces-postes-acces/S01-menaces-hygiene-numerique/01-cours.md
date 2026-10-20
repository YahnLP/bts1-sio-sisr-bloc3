# Cours – Menaces et hygiène numérique

*BTS SIO SISR 1re année – Bloc 3 – S01 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** Aucun (séance d'introduction au bloc 3).
> - **Matériel :** Postes de la salle ; une VM Windows de laboratoire ; navigateur web

## À la fin de ce cours tu sauras

- [ ] **Définir** la cybersécurité par ses quatre principes : disponibilité, intégrité, confidentialité, preuve ;
- [ ] **Distinguer** menace, vulnérabilité, risque et impact sur un cas concret ;
- [ ] **Décrire** le déroulement d'une attaque par rançongiciel et d'une attaque par hameçonnage ;
- [ ] **Repérer** les indices d'un message frauduleux (expéditeur, lien, pièce jointe, urgence) et choisir la bonne réaction ;
- [ ] **Distinguer** sûreté et sécurité et **vérifier** les éléments de sûreté d'un local technique ;
- [ ] **Appliquer** les règles d'hygiène numérique et **rédiger** un support de sensibilisation pour des utilisateurs.

## I. Pourquoi parler de cybersécurité ?

Une organisation dépend de son système d'information pour travailler : messagerie, fichiers, logiciel de gestion, accès à internet. La **cybersécurité** est l'ensemble des moyens qui protègent ce système et les données qu'il contient. Elle repose sur quatre principes, que l'on retrouve dans le référentiel du BTS :

| Principe | Question posée | Exemple d'atteinte |
|---|---|---|
| **Disponibilité** | Le service et les données sont-ils accessibles quand on en a besoin ? | Un rançongiciel bloque tous les postes |
| **Intégrité** | Les données sont-elles exactes, non modifiées à l'insu de leur propriétaire ? | Un IBAN est modifié dans une facture |
| **Confidentialité** | Seules les personnes autorisées peuvent-elles lire l'information ? | Une base de clients est publiée en ligne |
| **Preuve** | Peut-on démontrer qui a fait quoi, et quand ? | Aucun journal ne permet de retracer l'intrusion |

**Je vérifie.** Une sauvegarde qu'on ne parvient pas à restaurer, c'est une atteinte à quel principe ?

<details markdown="1">
<summary>Voir la réponse</summary>

À la **disponibilité** : les données existent, mais on ne peut plus s'en servir. C'est pourquoi on teste les restaurations (voir S05).

</details>

### A. Menace, vulnérabilité, risque

Ces mots ne sont pas synonymes.

| Terme | Définition | Exemple |
|---|---|---|
| **Actif** | Ce qu'il faut protéger | Le serveur de fichiers, la base clients |
| **Menace** | Ce qui peut causer un dommage | Un pirate, un rançongiciel, une erreur humaine, un incendie |
| **Vulnérabilité** | Une faiblesse que la menace peut exploiter | Un système non mis à jour, un mot de passe faible |
| **Risque** | La possibilité qu'une menace exploite une vulnérabilité, avec une **gravité** et une **vraisemblance** | « Un rançongiciel chiffre le serveur de fichiers par une faille non corrigée » |
| **Impact** | Les conséquences : arrêt d'activité, perte financière, sanction juridique, atteinte à l'image | Trois jours sans facturation |

On réduit un risque de trois façons : diminuer la vraisemblance (**prévenir**), diminuer la gravité (**limiter**, par exemple avec une sauvegarde) ou l'accepter en connaissance de cause.

### B. Sûreté et sécurité

Deux mots proches, deux familles de causes :

| | **Sûreté** | **Sécurité** |
|---|---|---|
| Contre quoi ? | Les événements **non intentionnels** : panne, incendie, dégât des eaux, coupure électrique, surchauffe, erreur | Les actes **malveillants** : intrusion, vol, rançongiciel |
| Exemples de mesures | Onduleur, parafoudre, climatisation, détection d'incendie, redondance | Mots de passe, droits, pare-feu, antivirus |

Un même actif a besoin des deux : un serveur chiffré et à jour (sécurité) reste perdu si le local est inondé (sûreté). Le référentiel demande de **vérifier les éléments de sûreté** d'une infrastructure. Pour un local technique, on contrôle :

| Élément | À vérifier |
|---|---|
| Alimentation | Onduleur présent, autonomie suffisante, test périodique, parafoudre |
| Climat | Température maîtrisée, ventilation dégagée |
| Incendie | Détection, extinction adaptée, matériel éloigné des sources de chaleur |
| Eau | Rien sous une canalisation, équipements surélevés |
| Accès physique | Local fermé, accès limité et tracé |
| Redondance | Alimentation et disques doublés, sauvegarde hors du local |

**Exemple.** Un onduleur dont la batterie fournit 360 Wh utilisables alimente des équipements qui consomment 240 W : autonomie = 360 / 240 = **1,5 h**, soit 90 minutes. C'est le temps dont on dispose pour arrêter proprement les machines.

**Je vérifie.** Un incendie dans le local détruit le serveur et la sauvegarde posée à côté. Est-ce un défaut de sûreté ou de sécurité ? Quelle mesure aurait limité les dégâts ? ______________________

<details markdown="1">
<summary>Éléments de réponse</summary>

Défaut de **sûreté** (événement non intentionnel). Une copie de sauvegarde **hors du local** (ou hors site) et une détection d'incendie auraient limité les dégâts.

</details>

### C. Le facteur humain

Les mesures techniques (pare-feu, antivirus, filtrage) arrêtent beaucoup d'attaques, mais pas celles qui **convainquent un utilisateur** d'ouvrir lui-même la porte. L'**ingénierie sociale** désigne l'ensemble des techniques qui manipulent la confiance, la peur, l'urgence ou la curiosité d'une personne. C'est pourquoi l'administrateur ne fait pas que de la technique : il **informe et sensibilise** les utilisateurs, ce qui est une compétence du bloc 3.

## II. Le rançongiciel

Un **rançongiciel** (*ransomware*) est un logiciel malveillant qui **chiffre** les fichiers de la victime, puis réclame une **rançon** contre la clé de déchiffrement. Les attaquants volent souvent aussi des données avant de chiffrer, pour menacer de les publier : c'est la **double extorsion**.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 384.60 618.60" style="max-width:513px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 607.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M319.5,-597C319.5,-597 43.5,-597 43.5,-597 37.5,-597 31.5,-591 31.5,-585 31.5,-585 31.5,-538 31.5,-538 31.5,-532 37.5,-526 43.5,-526 43.5,-526 319.5,-526 319.5,-526 325.5,-526 331.5,-532 331.5,-538 331.5,-538 331.5,-585 331.5,-585 331.5,-591 325.5,-597 319.5,-597"/>
<text text-anchor="start" x="127" y="-575" font-family="Helvetica,sans-Serif" font-size="15.00">1. Accès initial</text>
<text text-anchor="start" x="50.5" y="-558" font-family="Helvetica,sans-Serif" font-size="15.00">message piégé, mot de passe volé,</text>
<text text-anchor="start" x="80.5" y="-541" font-family="Helvetica,sans-Serif" font-size="15.00">service exposé non corrigé</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M304.5,-468C304.5,-468 58.5,-468 58.5,-468 52.5,-468 46.5,-462 46.5,-456 46.5,-456 46.5,-426 46.5,-426 46.5,-420 52.5,-414 58.5,-414 58.5,-414 304.5,-414 304.5,-414 310.5,-414 316.5,-420 316.5,-426 316.5,-426 316.5,-456 316.5,-456 316.5,-462 310.5,-468 304.5,-468"/>
<text text-anchor="start" x="130" y="-446" font-family="Helvetica,sans-Serif" font-size="15.00">2. Installation</text>
<text text-anchor="start" x="65.5" y="-429" font-family="Helvetica,sans-Serif" font-size="15.00">et déplacement dans le réseau</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M181.5,-525.91C181.5,-510.63 181.5,-492.7 181.5,-477.34"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="184.65,-477.15 181.5,-468.15 178.35,-477.15 184.65,-477.15"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M284,-356C284,-356 79,-356 79,-356 73,-356 67,-350 67,-344 67,-344 67,-314 67,-314 67,-308 73,-302 79,-302 79,-302 284,-302 284,-302 290,-302 296,-308 296,-314 296,-314 296,-344 296,-344 296,-350 290,-356 284,-356"/>
<text text-anchor="start" x="86" y="-334" font-family="Helvetica,sans-Serif" font-size="15.00">3. Élévation de privilèges</text>
<text text-anchor="start" x="95.5" y="-317" font-family="Helvetica,sans-Serif" font-size="15.00">compte administrateur</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M181.5,-413.93C181.5,-399.52 181.5,-381.39 181.5,-365.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="184.65,-365.26 181.5,-356.26 178.35,-365.26 184.65,-365.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M351,-244C351,-244 12,-244 12,-244 6,-244 0,-238 0,-232 0,-232 0,-202 0,-202 0,-196 6,-190 12,-190 12,-190 351,-190 351,-190 357,-190 363,-196 363,-202 363,-202 363,-232 363,-232 363,-238 357,-244 351,-244"/>
<text text-anchor="start" x="115" y="-222" font-family="Helvetica,sans-Serif" font-size="15.00">4. Vol de données</text>
<text text-anchor="start" x="19" y="-205" font-family="Helvetica,sans-Serif" font-size="15.00">et destruction des sauvegardes accessibles</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M181.5,-301.93C181.5,-287.52 181.5,-269.39 181.5,-253.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="184.65,-253.26 181.5,-244.26 178.35,-253.26 184.65,-253.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M288,-132C288,-132 75,-132 75,-132 69,-132 63,-126 63,-120 63,-120 63,-107 63,-107 63,-101 69,-95 75,-95 75,-95 288,-95 288,-95 294,-95 300,-101 300,-107 300,-107 300,-120 300,-120 300,-126 294,-132 288,-132"/>
<text text-anchor="start" x="82" y="-110" font-family="Helvetica,sans-Serif" font-size="15.00">5. Chiffrement des fichiers</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M181.5,-189.86C181.5,-175.02 181.5,-156.48 181.5,-141.5"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="184.65,-141.24 181.5,-132.24 178.35,-141.24 184.65,-141.24"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M274,-37C274,-37 89,-37 89,-37 83,-37 77,-31 77,-25 77,-25 77,-12 77,-12 77,-6 83,0 89,0 89,0 274,0 274,0 280,0 286,-6 286,-12 286,-12 286,-25 286,-25 286,-31 280,-37 274,-37"/>
<text text-anchor="start" x="96" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">6. Demande de rançon</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M181.5,-94.57C181.5,-80.84 181.5,-61.7 181.5,-46.18"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="184.65,-46.06 181.5,-37.06 178.35,-46.06 184.65,-46.06"/>
</g>
</g>
</svg>
</figure>

**Cas réel : WannaCry (12 mai 2017).** Ce ver s'est propagé de poste en poste en exploitant une faille du protocole de partage de fichiers de Windows (SMBv1, vulnérabilité **CVE-2017-0144**, outil *EternalBlue*). Microsoft avait publié le correctif (bulletin MS17-010) le **14 mars 2017**, soit près de deux mois avant. Les machines non mises à jour ont été chiffrées : on cite couramment plus de 200 000 machines dans environ 150 pays, dont des hôpitaux britanniques et des industriels. La propagation a été freinée par un chercheur qui a enregistré un nom de domaine servant d'« interrupteur » au code.

**Leçons :** une faille **connue et corrigée** reste exploitable tant qu'on ne met pas à jour ; un service inutile exposé (SMBv1) agrandit la surface d'attaque ; la **sauvegarde hors ligne** est la meilleure parade quand tout le reste a échoué.

> [!WARNING]
> **Payer la rançon ne garantit pas de récupérer ses données** et finance les attaquants. La conduite à tenir en cas d'incident est vue en S17 : isoler, préserver les preuves, prévenir, restaurer.

## III. L'hameçonnage et l'ingénierie sociale

L'**hameçonnage** (*phishing*) est un message qui se fait passer pour un tiers de confiance afin d'obtenir une information (identifiant, code, numéro de carte) ou une action (ouvrir un fichier, effectuer un virement).

| Variante | Canal | Particularité |
|---|---|---|
| **Hameçonnage** classique | Courriel | Envoi de masse, faux site de connexion |
| **Harponnage** (*spear phishing*) | Courriel | Message personnalisé pour une cible précise, informations tirées de réseaux sociaux |
| **Fraude au président** | Courriel, téléphone | Un faux dirigeant ordonne un virement urgent et confidentiel |
| **Smishing** | SMS | Faux suivi de colis, faux remboursement |
| **Vishing** | Téléphone | Faux conseiller bancaire ou faux support technique |

### Les indices d'un message frauduleux

1. **L'expéditeur** : afficher l'adresse réelle, pas seulement le nom (`service@paypa1.example` n'est pas `paypal`).
2. **Le lien** : survoler **sans cliquer** pour lire la vraie adresse ; un nom de domaine proche d'un nom connu est un piège.
3. **La pression** : urgence, menace de fermeture, de sanction, ou au contraire gain inespéré.
4. **La demande** : un mot de passe, un code reçu par SMS ou un virement ne se demandent jamais par message.
5. **La pièce jointe** : archive, fichier exécutable, ou **double extension** (`facture.pdf.exe`).

**Je vérifie.** Un message de « votre directeur » demande un virement urgent et confidentiel sur un nouveau compte. Le texte est parfaitement écrit. Que fais-tu ?

<details markdown="1">
<summary>Voir la réponse</summary>

On **n'exécute pas** le virement. On vérifie la demande par un **autre canal** (appel au numéro connu du dirigeant), on prévient le service informatique et on conserve le message. Une orthographe correcte ne prouve rien : les messages ciblés sont soignés. La **procédure de validation** d'un virement (double contrôle) est la vraie parade.

</details>

## IV. Les règles d'hygiène numérique

L'**hygiène numérique** réunit les gestes simples qui préviennent la plupart des incidents. Elle s'inspire des guides publiés par l'ANSSI (par exemple le *Guide des bonnes pratiques de l'informatique*, rédigé avec la CPME) et par Cybermalveillance.gouv.fr. Les sites officiels évoluent : consulte leur version actuelle.

| Règle | Pourquoi | Séance qui l'approfondit |
|---|---|---|
| Mettre à jour système et logiciels | Corriger les failles connues (voir WannaCry) | S02, S14 |
| Utiliser un antivirus ou une solution de protection à jour | Détecter les logiciels malveillants connus | S02 |
| Choisir des mots de passe longs et uniques, activer la double authentification | Empêcher l'usurpation de compte | S03 |
| N'utiliser que les droits nécessaires, éviter le compte administrateur au quotidien | Limiter les dégâts d'une compromission | S04 |
| Sauvegarder (règle 3-2-1) et tester la restauration | Survivre à un rançongiciel ou à une panne | S05 |
| Chiffrer les supports nomades et les données sensibles | Une perte ou un vol ne devient pas une fuite | S10 |
| Se méfier des messages, liens et pièces jointes | Bloquer l'ingénierie sociale | S01 |
| Verrouiller sa session quand on s'éloigne (`Windows` + `L`) | Éviter l'accès physique | S01 |
| Séparer usages professionnels et personnels | Limiter la propagation et protéger la vie privée | S09 |
| Se connecter avec prudence hors du réseau de l'entreprise (Wi-Fi public, VPN de l'organisation) | Empêcher l'écoute du trafic | S13 |

> [!NOTE]
> Dans une organisation, ces règles figurent dans la **charte informatique**, que les utilisateurs signent. Elle protège aussi l'entreprise : elle fixe ce qui est permis, ce qui est surveillé et les sanctions possibles (voir S08).

## V. Où signaler, où se renseigner

- **Message d'hameçonnage** : le signaler au service informatique de l'organisation ; en usage personnel, à la plateforme officielle de signalement des spams (signal-spam.fr) ; pour un SMS frauduleux, au 33700.
- **Victime d'une infraction numérique** : Cybermalveillance.gouv.fr propose un diagnostic et une mise en relation avec des prestataires ; le dépôt de plainte se fait auprès de la police ou de la gendarmerie (dispositif 17Cyber). Vérifie les dispositifs en vigueur le jour où tu en as besoin.
- **Vulnérabilité ou alerte technique** : le CERT-FR de l'ANSSI publie des avis et des alertes.

## À retenir

- La cybersécurité protège la **disponibilité**, l'**intégrité**, la **confidentialité** et la **preuve**.
- **Risque = menace qui exploite une vulnérabilité**, avec une gravité et une vraisemblance.
- Beaucoup d'attaques passent par l'**utilisateur** : former est une mesure de sécurité à part entière.
- **Sûreté** : se protéger des accidents et pannes (onduleur, incendie, eau, redondance) ; **sécurité** : se protéger des actes malveillants. Les deux se vérifient.
- Un rançongiciel se prévient par les **mises à jour**, des **droits limités** et une **sauvegarde testée hors ligne**.
- Devant un message suspect : **ne pas cliquer, vérifier par un autre canal, signaler**.
