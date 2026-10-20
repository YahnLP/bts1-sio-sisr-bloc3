# Cours – VPN : principes, protocoles et architecture

*BTS SIO SISR 1re année – Bloc 3 – S13 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S10 et S11 (chiffrement, clés publiques et privées) ; notions de routage IP.
> - **Matériel :** Deux VM Debian de laboratoire sur un réseau interne (`wireguard`, `tcpdump`) ; droits `sudo`

## À la fin de ce cours tu sauras

- [ ] **Définir** un VPN et la tunnelisation, et **distinguer** VPN nomade et VPN site à site ;
- [ ] **Comparer** IPsec, OpenVPN et WireGuard (usage, forces, limites) ;
- [ ] **Monter** un tunnel WireGuard avec une paire de clés par machine ;
- [ ] **Vérifier** que le trafic est chiffré et que seules les routes prévues passent par le tunnel ;
- [ ] **Citer** les mesures de sécurité d'un VPN d'entreprise (authentification, moindre privilège, journalisation).

## I. Qu'est-ce qu'un VPN ?

Un **VPN** (*Virtual Private Network*, réseau privé virtuel) crée un **tunnel chiffré et authentifié** à travers un réseau non sûr (Internet) pour relier deux extrémités comme si elles étaient sur le même réseau privé.

Il apporte, grâce à S10 et S11 :

| Garantie | Mécanisme |
|---|---|
| **Confidentialité** | Chiffrement symétrique du trafic |
| **Intégrité** | Mode authentifié ou HMAC |
| **Authentification** des extrémités | Clés publiques, certificats, secrets partagés, MFA |

### La tunnelisation

La **tunnelisation** consiste à **encapsuler** un paquet entier dans un autre paquet, après l'avoir chiffré.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 358.60 557.60" style="max-width:479px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 546.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M258.5,-536C258.5,-536 78.5,-536 78.5,-536 72.5,-536 66.5,-530 66.5,-524 66.5,-524 66.5,-494 66.5,-494 66.5,-488 72.5,-482 78.5,-482 78.5,-482 258.5,-482 258.5,-482 264.5,-482 270.5,-488 270.5,-494 270.5,-494 270.5,-524 270.5,-524 270.5,-530 264.5,-536 258.5,-536"/>
<text text-anchor="start" x="107" y="-514" font-family="Helvetica,sans-Serif" font-size="15.00">Paquet d&#39;origine</text>
<text text-anchor="start" x="85.5" y="-497" font-family="Helvetica,sans-Serif" font-size="15.00">10.8.0.2 → 172.16.0.1</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M244.5,-423C244.5,-423 92.5,-423 92.5,-423 86.5,-423 80.5,-417 80.5,-411 80.5,-411 80.5,-381 80.5,-381 80.5,-375 86.5,-369 92.5,-369 92.5,-369 244.5,-369 244.5,-369 250.5,-369 256.5,-375 256.5,-381 256.5,-381 256.5,-411 256.5,-411 256.5,-417 250.5,-423 244.5,-423"/>
<text text-anchor="start" x="123.5" y="-401" font-family="Helvetica,sans-Serif" font-size="15.00">Chiffrement</text>
<text text-anchor="start" x="99.5" y="-384" font-family="Helvetica,sans-Serif" font-size="15.00">+ authentification</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M168.5,-481.98C168.5,-467.19 168.5,-448.48 168.5,-432.37"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="171.65,-432.25 168.5,-423.25 165.35,-432.25 171.65,-432.25"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M325,-310C325,-310 12,-310 12,-310 6,-310 0,-304 0,-298 0,-298 0,-251 0,-251 0,-245 6,-239 12,-239 12,-239 325,-239 325,-239 331,-239 337,-245 337,-251 337,-251 337,-298 337,-298 337,-304 331,-310 325,-310"/>
<text text-anchor="start" x="106" y="-288" font-family="Helvetica,sans-Serif" font-size="15.00">Nouveau paquet</text>
<text text-anchor="start" x="19" y="-271" font-family="Helvetica,sans-Serif" font-size="15.00">IP publique client → IP publique serveur</text>
<text text-anchor="start" x="105" y="-254" font-family="Helvetica,sans-Serif" font-size="15.00">(contenu chiffré)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M168.5,-368.78C168.5,-354.28 168.5,-335.9 168.5,-319.29"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="171.65,-319.28 168.5,-310.28 165.35,-319.28 171.65,-319.28"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M245,-167C245,-167 92,-167 92,-167 86,-167 80,-161 80,-155 80,-155 80,-125 80,-125 80,-119 86,-113 92,-113 92,-113 245,-113 245,-113 251,-113 257,-119 257,-125 257,-125 257,-155 257,-155 257,-161 251,-167 245,-167"/>
<text text-anchor="start" x="114.5" y="-145" font-family="Helvetica,sans-Serif" font-size="15.00">Déchiffrement</text>
<text text-anchor="start" x="99" y="-128" font-family="Helvetica,sans-Serif" font-size="15.00">par le serveur VPN</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M168.5,-238.69C168.5,-219.45 168.5,-195.6 168.5,-176.29"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="171.65,-176.21 168.5,-167.21 165.35,-176.21 171.65,-176.21"/>
<text text-anchor="start" x="168.5" y="-199.6" font-family="Helvetica,sans-Serif" font-size="13.00">Internet</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M260.5,-54C260.5,-54 76.5,-54 76.5,-54 70.5,-54 64.5,-48 64.5,-42 64.5,-42 64.5,-12 64.5,-12 64.5,-6 70.5,0 76.5,0 76.5,0 260.5,0 260.5,0 266.5,0 272.5,-6 272.5,-12 272.5,-12 272.5,-42 272.5,-42 272.5,-48 266.5,-54 260.5,-54"/>
<text text-anchor="start" x="107" y="-32" font-family="Helvetica,sans-Serif" font-size="15.00">Paquet d&#39;origine</text>
<text text-anchor="start" x="83.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">livré au réseau interne</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M168.5,-112.98C168.5,-98.19 168.5,-79.48 168.5,-63.37"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="171.65,-63.25 168.5,-54.25 165.35,-63.25 171.65,-63.25"/>
</g>
</g>
</svg>
</figure>

Un observateur sur Internet ne voit que **deux adresses publiques** et des données chiffrées.

## II. Deux grands usages

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 480.60 477.60" style="max-width:641px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 466.8)">
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M20,-104C20,-104 208,-104 208,-104 214,-104 220,-110 220,-116 220,-116 220,-436 220,-436 220,-442 214,-448 208,-448 208,-448 20,-448 20,-448 14,-448 8,-442 8,-436 8,-436 8,-116 8,-116 8,-110 14,-104 20,-104"/>
<text text-anchor="start" x="16" y="-432.8" font-family="Helvetica,sans-Serif" font-size="14.00">VPN nomade (accès distant)</text>
</g>
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M240,-8C240,-8 438,-8 438,-8 444,-8 450,-14 450,-20 450,-20 450,-427.5 450,-427.5 450,-433.5 444,-439.5 438,-439.5 438,-439.5 240,-439.5 240,-439.5 234,-439.5 228,-433.5 228,-427.5 228,-427.5 228,-20 228,-20 228,-14 234,-8 240,-8"/>
<text text-anchor="start" x="236" y="-424.3" font-family="Helvetica,sans-Serif" font-size="14.00">VPN site à site</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M174,-409C174,-409 54,-409 54,-409 48,-409 42,-403 42,-397 42,-397 42,-367 42,-367 42,-361 48,-355 54,-355 54,-355 174,-355 174,-355 180,-355 186,-361 186,-367 186,-367 186,-397 186,-397 186,-403 180,-409 174,-409"/>
<text text-anchor="start" x="75" y="-387" font-family="Helvetica,sans-Serif" font-size="15.00">Poste d&#39;un</text>
<text text-anchor="start" x="61" y="-370" font-family="Helvetica,sans-Serif" font-size="15.00">télétravailleur</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M175.5,-283C175.5,-283 52.5,-283 52.5,-283 46.5,-283 40.5,-277 40.5,-271 40.5,-271 40.5,-241 40.5,-241 40.5,-235 46.5,-229 52.5,-229 52.5,-229 175.5,-229 175.5,-229 181.5,-229 187.5,-235 187.5,-241 187.5,-241 187.5,-271 187.5,-271 187.5,-277 181.5,-283 175.5,-283"/>
<text text-anchor="start" x="67" y="-261" font-family="Helvetica,sans-Serif" font-size="15.00">Serveur VPN</text>
<text text-anchor="start" x="59.5" y="-244" font-family="Helvetica,sans-Serif" font-size="15.00">de l&#39;entreprise</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M114,-354.7C114,-336.54 114,-312.17 114,-292.31"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="117.15,-292.26 114,-283.26 110.85,-292.26 117.15,-292.26"/>
<text text-anchor="start" x="114" y="-315.6" font-family="Helvetica,sans-Serif" font-size="13.00">tunnel</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M177.5,-157C177.5,-157 50.5,-157 50.5,-157 44.5,-157 38.5,-151 38.5,-145 38.5,-145 38.5,-132 38.5,-132 38.5,-126 44.5,-120 50.5,-120 50.5,-120 177.5,-120 177.5,-120 183.5,-120 189.5,-126 189.5,-132 189.5,-132 189.5,-145 189.5,-145 189.5,-151 183.5,-157 177.5,-157"/>
<text text-anchor="start" x="57.5" y="-135" font-family="Helvetica,sans-Serif" font-size="15.00">Réseau interne</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M114,-228.79C114,-210.09 114,-185.02 114,-166.2"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="117.15,-166 114,-157 110.85,-166 117.15,-166"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M408.5,-400.5C408.5,-400.5 269.5,-400.5 269.5,-400.5 263.5,-400.5 257.5,-394.5 257.5,-388.5 257.5,-388.5 257.5,-375.5 257.5,-375.5 257.5,-369.5 263.5,-363.5 269.5,-363.5 269.5,-363.5 408.5,-363.5 408.5,-363.5 414.5,-363.5 420.5,-369.5 420.5,-375.5 420.5,-375.5 420.5,-388.5 420.5,-388.5 420.5,-394.5 414.5,-400.5 408.5,-400.5"/>
<text text-anchor="start" x="276.5" y="-378.5" font-family="Helvetica,sans-Serif" font-size="15.00">Réseau du site A</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M422,-274.5C422,-274.5 256,-274.5 256,-274.5 250,-274.5 244,-268.5 244,-262.5 244,-262.5 244,-249.5 244,-249.5 244,-243.5 250,-237.5 256,-237.5 256,-237.5 422,-237.5 422,-237.5 428,-237.5 434,-243.5 434,-249.5 434,-249.5 434,-262.5 434,-262.5 434,-268.5 428,-274.5 422,-274.5"/>
<text text-anchor="start" x="263" y="-252.5" font-family="Helvetica,sans-Serif" font-size="15.00">Routeur / pare&#45;feu A</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M339,-363.5C339,-340 339,-298.47 339,-274.82"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M422,-157C422,-157 256,-157 256,-157 250,-157 244,-151 244,-145 244,-145 244,-132 244,-132 244,-126 250,-120 256,-120 256,-120 422,-120 422,-120 428,-120 434,-126 434,-132 434,-132 434,-145 434,-145 434,-151 428,-157 422,-157"/>
<text text-anchor="start" x="263" y="-135" font-family="Helvetica,sans-Serif" font-size="15.00">Routeur / pare&#45;feu B</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M339,-237.46C339,-218.55 339,-188.22 339,-166.31"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="342.15,-166.21 339,-157.21 335.85,-166.21 342.15,-166.21"/>
<text text-anchor="start" x="339" y="-189.6" font-family="Helvetica,sans-Serif" font-size="13.00">tunnel permanent</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M408.5,-61C408.5,-61 269.5,-61 269.5,-61 263.5,-61 257.5,-55 257.5,-49 257.5,-49 257.5,-36 257.5,-36 257.5,-30 263.5,-24 269.5,-24 269.5,-24 408.5,-24 408.5,-24 414.5,-24 420.5,-30 420.5,-36 420.5,-36 420.5,-49 420.5,-49 420.5,-55 414.5,-61 408.5,-61"/>
<text text-anchor="start" x="276.5" y="-39" font-family="Helvetica,sans-Serif" font-size="15.00">Réseau du site B</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M339,-119.82C339,-103.01 339,-77.88 339,-61.1"/>
</g>
</g>
</svg>
</figure>

| | **VPN nomade** | **VPN site à site** |
|---|---|---|
| Qui se connecte | Un **utilisateur** depuis un poste | Deux **réseaux** entre eux |
| Durée | À la demande | Permanent |
| Authentification | Utilisateur + appareil (**MFA** recommandé) | Équipements (clés, certificats) |
| Exemple | Télétravailleur qui accède au partage de fichiers | Agence reliée au siège |

## III. Les protocoles

| Protocole | Principe | Points forts | Limites |
|---|---|---|---|
| **IPsec** (IKEv2) | Intégré à la couche réseau, négociation par IKE, chiffrement ESP | Standard, très répandu sur les routeurs et pare-feu, idéal en **site à site** | Configuration complexe, nombreuses options (donc erreurs possibles) |
| **OpenVPN** | S'appuie sur **TLS** (certificats), en UDP ou TCP | Souple, passe les pare-feu (port 443 TCP), mature | Plus lourd, plus lent que WireGuard |
| **WireGuard** | Noyau Linux, une **paire de clés par machine**, cryptographie moderne figée | **Simple**, rapide, code très court (donc plus facile à auditer) | Pas d'attribution dynamique d'adresses ni de gestion d'utilisateurs intégrées, UDP seulement |
| **VPN SSL** (portail) | Accès par navigateur à des applications précises | Pas de client à installer | Limité aux applications publiées |

> [!NOTE]
> **Choisir** : site à site entre pare-feu → IPsec ; nomades avec gestion d'utilisateurs → OpenVPN ou une solution commerciale ; besoin de simplicité et de performances, avec un petit nombre de machines → WireGuard. Le bon choix dépend aussi de **ce que gèrent déjà** le pare-feu et l'équipe.

### Le principe de WireGuard

Chaque machine possède une **clé privée** et une **clé publique**. Une machine ne parle qu'aux **pairs** dont elle connaît la clé publique, et leur associe des **adresses autorisées** (`AllowedIPs`).

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 593.60 101.60" style="max-width:792px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 90.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M204,-80C204,-80 12,-80 12,-80 6,-80 0,-74 0,-68 0,-68 0,-12 0,-12 0,-6 6,0 12,0 12,0 204,0 204,0 210,0 216,-6 216,-12 216,-12 216,-68 216,-68 216,-74 210,-80 204,-80"/>
<text text-anchor="start" x="82.5" y="-59" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Client</text>
<text text-anchor="start" x="63.5" y="-44" font-family="Helvetica,sans-Serif" font-size="15.00">clé privée C</text>
<text text-anchor="start" x="28" y="-29" font-family="Helvetica,sans-Serif" font-size="15.00">connaît la publique S</text>
<text text-anchor="start" x="19" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">adresse tunnel 10.8.0.2</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M560,-80C560,-80 368,-80 368,-80 362,-80 356,-74 356,-68 356,-68 356,-12 356,-12 356,-6 362,0 368,0 368,0 560,0 560,0 566,0 572,-6 572,-12 572,-12 572,-68 572,-68 572,-74 566,-80 560,-80"/>
<text text-anchor="start" x="430.5" y="-59" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Serveur</text>
<text text-anchor="start" x="420" y="-44" font-family="Helvetica,sans-Serif" font-size="15.00">clé privée S</text>
<text text-anchor="start" x="383.5" y="-29" font-family="Helvetica,sans-Serif" font-size="15.00">connaît la publique C</text>
<text text-anchor="start" x="375" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">adresse tunnel 10.8.0.1</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M225.34,-40C264.28,-40 307.67,-40 346.61,-40"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="225.17,-36.85 216.17,-40 225.17,-43.15 225.17,-36.85"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="346.89,-43.15 355.89,-40 346.89,-36.85 346.89,-43.15"/>
<text text-anchor="start" x="249.5" y="-57.6" font-family="Helvetica,sans-Serif" font-size="13.00">UDP 51820</text>
<text text-anchor="start" x="245" y="-43.6" font-family="Helvetica,sans-Serif" font-size="13.00">trafic chiffré</text>
</g>
</g>
</svg>
</figure>

`AllowedIPs` joue **deux rôles** :
1. à l'**envoi** : le trafic vers ces adresses est envoyé dans le tunnel (c'est une **table de routage**) ;
2. à la **réception** : le trafic venant du pair n'est accepté que si l'adresse source en fait partie (**filtrage**).

## IV. Tunnel complet ou partiel

| Mode | `AllowedIPs` du client | Effet |
|---|---|---|
| **Tunnel complet** (*full tunnel*) | `0.0.0.0/0` | **Tout** le trafic passe par l'entreprise : contrôle et journalisation, mais plus de bande passante et de latence |
| **Tunnel partiel** (*split tunnel*) | Seuls les réseaux d'entreprise | Seul le trafic d'entreprise est tunnelisé ; le reste sort directement |

Le tunnel partiel est plus léger, mais le trafic Internet de l'utilisateur échappe aux contrôles de l'entreprise. Le choix est une décision de **sécurité**.

## V. Sécuriser un VPN d'entreprise

Un VPN est une **porte d'entrée vers le réseau interne** : il doit être exemplaire.

| Mesure | Détail |
|---|---|
| **Authentification forte** | Clé ou certificat **et** second facteur utilisateur (S03) |
| **Moindre privilège** | Le tunnel donne accès aux **services nécessaires**, pas à tout le réseau (pare-feu derrière le VPN, S14) |
| **Postes de confiance** | Poste à jour, chiffré, antivirus actif (S02) ; contrôle de conformité avant connexion |
| **Cycle de vie des clés** | Une clé par appareil ; **révocation** au départ ou à la perte (S04) |
| **Journalisation et alertes** | Qui s'est connecté, quand, d'où (S15) |
| **Maintenance** | Mises à jour du serveur VPN (des vulnérabilités critiques touchent régulièrement les équipements d'accès distant) |
| **Exposition minimale** | Un seul port ouvert, protocoles et versions à jour |

### Télétravail et équipements personnels (BYOD)

Le télétravail déplace le poste hors du réseau de l'entreprise. Le **BYOD** (*bring your own device*) va plus loin : l'agent utilise son **équipement personnel**. Dans les deux cas, l'administrateur ne maîtrise ni le réseau (box personnelle, objets connectés), ni toujours l'appareil (partagé en famille, perdu, volé).

| Risque | Mesure |
|---|---|
| Réseau domestique non maîtrisé | **VPN** vers l'entreprise, Wi-Fi domestique protégé (WPA2 ou WPA3, mot de passe changé) |
| Appareil perdu ou volé | **Chiffrement** du disque ou du téléphone, verrouillage, **déclaration immédiate** |
| Appareil partagé ou non à jour | Compte distinct, mises à jour, antivirus ; accès **refusé** si l'appareil n'est pas conforme |
| Mélange données pro / perso | **Profil ou espace professionnel** séparé ; accès par **navigateur** ou bureau distant plutôt que copie locale |
| Départ de l'agent | **Révocation** de la clé et effacement de la partie professionnelle seulement |

> [!NOTE]
> Le BYOD suppose une **charte** signée : usages autorisés, mesures exigées, ce que l'entreprise peut contrôler (la partie **professionnelle**, pas la vie privée de l'agent). Un poste **fourni** par l'entreprise reste plus simple à protéger : le BYOD est un arbitrage entre coût et maîtrise.

## À retenir

- Un VPN crée un **tunnel chiffré et authentifié** : confidentialité, intégrité, authentification des extrémités.
- **Nomade** (utilisateur) ou **site à site** (réseaux) ; protocoles **IPsec**, **OpenVPN**, **WireGuard**.
- WireGuard : une paire de clés par machine, `AllowedIPs` = routage **et** filtrage.
- **Tunnel complet** ou **partiel** : décision de sécurité.
- **Télétravail et BYOD** : réseau et appareil non maîtrisés ; VPN, chiffrement, profil professionnel séparé, conformité, charte.
- Un VPN est une **porte d'entrée** : MFA, moindre privilège, révocation, journaux, mises à jour.
