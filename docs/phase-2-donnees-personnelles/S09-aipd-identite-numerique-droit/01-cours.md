# Cours – AIPD, identité numérique de l'organisation et cadre pénal

*BTS SIO SISR 1re année – Bloc 3 – S09 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S06 à S08 (RGPD : registre, droits, conservation, violations).
> - **Matériel :** Fiches papier ou traitement de texte ; accès à Internet pour consulter cnil.fr et legifrance.gouv.fr

## À la fin de ce cours tu sauras

- [ ] **Décider** si un traitement exige une analyse d'impact (AIPD) à partir des critères de la CNIL ;
- [ ] **Conduire** les quatre étapes d'une AIPD et **coter** un risque (vraisemblance × gravité) ;
- [ ] **Définir** l'identité numérique d'une organisation et **traiter** un cas d'usurpation ou d'atteinte à la réputation ;
- [ ] **Expliquer** la valeur d'un écrit et d'une signature électroniques (preuve) ;
- [ ] **Qualifier** des comportements au regard des infractions informatiques et **situer** la responsabilité de l'administrateur.

## I. L'analyse d'impact (AIPD)

### Quand est-elle obligatoire ?

L'**analyse d'impact relative à la protection des données** (AIPD, article 35) est exigée **avant** de mettre en œuvre un traitement susceptible d'engendrer un **risque élevé** pour les droits et libertés des personnes. Elle se fait **en amont**, pas après la mise en production.

La CNIL s'appuie sur **neuf critères** :

| # | Critère | Exemple |
|---|---|---|
| 1 | **Évaluation ou notation** de personnes | Score de solvabilité, profilage |
| 2 | **Décision automatisée** avec effet juridique ou significatif | Refus automatique de crédit |
| 3 | **Surveillance systématique** | Vidéosurveillance, suivi de géolocalisation |
| 4 | Données **sensibles** ou à caractère très personnel | Santé, opinions, données financières, localisation |
| 5 | Traitement à **grande échelle** | Données de milliers de personnes |
| 6 | **Croisement** de jeux de données | Rapprocher fichiers clients et données d'achats externes |
| 7 | Personnes **vulnérables** | Patients, mineurs, salariés |
| 8 | Usage **innovant** ou nouvelle technologie | Reconnaissance faciale, intelligence artificielle |
| 9 | Traitement qui **empêche l'exercice d'un droit** ou l'accès à un service | Liste noire |

**Règle de décision :** si le traitement remplit **au moins deux** critères, l'AIPD est en principe obligatoire. La CNIL publie aussi des listes de traitements qui exigent (ou non) une AIPD : on les consulte sur cnil.fr.

> [!NOTE]
> Un seul critère ne dispense pas toujours de l'AIPD ; deux critères n'en font pas toujours une obligation. Le responsable de traitement **apprécie et documente** sa décision. Si l'AIPD conclut à un risque élevé qui reste **résiduel**, il doit **consulter la CNIL** avant de démarrer.

### Les quatre étapes de la méthode CNIL

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 284.60 440.60" style="max-width:380px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 429.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M216,-419C216,-419 47,-419 47,-419 41,-419 35,-413 35,-407 35,-407 35,-381 35,-381 35,-375 41,-369 47,-369 47,-369 216,-369 216,-369 222,-369 228,-375 228,-381 228,-381 228,-407 228,-407 228,-413 222,-419 216,-419"/>
<text text-anchor="start" x="81.5" y="-398" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">1. Contexte</text>
<text text-anchor="start" x="54" y="-383" font-family="Helvetica,sans-Serif" font-size="15.00">décrire le traitement</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M241.5,-311C241.5,-311 21.5,-311 21.5,-311 15.5,-311 9.5,-305 9.5,-299 9.5,-299 9.5,-258 9.5,-258 9.5,-252 15.5,-246 21.5,-246 21.5,-246 241.5,-246 241.5,-246 247.5,-246 253.5,-252 253.5,-258 253.5,-258 253.5,-299 253.5,-299 253.5,-305 247.5,-311 241.5,-311"/>
<text text-anchor="start" x="81" y="-290" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">2. Principes</text>
<text text-anchor="start" x="28.5" y="-275" font-family="Helvetica,sans-Serif" font-size="15.00">nécessité, proportionnalité,</text>
<text text-anchor="start" x="53.5" y="-260" font-family="Helvetica,sans-Serif" font-size="15.00">droits des personnes</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M131.5,-368.93C131.5,-354.9 131.5,-336.82 131.5,-320.59"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="134.65,-320.3 131.5,-311.3 128.35,-320.3 134.65,-320.3"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M251,-188C251,-188 12,-188 12,-188 6,-188 0,-182 0,-176 0,-176 0,-135 0,-135 0,-129 6,-123 12,-123 12,-123 251,-123 251,-123 257,-123 263,-129 263,-135 263,-135 263,-176 263,-176 263,-182 257,-188 251,-188"/>
<text text-anchor="start" x="87.5" y="-167" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">3. Risques</text>
<text text-anchor="start" x="19" y="-152" font-family="Helvetica,sans-Serif" font-size="15.00">accès illégitime, modification,</text>
<text text-anchor="start" x="48.5" y="-137" font-family="Helvetica,sans-Serif" font-size="15.00">disparition + mesures</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M131.5,-245.71C131.5,-230.84 131.5,-212.96 131.5,-197.13"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="134.65,-197.08 131.5,-188.08 128.35,-197.08 134.65,-197.08"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M192,-65C192,-65 71,-65 71,-65 65,-65 59,-59 59,-53 59,-53 59,-12 59,-12 59,-6 65,0 71,0 71,0 192,0 192,0 198,0 204,-6 204,-12 204,-12 204,-53 204,-53 204,-59 198,-65 192,-65"/>
<text text-anchor="start" x="78" y="-44" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">4. Validation</text>
<text text-anchor="start" x="80" y="-29" font-family="Helvetica,sans-Serif" font-size="15.00">plan d&#39;action,</text>
<text text-anchor="start" x="86" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">avis du DPO</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M131.5,-122.71C131.5,-107.84 131.5,-89.96 131.5,-74.13"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="134.65,-74.08 131.5,-65.08 128.35,-74.08 134.65,-74.08"/>
</g>
</g>
</svg>
</figure>

| Étape | Contenu |
|---|---|
| **1. Décrire** | Finalités, données, personnes, durées, destinataires, supports, sous-traitants, transferts |
| **2. Nécessité et proportionnalité** | Chaque donnée est-elle nécessaire ? Base légale, information, droits, sous-traitance, transferts |
| **3. Risques** | Trois événements redoutés : **accès illégitime**, **modification non désirée**, **disparition** des données |
| **4. Valider** | Plan d'action, risques résiduels, avis du DPO, décision du responsable |

### Coter un risque

On évalue deux dimensions, de **1 à 4** :

| Niveau | Gravité (impact sur les personnes) | Vraisemblance (facilité de survenue) |
|---|---|---|
| 1 | **Négligeable** : désagréments mineurs | **Négligeable** : très difficile |
| 2 | **Limitée** : désagréments surmontables | **Limitée** : difficile |
| 3 | **Importante** : conséquences sérieuses | **Importante** : possible |
| 4 | **Maximale** : conséquences irréversibles | **Maximale** : très facile |

Le **niveau de risque** résulte du croisement des deux. Une simple multiplication (de 1 à 16) est une aide : on classe par exemple **1 à 4 faible, 5 à 8 moyen, 9 à 12 élevé, 13 à 16 très élevé**. Puis on propose des **mesures**, et on recalcule le **risque résiduel**.

| Mesure | Agit sur |
|---|---|
| Chiffrement, pseudonymisation, droits minimaux, MFA | La **vraisemblance** d'un accès illégitime |
| Sauvegardes, journalisation, alertes | La **détection** et la **reprise** |
| Réduction des données, durées courtes | La **gravité** (moins à perdre) |

## II. L'identité numérique de l'organisation

### Définition

L'**identité numérique** d'une organisation est l'ensemble de ce qui la représente en ligne : **nom de domaine**, **site web**, **comptes sur les réseaux sociaux**, **adresses courriel**, **certificats**, avis publiés, et traces laissées par ses salariés. Elle repose sur la **confiance** : clients et partenaires doivent pouvoir vérifier qu'ils parlent à la vraie organisation.

### Menaces

| Menace | Description | Exemple |
|---|---|---|
| **Usurpation** de nom de domaine (*typosquatting*) | Enregistrement d'un nom très proche | `atelier-lumiere.example` contre `atelier-Iumiere.example` (un « I » majuscule à la place du « l ») |
| **Usurpation d'expéditeur** (*spoofing*) | Envoyer des courriels en se faisant passer pour l'organisation | Faux courriel de la direction demandant un virement |
| **Faux comptes** | Compte de réseau social à son nom | Faux service client qui demande des données |
| **Atteinte à la réputation** | Avis falsifiés, contenus diffamatoires | Campagne d'avis négatifs |
| **Détournement de site** | Prise de contrôle d'un site ou d'un compte | Défiguration (*defacement*) |

### Se protéger

- **Domaine** : verrou de transfert chez le bureau d'enregistrement, renouvellement suivi, **MFA** sur le compte de gestion ; enregistrer les variantes importantes.
- **Courriel** : les enregistrements **SPF**, **DKIM** et **DMARC** du domaine permettent aux destinataires de vérifier qu'un message vient bien du domaine ; ils limitent le *spoofing*.
- **Comptes** : MFA (S03), comptes « marque » certifiés par la plateforme quand elle le propose, **droits** limités sur qui publie.
- **Surveillance** : alertes sur le nom de l'organisation, veille sur les noms de domaine proches.
- **Réaction** : **preuves** (captures datées), **signalement** à la plateforme ou au bureau d'enregistrement, **demande de retrait**, **plainte** si nécessaire.

### Droit à l'image et vie privée

Publier la photo d'une personne reconnaissable (salarié, client) nécessite son **accord** (droit à l'image et protection de la vie privée), qui doit être précis (usage, durée). L'image est aussi une donnée personnelle (RGPD, S07).

## III. La preuve électronique

En cas de litige, il faut pouvoir **prouver**. Le Code civil (articles 1366 et 1367) reconnaît à l'**écrit électronique** la même force probante que le papier, à deux conditions : on peut **identifier** la personne dont il émane, et il est établi et **conservé** de façon à garantir son **intégrité**. La **signature électronique** manifeste le consentement d'un signataire.

Le règlement européen **eIDAS** distingue trois niveaux de signature : **simple**, **avancée** et **qualifiée** (la plus forte, assimilée par la loi à une signature manuscrite).

| Pour qu'une trace serve de preuve | Moyen |
|---|---|
| Identifier l'auteur | Authentification forte, certificat, signature |
| Garantir l'intégrité | **Hachage** de fichier (S10), journaux protégés, horodatage |
| Conserver | Archivage sécurisé, chaîne de conservation |
| Dater | Horodatage, **synchronisation NTP** des serveurs |

> [!NOTE]
> Une simple capture d'écran se conteste facilement. Pour un litige sérieux, on fait établir un **constat** par un commissaire de justice (anciennement huissier), et on conserve les journaux **sans les modifier** (S17).

## IV. Infractions informatiques et responsabilité

Le Code pénal (articles 323-1 et suivants, « atteintes aux systèmes de traitement automatisé de données ») punit notamment :

| Texte | Infraction | Exemple |
|---|---|---|
| **323-1** | **Accès ou maintien frauduleux** dans un système | Se connecter avec le mot de passe d'un collègue ; garder un accès après son départ |
| **323-2** | **Entrave** ou altération du fonctionnement | Déni de service, rançongiciel |
| **323-3** | **Introduction, extraction, modification ou suppression** frauduleuse de données | Copier une base clients |
| **323-3-1** | **Détention ou mise à disposition** d'outils conçus pour commettre ces infractions, sans motif légitime | Diffuser un outil d'attaque |
| **226-4-1** | **Usurpation d'identité**, y compris numérique | Faux profil à un nom réel |
| **226-16 et suivants** | Manquements aux règles sur les données personnelles | Traitement sans respecter la loi |

> [!WARNING]
> Les peines vont de plusieurs années d'emprisonnement à plusieurs dizaines de milliers d'euros d'amende, selon l'infraction et les circonstances : **consulte Légifrance** pour le texte à jour. Le mot clé est **frauduleux** : sans autorisation, il y a infraction, même si l'on n'a rien cassé.

### Responsabilité de l'administrateur

L'administrateur a des **pouvoirs étendus** (accès aux fichiers, aux journaux, aux messageries) et des **devoirs** :

- **Agir dans le cadre de sa mission** : un test d'intrusion ou un scan de vulnérabilités sans **autorisation écrite** peut être une infraction (voir S16) ;
- **Secret professionnel** et confidentialité sur ce qu'il voit ; pas d'ouverture de fichiers identifiés comme **personnels** par le salarié, sauf risque ou événement particulier, et en principe en sa présence ;
- **Loyauté** vis-à-vis de l'employeur et des utilisateurs : informer sur les journaux conservés et les contrôles (charte) ;
- **Alerter** la hiérarchie et le DPO en cas de violation, sans attendre.

### La charte informatique

La **charte d'utilisation du système d'information** fixe les règles : usages autorisés (professionnel et privé), mots de passe, matériel personnel, messagerie, journalisation, sanctions. Elle est **annexée au règlement intérieur** pour être opposable aux salariés, et ses règles de surveillance doivent respecter le principe de **transparence**. Elle protège aussi l'administrateur : ce qu'il fait est connu et encadré.

### Les organismes utiles

| Organisme | Rôle |
|---|---|
| **ANSSI** | Autorité nationale de la sécurité des systèmes d'information : guides, certifications, alertes (CERT-FR) |
| **CNIL** | Autorité de protection des données personnelles : conseils, contrôles, sanctions, notification des violations |
| **Cybermalveillance.gouv.fr** | Assistance aux victimes (particuliers, entreprises, collectivités) et prévention |
| **Plateformes de signalement** (Pharos pour les contenus illicites, Thésée pour les escroqueries en ligne) | Dépôt de signalements ou de plaintes |
| Police, gendarmerie | Dépôt de plainte |

## À retenir

- AIPD : **avant** le traitement, si **deux critères** ou plus ; méthode en **quatre étapes** ; risque = **vraisemblance × gravité**.
- L'identité numérique d'une organisation (domaine, courriel, comptes) se **protège** (verrou, SPF/DKIM/DMARC, MFA) et se **défend** (preuves, signalement, plainte).
- Un écrit électronique vaut preuve s'il identifie son auteur et garantit son **intégrité**.
- **Sans autorisation**, accéder à un système ou en modifier les données est une **infraction** (323-1 et suivants).
- L'administrateur agit dans le cadre de sa mission, respecte la **confidentialité** et s'appuie sur la **charte**.
