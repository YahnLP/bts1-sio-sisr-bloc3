# Cours – Conservation, sécurité du traitement, sous-traitance et violations de données

*BTS SIO SISR 1re année – Bloc 3 – S08 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S06 (principes, registre) et S07 (droits, effacement).
> - **Matériel :** VM Debian de laboratoire (paquets `sqlite3`, `cron`) ; éditeur de texte

## À la fin de ce cours tu sauras

- [ ] **Définir** une durée de conservation et les trois phases de vie d'une donnée (base active, archive, suppression) ;
- [ ] **Écrire** une purge automatique d'une base de données et d'un dossier de journaux ;
- [ ] **Distinguer** pseudonymisation et anonymisation ;
- [ ] **Citer** les mesures de sécurité de l'article 32 et les mentions d'un contrat de sous-traitance (article 28) ;
- [ ] **Qualifier** une violation de données et **préparer** la notification à la CNIL dans le délai de 72 heures.

## I. Combien de temps conserver ?

Le principe de **limitation de la conservation** (article 5) impose de ne garder les données **que le temps nécessaire** à la finalité. Il n'existe pas de durée universelle : on la **fixe**, on la **justifie** et on l'écrit dans le registre (S06).

### Les trois phases de vie d'une donnée

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 245.60 345.60" style="max-width:328px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 334.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M196.5,-324C196.5,-324 27.5,-324 27.5,-324 21.5,-324 15.5,-318 15.5,-312 15.5,-312 15.5,-271 15.5,-271 15.5,-265 21.5,-259 27.5,-259 27.5,-259 196.5,-259 196.5,-259 202.5,-259 208.5,-265 208.5,-271 208.5,-271 208.5,-312 208.5,-312 208.5,-318 202.5,-324 196.5,-324"/>
<text text-anchor="start" x="63" y="-303" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Base active</text>
<text text-anchor="start" x="34.5" y="-288" font-family="Helvetica,sans-Serif" font-size="15.00">utilisée au quotidien</text>
<text text-anchor="start" x="69.5" y="-273" font-family="Helvetica,sans-Serif" font-size="15.00">accès large</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M212,-187C212,-187 12,-187 12,-187 6,-187 0,-181 0,-175 0,-175 0,-134 0,-134 0,-128 6,-122 12,-122 12,-122 212,-122 212,-122 218,-122 224,-128 224,-134 224,-134 224,-175 224,-175 224,-181 218,-187 212,-187"/>
<text text-anchor="start" x="19" y="-166" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Archive intermédiaire</text>
<text text-anchor="start" x="25" y="-151" font-family="Helvetica,sans-Serif" font-size="15.00">obligation légale, litige</text>
<text text-anchor="start" x="56.5" y="-136" font-family="Helvetica,sans-Serif" font-size="15.00">accès restreint</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M112,-258.85C112,-240.28 112,-216.61 112,-196.61"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="115.15,-196.42 112,-187.42 108.85,-196.42 115.15,-196.42"/>
<text text-anchor="start" x="112" y="-219.6" font-family="Helvetica,sans-Serif" font-size="13.00">fin de la finalité</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M186.5,-50C186.5,-50 37.5,-50 37.5,-50 31.5,-50 25.5,-44 25.5,-38 25.5,-38 25.5,-12 25.5,-12 25.5,-6 31.5,0 37.5,0 37.5,0 186.5,0 186.5,0 192.5,0 198.5,-6 198.5,-12 198.5,-12 198.5,-38 198.5,-38 198.5,-44 192.5,-50 186.5,-50"/>
<text text-anchor="start" x="59.5" y="-29" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Suppression</text>
<text text-anchor="start" x="44.5" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">ou anonymisation</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M112,-121.98C112,-102.97 112,-78.77 112,-59.42"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="115.15,-59.36 112,-50.36 108.85,-59.36 115.15,-59.36"/>
<text text-anchor="start" x="112" y="-82.6" font-family="Helvetica,sans-Serif" font-size="13.00">fin du délai légal</text>
</g>
</g>
</svg>
</figure>

| Phase | Ce qui la justifie | Qui y accède |
|---|---|---|
| **Base active** | La finalité est en cours (la relation commerciale, le contrat de travail) | Les équipes opérationnelles |
| **Archive intermédiaire** | Une **obligation légale** ou un risque de litige (pièces comptables, prescription) | Un petit nombre de personnes, **sur demande** |
| **Suppression** | Plus aucune justification | Personne |

### Ordres de grandeur

> [!WARNING]
> Ces durées sont **indicatives** et **évoluent** : on les confirme auprès du service juridique ou sur les sites officiels (CNIL, Légifrance) avant de les appliquer. Ce ne sont pas des consignes à recopier.

| Donnée | Durée usuellement retenue |
|---|---|
| Pièces comptables (factures) | **10 ans** (Code de commerce) |
| Bulletins de paie (double conservé par l'employeur) | **5 ans** en pratique, avec des obligations de conservation plus longues pour d'autres documents sociaux |
| Candidature non retenue | **2 ans** au plus après le dernier contact (recommandation CNIL, avec l'accord du candidat au-delà) |
| Prospect (prospection commerciale) | **3 ans** à compter du dernier contact (recommandation CNIL) |
| Enregistrement de vidéosurveillance | **un mois** au plus en pratique (recommandation CNIL) |
| Journaux de connexion (hébergeurs et fournisseurs d'accès) | **1 an** (obligation légale) |

### Pseudonymisation et anonymisation

| | **Pseudonymisation** | **Anonymisation** |
|---|---|---|
| Principe | Remplacer l'identité par un **pseudonyme** (un code, un hachage salé) | Rendre la ré-identification **impossible** |
| La donnée reste-t-elle personnelle ? | **Oui** (on peut ré-identifier avec une information supplémentaire conservée à part) | **Non**, si l'anonymisation est irréversible |
| Le RGPD s'applique-t-il ? | Oui, avec une mesure de **sécurité** appréciée | Non, une fois anonyme |
| Exemple | `client_4821` à la place de « Camille Roux » | Statistiques agrégées sans aucune donnée individuelle |

> [!NOTE]
> Attention : **hacher** une adresse courriel avec SHA-256 ne l'anonymise pas. Il suffit de calculer les empreintes de millions d'adresses plausibles pour retrouver la bonne. Le **sel secret** et la clé conservée à part rendent l'opération beaucoup plus sûre, sans la rendre irréversible.

### Mettre en œuvre la conservation

Sans automatisation, les durées restent des vœux. Un technicien met en place :

- une **purge planifiée** des bases (requête SQL lancée par **cron**, tâche planifiée sous Windows) ;
- la **rotation des journaux** (`logrotate`) avec une durée maximale ;
- la **purge des sauvegardes** : une donnée supprimée de la base disparaît des sauvegardes à l'expiration de leur rétention (voir S05) ;
- une **trace** de ce qui a été purgé (date, nombre de lignes, jamais le contenu).

## II. Sécuriser le traitement : l'article 32

L'article 32 demande des mesures techniques et organisationnelles **adaptées au risque**. Il cite en particulier :

| Mesure | Exemple | Séance |
|---|---|---|
| **Pseudonymisation** et **chiffrement** | Disque chiffré, base chiffrée, TLS | S05, S10 |
| **Confidentialité, intégrité, disponibilité, résilience** | Droits minimaux, sauvegardes, redondance | S04, S05 |
| **Rétablir** l'accès aux données dans un délai approprié | Plan de reprise, sauvegarde testée | S05 |
| **Tester et évaluer** régulièrement l'efficacité des mesures | Audit, scan de vulnérabilités | S16 |

Il n'y a pas de liste de mesures obligatoires : c'est au responsable de traitement de **démontrer** (article 5, responsabilité) que ses choix sont adaptés.

## III. Sous-traitance : l'article 28

Un **sous-traitant** traite des données **pour le compte** du responsable : hébergeur, éditeur d'un logiciel en ligne (SaaS), prestataire de paie, entreprise de maintenance qui accède aux données. Le responsable doit choisir un sous-traitant qui offre des garanties suffisantes et conclure un **contrat** qui précise au minimum :

| Élément du contrat | Pourquoi |
|---|---|
| Objet, durée, nature et finalité du traitement | Cadrer le périmètre |
| Types de données et catégories de personnes | Savoir ce qui est confié |
| Traitement **uniquement sur instruction** documentée du responsable | Le sous-traitant ne détourne pas les données |
| Engagement de **confidentialité** du personnel | Protéger les données |
| **Mesures de sécurité** (article 32) | Niveau de protection attendu |
| Recours à un **autre sous-traitant** (sous-traitance en cascade) avec autorisation | Maîtriser la chaîne |
| **Aide** du sous-traitant pour les droits des personnes et les violations | Répondre dans les délais |
| **Sort des données** en fin de contrat (suppression ou restitution) | Pas de copie résiduelle |
| Droit d'**audit** par le responsable | Contrôler |

En tant que technicien ou administrateur, tu es souvent la personne qui **donne un accès** à un prestataire : vérifie qu'un contrat existe et que l'accès est **limité et tracé** (S04).

## IV. Les violations de données : articles 33 et 34

### Définition

Une **violation de données à caractère personnel** est une atteinte à la **sécurité** qui entraîne, de manière accidentelle ou illicite, la **destruction**, la **perte**, l'**altération**, la **divulgation** ou l'**accès non autorisé** à des données personnelles. Elle couvre les trois principes de la sécurité :

| Type | Principe atteint | Exemple |
|---|---|---|
| Violation de **confidentialité** | Confidentialité | Fichier clients envoyé au mauvais destinataire, base copiée par un attaquant |
| Violation d'**intégrité** | Intégrité | Données modifiées par un attaquant |
| Violation de **disponibilité** | Disponibilité | Rançongiciel qui chiffre le fichier clients sans sauvegarde |

### Que faire ?

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 663.60 845.60" style="max-width:885px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 834.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M380.5,-824C380.5,-824 99.5,-824 99.5,-824 93.5,-824 87.5,-818 87.5,-812 87.5,-812 87.5,-782 87.5,-782 87.5,-776 93.5,-770 99.5,-770 99.5,-770 380.5,-770 380.5,-770 386.5,-770 392.5,-776 392.5,-782 392.5,-782 392.5,-812 392.5,-812 392.5,-818 386.5,-824 380.5,-824"/>
<text text-anchor="start" x="159" y="-802" font-family="Helvetica,sans-Serif" font-size="15.00">Constat d&#39;un incident</text>
<text text-anchor="start" x="106.5" y="-785" font-family="Helvetica,sans-Serif" font-size="15.00">touchant des données personnelles</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M337.5,-711C337.5,-711 142.5,-711 142.5,-711 136.5,-711 130.5,-705 130.5,-699 130.5,-699 130.5,-669 130.5,-669 130.5,-663 136.5,-657 142.5,-657 142.5,-657 337.5,-657 337.5,-657 343.5,-657 349.5,-663 349.5,-669 349.5,-669 349.5,-699 349.5,-699 349.5,-705 343.5,-711 337.5,-711"/>
<text text-anchor="start" x="207.5" y="-689" font-family="Helvetica,sans-Serif" font-size="15.00">Contenir</text>
<text text-anchor="start" x="149.5" y="-672" font-family="Helvetica,sans-Serif" font-size="15.00">et préserver les preuves</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M240,-769.98C240,-755.19 240,-736.48 240,-720.37"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="243.15,-720.25 240,-711.25 236.85,-720.25 243.15,-720.25"/>
</g>
<g class="node n&#45;diamond">
<polygon fill="none" stroke="black" stroke-width="1.8" points="240,-598 0,-544 240,-490 480,-544 240,-598"/>
<text text-anchor="start" x="158.5" y="-549" font-family="Helvetica,sans-Serif" font-size="15.00">Risque pour les droits</text>
<text text-anchor="start" x="139" y="-532" font-family="Helvetica,sans-Serif" font-size="15.00">et libertés des personnes ?</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M240,-656.72C240,-642.6 240,-624.55 240,-607.09"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="243.15,-607.04 240,-598.04 236.85,-607.04 243.15,-607.04"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M422,-54C422,-54 194,-54 194,-54 188,-54 182,-48 182,-42 182,-42 182,-12 182,-12 182,-6 188,0 194,0 194,0 422,0 422,0 428,0 434,-6 434,-12 434,-12 434,-42 434,-42 434,-48 428,-54 422,-54"/>
<text text-anchor="start" x="201" y="-32" font-family="Helvetica,sans-Serif" font-size="15.00">Documenter dans le registre</text>
<text text-anchor="start" x="256" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">des violations</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M223.4,-493.6C215.19,-464.87 207,-427.78 207,-394 207,-394 207,-394 207,-137 207,-104.95 230.79,-78.34 255.27,-59.43"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="257.17,-61.95 262.52,-54.06 253.42,-56.89 257.17,-61.95"/>
<text text-anchor="start" x="207" y="-268.6" font-family="Helvetica,sans-Serif" font-size="13.00">Aucun risque</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M492,-418C492,-418 348,-418 348,-418 342,-418 336,-412 336,-406 336,-406 336,-380 336,-380 336,-374 342,-368 348,-368 348,-368 492,-368 492,-368 498,-368 504,-374 504,-380 504,-380 504,-406 504,-406 504,-412 498,-418 492,-418"/>
<text text-anchor="start" x="355" y="-397" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Notifier la CNIL</text>
<text text-anchor="start" x="383.5" y="-382" font-family="Helvetica,sans-Serif" font-size="15.00">sous 72 h</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M290.62,-501.1C320.18,-476.63 356.8,-446.32 383.53,-424.19"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="385.86,-426.35 390.79,-418.18 381.85,-421.49 385.86,-426.35"/>
<text text-anchor="start" x="351" y="-450.6" font-family="Helvetica,sans-Serif" font-size="13.00">Risque</text>
</g>
<g class="node n&#45;diamond">
<polygon fill="none" stroke="black" stroke-width="1.8" points="488,-309 334,-272 488,-235 642,-272 488,-309"/>
<text text-anchor="start" x="430" y="-269.5" font-family="Helvetica,sans-Serif" font-size="15.00">Risque </text>
<text text-anchor="start" x="486" y="-269.5" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">élevé</text>
<text text-anchor="start" x="533" y="-269.5" font-family="Helvetica,sans-Serif" font-size="15.00"> ?</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M433.76,-367.92C442.78,-352.13 454.79,-331.12 465.21,-312.88"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="468.14,-314.1 469.87,-304.72 462.67,-310.98 468.14,-314.1"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M433.11,-247.92C397.59,-230.05 353.54,-201.77 329,-163 310.14,-133.2 306.1,-92.47 306.03,-63.57"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="309.19,-63.29 306.15,-54.25 302.89,-63.21 309.19,-63.29"/>
<text text-anchor="start" x="329" y="-134.6" font-family="Helvetica,sans-Serif" font-size="13.00">Non</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M600.5,-163C600.5,-163 387.5,-163 387.5,-163 381.5,-163 375.5,-157 375.5,-151 375.5,-151 375.5,-125 375.5,-125 375.5,-119 381.5,-113 387.5,-113 387.5,-113 600.5,-113 600.5,-113 606.5,-113 612.5,-119 612.5,-125 612.5,-125 612.5,-151 612.5,-151 612.5,-157 606.5,-163 600.5,-163"/>
<text text-anchor="start" x="394.5" y="-142" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Informer les personnes</text>
<text text-anchor="start" x="402" y="-127" font-family="Helvetica,sans-Serif" font-size="15.00">dans les meilleurs délais</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M489.62,-235.28C490.52,-215.59 491.62,-191.32 492.5,-172.07"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="495.64,-172.2 492.91,-163.07 489.35,-171.92 495.64,-172.2"/>
<text text-anchor="start" x="491" y="-195.6" font-family="Helvetica,sans-Serif" font-size="13.00">Oui</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M452.72,-112.81C425.52,-96.87 389.68,-75.86 360.46,-58.74"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="361.77,-55.86 352.41,-54.03 358.58,-61.29 361.77,-55.86"/>
</g>
</g>
</svg>
</figure>

| Obligation | Détail |
|---|---|
| **Documenter** toute violation | Dans un **registre des violations**, **même sans notification** (faits, effets, mesures) |
| **Notifier la CNIL** | Sans retard et si possible **72 heures au plus tard** après en avoir pris connaissance, **sauf** si la violation n'est pas susceptible d'engendrer un risque |
| **Informer les personnes** | Dans les meilleurs délais, si le risque est **élevé** (article 34) ; pas obligatoire si les données étaient **chiffrées** de façon efficace |
| Pour un **sous-traitant** | Prévenir le responsable de traitement **dans les meilleurs délais** |

### Contenu de la notification

La notification décrit : la **nature** de la violation (catégories et nombre approximatif de personnes et de données), les **coordonnées** du DPO ou d'un contact, les **conséquences probables**, les **mesures prises ou envisagées**. Si certaines informations manquent, on notifie quand même et on **complète ensuite**.

### Évaluer la gravité

On croise trois critères :

| Critère | Questions |
|---|---|
| **Nature des données** | Identité seule ? Santé, finances, mots de passe, pièces d'identité ? |
| **Volume et personnes** | Combien de personnes ? Des mineurs ou des personnes vulnérables ? |
| **Facilité d'exploitation** | Données lisibles ou chiffrées ? Publiques ou entre les mains d'un tiers malveillant ? |

Plus les données sont sensibles, nombreuses et lisibles, plus le risque est élevé.

## À retenir

- La conservation est **limitée**, **fixée** et **justifiée** ; elle s'automatise (purge, rotation, rétention des sauvegardes).
- **Pseudonymiser** n'est pas **anonymiser** : la donnée pseudonymisée reste personnelle.
- Un **sous-traitant** agit sur **instruction** et sous **contrat** (article 28).
- Violation de données : **contenir, documenter, évaluer, notifier la CNIL sous 72 h** si risque, **informer les personnes** si risque élevé.
- Toute violation est inscrite au **registre des violations**, même sans notification.
