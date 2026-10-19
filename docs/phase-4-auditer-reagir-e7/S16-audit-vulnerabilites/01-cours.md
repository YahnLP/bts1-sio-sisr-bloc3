# Cours – Audit de vulnérabilités : cadre, scans, CVE et CVSS

*BTS SIO SISR 1re année – Bloc 3 – S16 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S09 (infractions, autorisation), S14 (durcissement), S15 (journaux, détection).
> - **Matériel :** VM Debian `adm` (`nmap`) et VM Debian cible `srv` (`nginx`, `vsftpd`) sur un réseau interne isolé

## À la fin de ce cours tu sauras

- [ ] **Rédiger** une autorisation d'audit précisant périmètre, dates et règles ;
- [ ] **Distinguer** découverte, scan de ports, détection de services et scan de vulnérabilités ;
- [ ] **Utiliser** Nmap pour découvrir les machines, les ports ouverts et les versions de services ;
- [ ] **Interpréter** une référence CVE et un score CVSS, et **prioriser** les corrections ;
- [ ] **Rédiger** une fiche d'audit et un plan de remédiation.

## I. Pourquoi auditer ?

Un **audit de vulnérabilités** recherche les failles d'un système **avant** qu'un attaquant ne les exploite. Une **vulnérabilité** est une faiblesse (logiciel non corrigé, mauvaise configuration, mot de passe faible) qui peut être exploitée par une menace (S01).

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 332.60 747.60" style="max-width:444px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 736.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M290.5,-726C290.5,-726 103.5,-726 103.5,-726 97.5,-726 91.5,-720 91.5,-714 91.5,-714 91.5,-684 91.5,-684 91.5,-678 97.5,-672 103.5,-672 103.5,-672 290.5,-672 290.5,-672 296.5,-672 302.5,-678 302.5,-684 302.5,-684 302.5,-714 302.5,-714 302.5,-720 296.5,-726 290.5,-726"/>
<text text-anchor="start" x="162" y="-704" font-family="Helvetica,sans-Serif" font-size="15.00">1. Cadrer</text>
<text text-anchor="start" x="110.5" y="-687" font-family="Helvetica,sans-Serif" font-size="15.00">autorisation, périmètre</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M299,-614C299,-614 95,-614 95,-614 89,-614 83,-608 83,-602 83,-602 83,-572 83,-572 83,-566 89,-560 95,-560 95,-560 299,-560 299,-560 305,-560 311,-566 311,-572 311,-572 311,-602 311,-602 311,-608 305,-614 299,-614"/>
<text text-anchor="start" x="151" y="-592" font-family="Helvetica,sans-Serif" font-size="15.00">2. Découvrir</text>
<text text-anchor="start" x="102" y="-575" font-family="Helvetica,sans-Serif" font-size="15.00">machines, ports, services</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M197,-671.93C197,-657.52 197,-639.39 197,-623.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="200.15,-623.26 197,-614.26 193.85,-623.26 200.15,-623.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M207.5,-502C207.5,-502 18.5,-502 18.5,-502 12.5,-502 6.5,-496 6.5,-490 6.5,-490 6.5,-460 6.5,-460 6.5,-454 12.5,-448 18.5,-448 18.5,-448 207.5,-448 207.5,-448 213.5,-448 219.5,-454 219.5,-460 219.5,-460 219.5,-490 219.5,-490 219.5,-496 213.5,-502 207.5,-502"/>
<text text-anchor="start" x="69" y="-480" font-family="Helvetica,sans-Serif" font-size="15.00">3. Identifier</text>
<text text-anchor="start" x="25.5" y="-463" font-family="Helvetica,sans-Serif" font-size="15.00">versions, vulnérabilités</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M177.09,-559.93C165.57,-544.84 150.93,-525.67 138.56,-509.47"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="141.02,-507.5 133.06,-502.26 136.01,-511.33 141.02,-507.5"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M210,-390C210,-390 12,-390 12,-390 6,-390 0,-384 0,-378 0,-378 0,-348 0,-348 0,-342 6,-336 12,-336 12,-336 210,-336 210,-336 216,-336 222,-342 222,-348 222,-348 222,-378 222,-378 222,-384 216,-390 210,-390"/>
<text text-anchor="start" x="73" y="-368" font-family="Helvetica,sans-Serif" font-size="15.00">4. Évaluer</text>
<text text-anchor="start" x="19" y="-351" font-family="Helvetica,sans-Serif" font-size="15.00">score, exposition, valeur</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M112.53,-447.93C112.26,-433.52 111.93,-415.39 111.65,-399.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="114.79,-399.2 111.48,-390.26 108.49,-399.32 114.79,-399.2"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M173,-278C173,-278 65,-278 65,-278 59,-278 53,-272 53,-266 53,-266 53,-236 53,-236 53,-230 59,-224 65,-224 65,-224 173,-224 173,-224 179,-224 185,-230 185,-236 185,-236 185,-266 185,-266 185,-272 179,-278 173,-278"/>
<text text-anchor="start" x="72" y="-256" font-family="Helvetica,sans-Serif" font-size="15.00">5. Rapporter</text>
<text text-anchor="start" x="72" y="-239" font-family="Helvetica,sans-Serif" font-size="15.00">fiche d&#39;audit</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M112.9,-335.93C113.94,-321.52 115.26,-303.39 116.41,-287.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="119.58,-287.47 117.09,-278.26 113.3,-287.01 119.58,-287.47"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M206,-166C206,-166 40,-166 40,-166 34,-166 28,-160 28,-154 28,-154 28,-124 28,-124 28,-118 34,-112 40,-112 40,-112 206,-112 206,-112 212,-112 218,-118 218,-124 218,-124 218,-154 218,-154 218,-160 212,-166 206,-166"/>
<text text-anchor="start" x="83" y="-144" font-family="Helvetica,sans-Serif" font-size="15.00">6. Corriger</text>
<text text-anchor="start" x="47" y="-127" font-family="Helvetica,sans-Serif" font-size="15.00">plan de remédiation</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M119.95,-223.93C120.47,-209.52 121.13,-191.39 121.7,-175.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="124.87,-175.37 122.04,-166.26 118.57,-175.14 124.87,-175.37"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M260.5,-54C260.5,-54 141.5,-54 141.5,-54 135.5,-54 129.5,-48 129.5,-42 129.5,-42 129.5,-12 129.5,-12 129.5,-6 135.5,0 141.5,0 141.5,0 260.5,0 260.5,0 266.5,0 272.5,-6 272.5,-12 272.5,-12 272.5,-42 272.5,-42 272.5,-48 266.5,-54 260.5,-54"/>
<text text-anchor="start" x="164.5" y="-32" font-family="Helvetica,sans-Serif" font-size="15.00">7. Vérifier</text>
<text text-anchor="start" x="148.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">nouveau scan</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M141.48,-111.93C152.09,-96.97 165.53,-78.02 176.95,-61.91"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="179.74,-63.43 182.38,-54.26 174.6,-59.78 179.74,-63.43"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M217.59,-54.18C241.55,-94.56 283,-175.22 283,-250 283,-364 283,-364 283,-364 283,-434.67 244.64,-509.97 219.16,-552.19"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="216.43,-550.61 214.4,-559.93 221.8,-553.91 216.43,-550.61"/>
</g>
</g>
</svg>
</figure>

L'audit est **récurrent** : de nouvelles vulnérabilités sont publiées chaque jour. Un scan régulier fait partie de la gestion du parc (S02, S14).

## II. Le cadre légal : l'autorisation

> [!WARNING]
> **Scanner un système sans autorisation peut constituer une infraction** (accès ou tentative d'accès frauduleux, entrave : S09, articles 323-1 et suivants du Code pénal). Le but, « m'entraîner » ou « aider », n'efface pas l'infraction. **Toujours** une **autorisation écrite** du propriétaire du système.

Elle précise au minimum :

| Élément | Exemple |
|---|---|
| **Qui autorise** | Représentant légal ou responsable désigné |
| **Qui réalise** | Nom de l'auditeur ou du prestataire |
| **Périmètre** | Plages d'adresses, noms de domaine, systèmes **inclus** et **exclus** |
| **Période** | Dates et plages horaires |
| **Méthodes** | Scan de ports et de vulnérabilités ; pas d'exploitation, pas de déni de service |
| **Contacts d'urgence** | Qui prévenir en cas d'incident pendant le test |
| **Confidentialité** | Traitement du rapport et des données rencontrées |
| **Livrable** | Rapport, restitution |

Un audit chez un **tiers** (client, hébergeur) exige l'accord de **ce tiers** : le consentement du client ne suffit pas pour scanner l'infrastructure de son hébergeur.

## III. Types d'approche

| Approche | L'auditeur dispose de… | Avantage |
|---|---|---|
| **Boîte noire** | Rien (il se place en attaquant externe) | Vue réaliste de l'extérieur |
| **Boîte grise** | Quelques informations (un compte, un schéma) | Compromis pertinence/temps |
| **Boîte blanche** | Toutes les informations (configurations, code) | Exhaustif |

On distingue aussi :

| | **Scan non authentifié** | **Scan authentifié** |
|---|---|---|
| Principe | Vue extérieure : ports, bannières | Se connecte avec un compte pour lire les versions et la configuration |
| Résultat | Moins précis, moins de faux positifs d'accès | Plus complet |

Un **scan de vulnérabilités** (outil automatisé) n'est pas un **test d'intrusion** (un humain tente de les exploiter pour mesurer l'impact) : le premier **liste**, le second **démontre**.

## IV. Les étapes d'un scan avec Nmap

**Nmap** est l'outil de référence pour explorer un réseau.

| Étape | Question | Commande |
|---|---|---|
| **Découverte** | Quelles machines répondent ? | `nmap -sn 192.168.56.0/24` |
| **Ports** | Quels ports sont ouverts ? | `nmap -sS -p- 192.168.56.10` |
| **Services et versions** | Quel logiciel, quelle version ? | `nmap -sV -p 21,22,80,443 192.168.56.10` |
| **Système** | Quel système d'exploitation ? | `nmap -O 192.168.56.10` |
| **Scripts** | Un contrôle précis (accès anonyme, chiffrement) | `nmap --script ftp-anon -p 21 192.168.56.10` |
| **Sauvegarde** | Conserver la preuve | `-oN scan.txt` (texte) ou `-oX scan.xml` |

### Les états d'un port

| État | Sens |
|---|---|
| **open** | Un service écoute et répond |
| **closed** | Accessible, mais aucun service n'écoute |
| **filtered** | Un pare-feu filtre : pas de réponse exploitable |

> [!NOTE]
> Un scan **bruyant** laisse des traces dans les journaux et déclenche des alertes (S15) : c'est normal et utile pour tester la détection. Prévenir l'équipe de supervision avant un scan en production.

## V. CVE et CVSS

### CVE

Une **CVE** (*Common Vulnerabilities and Exposures*) est un identifiant unique de vulnérabilité connue, au format `CVE-ANNÉE-NUMÉRO` (par exemple `CVE-2017-0144`). On y associe le logiciel concerné, les versions touchées, et une description. Les fiches sont consultables sur la base **NVD** (*National Vulnerability Database*) et sur les bulletins des éditeurs et du **CERT-FR**.

### CVSS

Le **CVSS** (*Common Vulnerability Scoring System*) note la **gravité technique** d'une vulnérabilité de 0 à 10.

| Score | Gravité |
|---|---|
| 0,0 | Aucune |
| 0,1 à 3,9 | **Faible** |
| 4,0 à 6,9 | **Moyenne** |
| 7,0 à 8,9 | **Élevée** |
| 9,0 à 10,0 | **Critique** |

Le score dépend de critères comme le **vecteur d'attaque** (réseau ou local), la **complexité**, les **privilèges requis**, l'**interaction de l'utilisateur** et l'impact sur la confidentialité, l'intégrité et la disponibilité.

### Prioriser : le score ne suffit pas

On croise le score avec le **contexte** :

| Critère | Questions |
|---|---|
| **Exposition** | La machine est-elle accessible depuis Internet ? depuis le LAN seulement ? |
| **Exploitabilité** | Existe-t-il un code d'exploitation public ? La vulnérabilité est-elle **activement exploitée** (catalogues des vulnérabilités exploitées) ? |
| **Valeur du bien** | Données personnelles, serveur critique, poste de test ? |
| **Facilité de correction** | Correctif disponible ? Arrêt nécessaire ? Mesure de contournement ? |

Une vulnérabilité « moyenne » sur un serveur exposé et critique peut passer **avant** une « élevée » sur un poste isolé.

## VI. Le rapport d'audit

Une **fiche d'audit** doit être lisible par la direction **et** exploitable par les techniciens :

| Rubrique | Contenu |
|---|---|
| **Cadre** | Périmètre, dates, méthode, outils et versions |
| **Synthèse** | Résultat global en quelques lignes, nombre de vulnérabilités par gravité |
| **Constats** | Pour chacun : machine, port, service, vulnérabilité (CVE), score, **preuve** (extrait du scan) |
| **Risque** | Impact métier, exposition |
| **Recommandations** | Action précise, priorité, responsable, échéance |
| **Suivi** | Nouveau scan après correction |

Les **recommandations** donnent la **marche à suivre** (mettre à jour tel paquet vers telle version, désactiver tel service, restreindre tel port), pas seulement le constat.

## À retenir

- **Pas d'audit sans autorisation écrite** : périmètre, dates, méthodes, contacts.
- Découverte → ports → services et versions → vulnérabilités → rapport → correction → **nouveau scan**.
- **CVE** identifie une vulnérabilité ; **CVSS** note sa gravité de 0 à 10 (faible, moyenne, élevée, critique).
- Prioriser = score **et** exposition, exploitabilité, valeur du bien.
- Un scan **liste** ; un test d'intrusion **démontre** ; la fiche d'audit propose des actions concrètes.
