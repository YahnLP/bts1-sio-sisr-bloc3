# Cours – Collecte, base légale, consentement et droits des personnes

*BTS SIO SISR 1re année – Bloc 3 – S07 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S06 (notions, principes, registre).
> - **Matériel :** VM Debian de laboratoire (paquet `sqlite3`) ; navigateur web avec outils de développement

## À la fin de ce cours tu sauras

- [ ] **Choisir** une base légale adaptée à un traitement (les six bases de l'article 6) ;
- [ ] **Reconnaître** un consentement valide (libre, spécifique, éclairé, univoque) et un consentement non conforme ;
- [ ] **Rédiger** les mentions d'information d'un formulaire de collecte ;
- [ ] **Analyser** le comportement d'un site vis-à-vis des cookies et traceurs ;
- [ ] **Citer** les droits des personnes et les délais de réponse ;
- [ ] **Traiter** techniquement une demande d'accès et une demande d'effacement sur une base de données.

## I. Sur quel fondement collecter ?

Le principe de **licéité** (S06) impose que chaque traitement repose sur une **base légale** (article 6). Il y en a six ; le **consentement** n'est qu'une d'entre elles.

| Base légale | Quand | Exemple |
|---|---|---|
| **Consentement** | La personne accepte, pour une finalité précise | Newsletter promotionnelle, cookies publicitaires |
| **Contrat** | Le traitement est nécessaire à l'exécution d'un contrat ou à des mesures précontractuelles | Adresse de livraison d'une commande |
| **Obligation légale** | La loi impose le traitement | Conservation des factures, déclarations sociales |
| **Intérêts vitaux** | Protéger la vie d'une personne | Urgence médicale |
| **Mission d'intérêt public** | Autorité publique | Traitement d'un service public |
| **Intérêt légitime** | Intérêt de l'organisation, à condition que les droits des personnes ne priment pas | Sécurité du réseau, prévention de la fraude |

> [!NOTE]
> On choisit la base légale **avant** de collecter et on la **documente** dans le registre. Changer de base légale après coup parce qu'on s'est trompé n'est pas permis. Un même traitement n'a pas à additionner les bases : on choisit **la plus adaptée**.

**Je vérifie.** Une entreprise de livraison collecte l'adresse du client pour livrer. Faut-il recueillir son consentement ?

<details markdown="1">
<summary>Voir la réponse</summary>

Non : la base légale est le **contrat** (livrer la commande suppose de connaître l'adresse). Demander un consentement serait même **trompeur** : le client pourrait le retirer, et la livraison deviendrait impossible. Un **consentement** serait en revanche nécessaire pour utiliser cette adresse à des fins de **démarchage commercial** d'un autre type.

</details>

## II. Le consentement valide

Quand le consentement est la base légale, il doit être (articles 4 et 7) :

| Caractère | Signification | Contre-exemple |
|---|---|---|
| **Libre** | Sans contrainte, sans conditionner un service qui n'en a pas besoin | « Accepte tout ou pas d'accès » |
| **Spécifique** | Une finalité par consentement | Une seule case pour la newsletter **et** le partage avec des partenaires |
| **Éclairé** | La personne sait qui, quoi, pourquoi | Texte juridique illisible |
| **Univoque** | Un acte positif **clair** | **Case pré-cochée**, silence, poursuite de la navigation |

En plus :

- le responsable doit pouvoir **prouver** le consentement (qui, quand, à quel texte) ;
- le **retrait** doit être **aussi simple** que le consentement ;
- en France, un mineur de **moins de 15 ans** ne peut consentir seul à certains services en ligne : l'accord d'un titulaire de l'autorité parentale est nécessaire.

## III. Informer les personnes

À la collecte, la personne doit être informée (articles 13 et 14), **de façon concise, claire et accessible** :

- l'**identité** du responsable et les coordonnées du DPO s'il y en a un ;
- les **finalités** et la **base légale** ;
- les **destinataires** et les éventuels transferts hors Union européenne ;
- la **durée de conservation** ;
- les **droits** (accès, rectification, effacement…), le droit de **retirer** le consentement, le droit de **saisir la CNIL**.

Une présentation **à deux niveaux** est courante : une mention courte sous le formulaire, avec un lien vers la politique de confidentialité complète.

La protection des données **dès la conception** et **par défaut** (article 25) demande de prévoir ces éléments **dans l'architecture** : ne collecter que le nécessaire, régler par défaut les options les plus protectrices.

## IV. Cookies et traceurs

Un **traceur** (cookie, identifiant publicitaire, pixel) lit ou écrit des informations sur le terminal de l'utilisateur. La règle française (loi Informatique et Libertés, article 82, reprise de la directive ePrivacy) est :

| Type de traceur | Consentement préalable ? |
|---|---|
| **Strictement nécessaire** au service demandé (panier, authentification, sécurité, équilibrage de charge) | **Non** |
| Mesure d'audience **limitée** à des statistiques anonymes, selon des conditions précises de la CNIL | Non, sous conditions |
| **Publicité ciblée**, réseaux sociaux, suivi inter-sites | **Oui** |

Selon les lignes directrices de la CNIL : **refuser doit être aussi simple qu'accepter** (un bouton de refus au même niveau que le bouton d'acceptation), les traceurs soumis au consentement **ne sont pas déposés avant** le choix, et le choix de l'utilisateur est conservé pour une durée limitée (la CNIL recommande de le lui redemander après environ **six mois**). Ces points sont à relire sur le site de la CNIL.

**Je vérifie.** Un site affiche « En poursuivant votre navigation, vous acceptez les cookies ». Est-ce conforme ?

<details markdown="1">
<summary>Voir la réponse</summary>

**Non** : la poursuite de la navigation n'est pas un acte positif **clair** ; le consentement doit être explicite, avec un choix réel (accepter ou refuser) avant le dépôt de traceurs non essentiels.

</details>

## V. Les droits des personnes

| Droit | Contenu | Article |
|---|---|---|
| **Information** | Savoir comment les données sont traitées | 13, 14 |
| **Accès** | Obtenir **copie** de ses données et des informations sur le traitement | 15 |
| **Rectification** | Corriger des données inexactes | 16 |
| **Effacement** (« droit à l'oubli ») | Faire supprimer ses données dans certains cas | 17 |
| **Limitation** | Geler le traitement pendant une vérification | 18 |
| **Portabilité** | Récupérer ses données dans un format structuré, courant et lisible par une machine, ou les faire transmettre à un autre responsable | 20 |
| **Opposition** | S'opposer à un traitement (toujours pour la prospection) | 21 |
| **Décision automatisée** | Ne pas être soumis à une décision fondée uniquement sur un traitement automatisé produisant des effets importants | 22 |

**Délai :** le responsable répond **dans un mois** à compter de la réception de la demande ; ce délai peut être prolongé de **deux mois** si la demande est complexe ou nombreuses, à condition d'en informer la personne dans le premier mois. L'exercice des droits est **gratuit**, sauf demandes manifestement infondées ou excessives.

Le droit à l'**effacement** n'est pas absolu : on ne supprime pas ce qu'une **obligation légale** impose de conserver (par exemple des pièces comptables) ; on **limite** alors l'accès et on **supprime le reste**.

### Le rôle du technicien dans une demande d'accès

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 276.60 631.60" style="max-width:369px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 620.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M190.5,-610C190.5,-610 64.5,-610 64.5,-610 58.5,-610 52.5,-604 52.5,-598 52.5,-598 52.5,-568 52.5,-568 52.5,-562 58.5,-556 64.5,-556 64.5,-556 190.5,-556 190.5,-556 196.5,-556 202.5,-562 202.5,-568 202.5,-568 202.5,-598 202.5,-598 202.5,-604 196.5,-610 190.5,-610"/>
<text text-anchor="start" x="89.5" y="-588" font-family="Helvetica,sans-Serif" font-size="15.00">Réception</text>
<text text-anchor="start" x="71.5" y="-571" font-family="Helvetica,sans-Serif" font-size="15.00">de la demande</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M168,-498C168,-498 87,-498 87,-498 81,-498 75,-492 75,-486 75,-486 75,-456 75,-456 75,-450 81,-444 87,-444 87,-444 168,-444 168,-444 174,-444 180,-450 180,-456 180,-456 180,-486 180,-486 180,-492 174,-498 168,-498"/>
<text text-anchor="start" x="100.5" y="-476" font-family="Helvetica,sans-Serif" font-size="15.00">Vérifier</text>
<text text-anchor="start" x="94" y="-459" font-family="Helvetica,sans-Serif" font-size="15.00">l&#39;identité</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M127.5,-555.93C127.5,-541.52 127.5,-523.39 127.5,-507.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="130.65,-507.26 127.5,-498.26 124.35,-507.26 130.65,-507.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M201,-386C201,-386 54,-386 54,-386 48,-386 42,-380 42,-374 42,-374 42,-344 42,-344 42,-338 48,-332 54,-332 54,-332 201,-332 201,-332 207,-332 213,-338 213,-344 213,-344 213,-374 213,-374 213,-380 207,-386 201,-386"/>
<text text-anchor="start" x="64.5" y="-364" font-family="Helvetica,sans-Serif" font-size="15.00">Rechercher dans</text>
<text text-anchor="start" x="61" y="-347" font-family="Helvetica,sans-Serif" font-size="15.00">tous les systèmes</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M127.5,-443.93C127.5,-429.52 127.5,-411.39 127.5,-395.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="130.65,-395.26 127.5,-386.26 124.35,-395.26 130.65,-395.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M237,-274C237,-274 18,-274 18,-274 12,-274 6,-268 6,-262 6,-262 6,-236 6,-236 6,-230 12,-224 18,-224 18,-224 237,-224 237,-224 243,-224 249,-230 249,-236 249,-236 249,-262 249,-262 249,-268 243,-274 237,-274"/>
<text text-anchor="start" x="44" y="-253" font-family="Helvetica,sans-Serif" font-size="15.00">Extraire </text>
<text text-anchor="start" x="108" y="-253" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">uniquement</text>
<text text-anchor="start" x="25" y="-238" font-family="Helvetica,sans-Serif" font-size="15.00">les données du demandeur</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M127.5,-331.86C127.5,-317.28 127.5,-298.97 127.5,-283.36"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="130.65,-283.06 127.5,-274.06 124.35,-283.06 130.65,-283.06"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M243,-166C243,-166 12,-166 12,-166 6,-166 0,-160 0,-154 0,-154 0,-124 0,-124 0,-118 6,-112 12,-112 12,-112 243,-112 243,-112 249,-112 255,-118 255,-124 255,-124 255,-154 255,-154 255,-160 249,-166 243,-166"/>
<text text-anchor="start" x="19" y="-144" font-family="Helvetica,sans-Serif" font-size="15.00">Répondre de façon sécurisée</text>
<text text-anchor="start" x="79.5" y="-127" font-family="Helvetica,sans-Serif" font-size="15.00">dans le délai</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M127.5,-223.76C127.5,-209.41 127.5,-190.99 127.5,-175.07"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="130.65,-175.04 127.5,-166.04 124.35,-175.04 130.65,-175.04"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M204,-54C204,-54 51,-54 51,-54 45,-54 39,-48 39,-42 39,-42 39,-12 39,-12 39,-6 45,0 51,0 51,0 204,0 204,0 210,0 216,-6 216,-12 216,-12 216,-42 216,-42 216,-48 210,-54 204,-54"/>
<text text-anchor="start" x="58" y="-32" font-family="Helvetica,sans-Serif" font-size="15.00">Tracer la demande</text>
<text text-anchor="start" x="78.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">et la réponse</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M127.5,-111.93C127.5,-97.52 127.5,-79.39 127.5,-63.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="130.65,-63.26 127.5,-54.26 124.35,-63.26 130.65,-63.26"/>
</g>
</g>
</svg>
</figure>

Trois pièges : **ne pas vérifier l'identité** (on risque de livrer des données à un tiers), **oublier un système** (sauvegardes, messagerie, fichiers en vrac : d'où le registre de S06), **divulguer les données d'autres personnes** dans l'export.

## À retenir

- Six **bases légales** (article 6) : on choisit **avant** de collecter et on la documente.
- **Consentement valide** = libre, spécifique, éclairé, **univoque** ; pas de case pré-cochée ; retrait aussi simple.
- L'**information** à la collecte est obligatoire (identité, finalité, base légale, durée, droits, CNIL).
- Cookies : consentement préalable sauf **strictement nécessaires** ; **refuser aussi simple qu'accepter**.
- Droits : accès, rectification, effacement, limitation, portabilité, opposition, décision automatisée ; réponse **sous un mois**.
- L'effacement cède devant une **obligation légale de conservation**.
