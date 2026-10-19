# Cours – Chiffrement asymétrique, signature numérique, certificats et PKI

*BTS SIO SISR 1re année – Bloc 3 – S11 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S10 (chiffrement symétrique, hachage, HMAC).
> - **Matériel :** VM Debian de laboratoire (`openssl`, `gpg`) ; navigateur web

## À la fin de ce cours tu sauras

- [ ] **Expliquer** le principe d'une paire de clés (publique / privée) et ses deux usages : chiffrer et signer ;
- [ ] **Décrire** le chiffrement hybride et l'échange de clés Diffie-Hellman ;
- [ ] **Générer** une paire de clés, **chiffrer** une clé de session, **signer** et **vérifier** un fichier avec OpenSSL ;
- [ ] **Lire** un certificat X.509 et en citer les champs essentiels ;
- [ ] **Décrire** les acteurs d'une PKI, la chaîne de confiance et le cycle de vie d'un certificat.

## I. Le chiffrement asymétrique

### Une paire de clés

En S10, la clé symétrique devait être partagée **avant** de pouvoir communiquer en secret. La cryptographie **asymétrique** supprime ce problème : chaque personne possède **deux clés** mathématiquement liées.

| Clé | Qui la connaît ? | Rôle |
|---|---|---|
| **Clé publique** | **Tout le monde** (on la distribue librement) | Chiffrer pour son propriétaire ; **vérifier** sa signature |
| **Clé privée** | **Son propriétaire seul** | Déchiffrer ; **signer** |

Ce qui est chiffré par une clé ne se déchiffre qu'avec l'**autre** clé de la paire. On ne peut pas, en pratique, déduire la clé privée de la clé publique.

### Deux usages, deux sens

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 575.60 255.60" style="max-width:768px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 244.8)">
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M20,-8C20,-8 534,-8 534,-8 540,-8 546,-14 546,-20 546,-20 546,-101 546,-101 546,-107 540,-113 534,-113 534,-113 20,-113 20,-113 14,-113 8,-107 8,-101 8,-101 8,-20 8,-20 8,-14 14,-8 20,-8"/>
<text text-anchor="start" x="16" y="-97.8" font-family="Helvetica,sans-Serif" font-size="14.00">Confidentialité : chiffrer</text>
</g>
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M26.5,-121C26.5,-121 507,-121 507,-121 513,-121 519,-127 519,-133 519,-133 519,-214 519,-214 519,-220 513,-226 507,-226 507,-226 26.5,-226 26.5,-226 20.5,-226 14.5,-220 14.5,-214 14.5,-214 14.5,-133 14.5,-133 14.5,-127 20.5,-121 26.5,-121"/>
<text text-anchor="start" x="22.5" y="-210.8" font-family="Helvetica,sans-Serif" font-size="14.00">Authenticité : signer</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M206,-74C206,-74 36,-74 36,-74 30,-74 24,-68 24,-62 24,-62 24,-36 24,-36 24,-30 30,-24 36,-24 36,-24 206,-24 206,-24 212,-24 218,-30 218,-36 218,-36 218,-62 218,-62 218,-68 212,-74 206,-74"/>
<text text-anchor="start" x="51" y="-53" font-family="Helvetica,sans-Serif" font-size="15.00">Bob chiffre avec la</text>
<text text-anchor="start" x="43" y="-38" font-family="Helvetica,sans-Serif" font-size="15.00">clé </text>
<text text-anchor="start" x="70" y="-38" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">publique</text>
<text text-anchor="start" x="144" y="-38" font-family="Helvetica,sans-Serif" font-size="15.00"> d&#39;Alice</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M518,-74C518,-74 288,-74 288,-74 282,-74 276,-68 276,-62 276,-62 276,-36 276,-36 276,-30 282,-24 288,-24 288,-24 518,-24 518,-24 524,-24 530,-30 530,-36 530,-36 530,-62 530,-62 530,-68 524,-74 518,-74"/>
<text text-anchor="start" x="295" y="-53" font-family="Helvetica,sans-Serif" font-size="15.00">Seule Alice déchiffre avec sa</text>
<text text-anchor="start" x="362" y="-38" font-family="Helvetica,sans-Serif" font-size="15.00">clé </text>
<text text-anchor="start" x="389" y="-38" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">privée</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M218.36,-49C233.98,-49 250.4,-49 266.73,-49"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="266.79,-52.15 275.79,-49 266.79,-45.85 266.79,-52.15"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M199.5,-187C199.5,-187 42.5,-187 42.5,-187 36.5,-187 30.5,-181 30.5,-175 30.5,-175 30.5,-149 30.5,-149 30.5,-143 36.5,-137 42.5,-137 42.5,-137 199.5,-137 199.5,-137 205.5,-137 211.5,-143 211.5,-149 211.5,-149 211.5,-175 211.5,-175 211.5,-181 205.5,-187 199.5,-187"/>
<text text-anchor="start" x="49.5" y="-166" font-family="Helvetica,sans-Serif" font-size="15.00">Alice signe avec sa</text>
<text text-anchor="start" x="80" y="-151" font-family="Helvetica,sans-Serif" font-size="15.00">clé </text>
<text text-anchor="start" x="107" y="-151" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">privée</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M491,-187C491,-187 315,-187 315,-187 309,-187 303,-181 303,-175 303,-175 303,-149 303,-149 303,-143 309,-137 315,-137 315,-137 491,-137 491,-137 497,-137 503,-143 503,-149 503,-149 503,-175 503,-175 503,-181 497,-187 491,-187"/>
<text text-anchor="start" x="322" y="-166" font-family="Helvetica,sans-Serif" font-size="15.00">Tous vérifient avec sa</text>
<text text-anchor="start" x="352.5" y="-151" font-family="Helvetica,sans-Serif" font-size="15.00">clé </text>
<text text-anchor="start" x="379.5" y="-151" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">publique</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M211.75,-162C237.76,-162 266.44,-162 293.47,-162"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="293.57,-165.15 302.57,-162 293.57,-158.85 293.57,-165.15"/>
</g>
</g>
</svg>
</figure>

> [!WARNING]
> **Chiffrer** : on utilise la clé **publique du destinataire**. **Signer** : on utilise sa **propre clé privée**. La clé privée ne quitte **jamais** son propriétaire ; si elle est volée, tout est compromis.

### Algorithmes courants

| Algorithme | Usage | Taille ou courbe recommandée |
|---|---|---|
| **RSA** | Chiffrement, signature | 2048 bits au minimum ; **3072 bits** conseillé pour durer (recommandations ANSSI et NIST, à vérifier) |
| **ECDSA**, **Ed25519** | Signature (courbes elliptiques) | Courbes P-256 ou Curve25519 |
| **ECDH**, **X25519** | Échange de clés | Courbes elliptiques |

Les **courbes elliptiques** offrent une sécurité équivalente avec des clés beaucoup plus courtes, donc des calculs plus rapides.

### Le chiffrement hybride

Le chiffrement asymétrique est **lent** et limité à de petits messages. En pratique, on **combine** les deux familles :

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 581.60 293.60" style="max-width:776px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 282.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M373.5,-272C373.5,-272 138.5,-272 138.5,-272 132.5,-272 126.5,-266 126.5,-260 126.5,-260 126.5,-230 126.5,-230 126.5,-224 132.5,-218 138.5,-218 138.5,-218 373.5,-218 373.5,-218 379.5,-218 385.5,-224 385.5,-230 385.5,-230 385.5,-260 385.5,-260 385.5,-266 379.5,-272 373.5,-272"/>
<text text-anchor="start" x="145.5" y="-250" font-family="Helvetica,sans-Serif" font-size="15.00">1. Générer une clé de session</text>
<text text-anchor="start" x="199.5" y="-233" font-family="Helvetica,sans-Serif" font-size="15.00">aléatoire (AES)</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M200,-160C200,-160 12,-160 12,-160 6,-160 0,-154 0,-148 0,-148 0,-107 0,-107 0,-101 6,-95 12,-95 12,-95 200,-95 200,-95 206,-95 212,-101 212,-107 212,-107 212,-148 212,-148 212,-154 206,-160 200,-160"/>
<text text-anchor="start" x="19" y="-139" font-family="Helvetica,sans-Serif" font-size="15.00">2. Chiffrer le </text>
<text text-anchor="start" x="117" y="-139" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">message</text>
<text text-anchor="start" x="24.5" y="-124" font-family="Helvetica,sans-Serif" font-size="15.00">avec la clé de session</text>
<text text-anchor="start" x="29" y="-109" font-family="Helvetica,sans-Serif" font-size="15.00">(symétrique, rapide)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M221.96,-217.79C202,-202.42 176.46,-182.76 154.43,-165.79"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="156.16,-163.15 147.11,-160.16 152.32,-168.14 156.16,-163.15"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M548,-160C548,-160 264,-160 264,-160 258,-160 252,-154 252,-148 252,-148 252,-107 252,-107 252,-101 258,-95 264,-95 264,-95 548,-95 548,-95 554,-95 560,-101 560,-107 560,-107 560,-148 560,-148 560,-154 554,-160 548,-160"/>
<text text-anchor="start" x="296.5" y="-139" font-family="Helvetica,sans-Serif" font-size="15.00">3. Chiffrer la </text>
<text text-anchor="start" x="394.5" y="-139" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">clé de session</text>
<text text-anchor="start" x="271" y="-124" font-family="Helvetica,sans-Serif" font-size="15.00">avec la clé publique du destinataire</text>
<text text-anchor="start" x="353" y="-109" font-family="Helvetica,sans-Serif" font-size="15.00">(asymétrique)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M290.04,-217.79C310,-202.42 335.54,-182.76 357.57,-165.79"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="359.68,-168.14 364.89,-160.16 355.84,-163.15 359.68,-168.14"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M337,-37C337,-37 175,-37 175,-37 169,-37 163,-31 163,-25 163,-25 163,-12 163,-12 163,-6 169,0 175,0 175,0 337,0 337,0 343,0 349,-6 349,-12 349,-12 349,-25 349,-25 349,-31 343,-37 337,-37"/>
<text text-anchor="start" x="182" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">4. Envoyer les deux</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M150.19,-94.98C173.75,-78.17 202.2,-57.88 223.67,-42.56"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="225.74,-44.95 231.24,-37.16 222.08,-39.82 225.74,-44.95"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M361.81,-94.98C338.25,-78.17 309.8,-57.88 288.33,-42.56"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="289.92,-39.82 280.76,-37.16 286.26,-44.95 289.92,-39.82"/>
</g>
</g>
</svg>
</figure>

C'est le principe de TLS, de GnuPG, de S/MIME et de la plupart des protocoles sécurisés.

### L'échange de clés Diffie-Hellman

L'**échange de clés Diffie-Hellman** permet à deux interlocuteurs de **fabriquer un secret commun** en échangeant uniquement des valeurs publiques, sur un canal observable. Chacun garde une valeur privée, envoie la valeur publique associée, puis calcule le même secret. Un espion qui voit les valeurs publiques ne peut pas retrouver le secret.

Utilisé avec des clés **éphémères** (nouvelle paire à chaque session), il apporte la **confidentialité persistante** (*forward secrecy*) : même si une clé privée est volée plus tard, les sessions passées enregistrées restent illisibles.

> [!NOTE]
> Diffie-Hellman seul n'**authentifie** pas les interlocuteurs : un attaquant placé au milieu peut mener deux échanges (attaque de l'homme du milieu). D'où le besoin de **signatures** et de **certificats**.

## II. La signature numérique

Une signature prouve **qui** a produit un document et que le document **n'a pas changé**.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 879.60 422.60" style="max-width:1173px;min-width:900px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 411.8)">
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M205,-37C205,-37 455,-37 455,-37 461,-37 467,-43 467,-49 467,-49 467,-381 467,-381 467,-387 461,-393 455,-393 455,-393 205,-393 205,-393 199,-393 193,-387 193,-381 193,-381 193,-49 193,-49 193,-43 199,-37 205,-37"/>
<text text-anchor="start" x="201" y="-377.8" font-family="Helvetica,sans-Serif" font-size="14.00">Émetteur</text>
</g>
<g class="cluster cl">
<path fill="transparent" stroke="black" d="M487,-8C487,-8 838,-8 838,-8 844,-8 850,-14 850,-20 850,-20 850,-381 850,-381 850,-387 844,-393 838,-393 838,-393 487,-393 487,-393 481,-393 475,-387 475,-381 475,-381 475,-20 475,-20 475,-14 481,-8 487,-8"/>
<text text-anchor="start" x="483" y="-377.8" font-family="Helvetica,sans-Serif" font-size="14.00">Destinataire</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M42,-354C42,-354 12,-354 12,-354 6,-354 0,-348 0,-342 0,-342 0,-329 0,-329 0,-323 6,-317 12,-317 12,-317 42,-317 42,-317 48,-317 54,-323 54,-329 54,-329 54,-342 54,-342 54,-348 48,-354 42,-354"/>
<text text-anchor="middle" x="27" y="-332" font-family="Helvetica,sans-Serif" font-size="15.00">E</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M42,-236.5C42,-236.5 12,-236.5 12,-236.5 6,-236.5 0,-230.5 0,-224.5 0,-224.5 0,-211.5 0,-211.5 0,-205.5 6,-199.5 12,-199.5 12,-199.5 42,-199.5 42,-199.5 48,-199.5 54,-205.5 54,-211.5 54,-211.5 54,-224.5 54,-224.5 54,-230.5 48,-236.5 42,-236.5"/>
<text text-anchor="middle" x="27" y="-214.5" font-family="Helvetica,sans-Serif" font-size="15.00">R</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M27,-316.96C27,-298.05 27,-267.72 27,-245.81"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="30.15,-245.71 27,-236.71 23.85,-245.71 30.15,-245.71"/>
<text text-anchor="start" x="27" y="-277.6" font-family="Helvetica,sans-Serif" font-size="13.00">document + signature</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M376,-354C376,-354 284,-354 284,-354 278,-354 272,-348 272,-342 272,-342 272,-329 272,-329 272,-323 278,-317 284,-317 284,-317 376,-317 376,-317 382,-317 388,-323 388,-329 388,-329 388,-342 388,-342 388,-348 382,-354 376,-354"/>
<text text-anchor="start" x="291" y="-332" font-family="Helvetica,sans-Serif" font-size="15.00">Document</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M376,-245C376,-245 284,-245 284,-245 278,-245 272,-239 272,-233 272,-233 272,-203 272,-203 272,-197 278,-191 284,-191 284,-191 376,-191 376,-191 382,-191 388,-197 388,-203 388,-203 388,-233 388,-233 388,-239 382,-245 376,-245"/>
<text text-anchor="start" x="296.5" y="-223" font-family="Helvetica,sans-Serif" font-size="15.00">Hachage</text>
<text text-anchor="start" x="291" y="-206" font-family="Helvetica,sans-Serif" font-size="15.00">(SHA&#45;256)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M330,-316.96C330,-300.43 330,-275.18 330,-254.46"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="333.15,-254.3 330,-245.3 326.85,-254.3 333.15,-254.3"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M438.5,-103C438.5,-103 221.5,-103 221.5,-103 215.5,-103 209.5,-97 209.5,-91 209.5,-91 209.5,-65 209.5,-65 209.5,-59 215.5,-53 221.5,-53 221.5,-53 438.5,-53 438.5,-53 444.5,-53 450.5,-59 450.5,-65 450.5,-65 450.5,-91 450.5,-91 450.5,-97 444.5,-103 438.5,-103"/>
<text text-anchor="start" x="228.5" y="-82" font-family="Helvetica,sans-Serif" font-size="15.00">Chiffrement de l&#39;empreinte</text>
<text text-anchor="start" x="260" y="-67" font-family="Helvetica,sans-Serif" font-size="15.00">avec la clé </text>
<text text-anchor="start" x="345" y="-67" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">privée</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M330,-190.72C330,-168.49 330,-136.51 330,-112.45"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="333.15,-112.33 330,-103.33 326.85,-112.33 333.15,-112.33"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M821.5,-354C821.5,-354 692.5,-354 692.5,-354 686.5,-354 680.5,-348 680.5,-342 680.5,-342 680.5,-329 680.5,-329 680.5,-323 686.5,-317 692.5,-317 692.5,-317 821.5,-317 821.5,-317 827.5,-317 833.5,-323 833.5,-329 833.5,-329 833.5,-342 833.5,-342 833.5,-348 827.5,-354 821.5,-354"/>
<text text-anchor="start" x="699.5" y="-332" font-family="Helvetica,sans-Serif" font-size="15.00">Document reçu</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M821.5,-236.5C821.5,-236.5 740.5,-236.5 740.5,-236.5 734.5,-236.5 728.5,-230.5 728.5,-224.5 728.5,-224.5 728.5,-211.5 728.5,-211.5 728.5,-205.5 734.5,-199.5 740.5,-199.5 740.5,-199.5 821.5,-199.5 821.5,-199.5 827.5,-199.5 833.5,-205.5 833.5,-211.5 833.5,-211.5 833.5,-224.5 833.5,-224.5 833.5,-230.5 827.5,-236.5 821.5,-236.5"/>
<text text-anchor="start" x="747.5" y="-214.5" font-family="Helvetica,sans-Serif" font-size="15.00">Hachage</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M760.65,-316.96C764.59,-297.96 770.93,-267.45 775.49,-245.52"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="778.57,-246.16 777.32,-236.71 772.41,-244.88 778.57,-246.16"/>
</g>
<g class="node n&#45;diamond">
<polygon fill="none" stroke="black" stroke-width="1.8" points="622,-132 491,-78 622,-24 753,-78 622,-132"/>
<text text-anchor="start" x="579" y="-83" font-family="Helvetica,sans-Serif" font-size="15.00">Empreintes</text>
<text text-anchor="start" x="575.5" y="-66" font-family="Helvetica,sans-Serif" font-size="15.00">identiques ?</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M760.54,-199.24C737.94,-179.63 700.77,-147.37 670.62,-121.19"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="672.37,-118.55 663.51,-115.03 668.24,-123.31 672.37,-118.55"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M676.5,-243C676.5,-243 503.5,-243 503.5,-243 497.5,-243 491.5,-237 491.5,-231 491.5,-231 491.5,-205 491.5,-205 491.5,-199 497.5,-193 503.5,-193 503.5,-193 676.5,-193 676.5,-193 682.5,-193 688.5,-199 688.5,-205 688.5,-205 688.5,-231 688.5,-231 688.5,-237 682.5,-243 676.5,-243"/>
<text text-anchor="start" x="513" y="-222" font-family="Helvetica,sans-Serif" font-size="15.00">Signature déchiffrée</text>
<text text-anchor="start" x="510.5" y="-207" font-family="Helvetica,sans-Serif" font-size="15.00">avec la clé </text>
<text text-anchor="start" x="595.5" y="-207" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">publique</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M595.57,-192.96C599.19,-177.36 604.07,-156.32 608.65,-136.57"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="611.76,-137.09 610.73,-127.61 605.63,-135.67 611.76,-137.09"/>
</g>
</g>
</svg>
</figure>

| Si la vérification… | Alors |
|---|---|
| **réussit** | Le document n'a pas changé **et** a bien été signé avec la clé privée correspondante |
| **échoue** | Le document a été modifié, ou la signature n'est pas celle de cette clé |

Elle garantit l'**intégrité**, l'**authenticité** et la **non-répudiation** (contrairement au HMAC, S10), à condition de savoir **à qui appartient la clé publique**. C'est le rôle des certificats.

## III. Les certificats numériques

### Le problème

Si Bob reçoit une clé publique « d'Alice », comment sait-il qu'elle est vraiment à Alice, et pas à un attaquant qui se fait passer pour elle ?

Un **certificat** (norme **X.509**) est un document numérique qui **lie une identité à une clé publique**, et qui est **signé par une autorité de confiance**.

### Les champs essentiels

| Champ | Contenu |
|---|---|
| **Sujet** (*Subject*) | À qui appartient le certificat (nom de domaine, organisation) |
| **Émetteur** (*Issuer*) | L'autorité qui l'a signé |
| **Validité** | Dates de début et de fin |
| **Clé publique** | La clé du sujet, avec son algorithme |
| **Nom alternatif** (*Subject Alternative Name*, SAN) | Les noms de domaine valables (le navigateur contrôle **celui-ci**) |
| **Usage de la clé** | Ce que le certificat peut faire (authentifier un serveur, signer…) |
| **Numéro de série** | Identifiant unique chez l'émetteur |
| **Signature** | Celle de l'émetteur sur tout le reste |

## IV. L'infrastructure à clés publiques (PKI)

Une **PKI** (*Public Key Infrastructure*) est l'ensemble des acteurs, règles et outils qui émettent, distribuent, valident et révoquent les certificats.

| Acteur | Rôle |
|---|---|
| **Autorité de certification (AC)** | Émet et signe les certificats ; sa clé privée est protégée au plus haut niveau |
| **Autorité d'enregistrement (AE)** | Vérifie l'identité du demandeur avant l'émission |
| **Titulaire** | Le serveur ou la personne qui possède le certificat |
| **Utilisateur de confiance** | Le navigateur ou le système qui vérifie le certificat |
| **Service de révocation** | **CRL** (liste de révocation) ou **OCSP** (interrogation en ligne) |

### La chaîne de confiance

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 342.60 345.60" style="max-width:457px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 334.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M309,-324C309,-324 12,-324 12,-324 6,-324 0,-318 0,-312 0,-312 0,-256 0,-256 0,-250 6,-244 12,-244 12,-244 309,-244 309,-244 315,-244 321,-250 321,-256 321,-256 321,-312 321,-312 321,-318 315,-324 309,-324"/>
<text text-anchor="start" x="120" y="-303" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">AC racine</text>
<text text-anchor="start" x="84.5" y="-288" font-family="Helvetica,sans-Serif" font-size="15.00">certificat auto&#45;signé</text>
<text text-anchor="start" x="19" y="-273" font-family="Helvetica,sans-Serif" font-size="15.00">installé dans le magasin de confiance</text>
<text text-anchor="start" x="67" y="-258" font-family="Helvetica,sans-Serif" font-size="15.00">de l&#39;OS ou du navigateur</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M278,-172C278,-172 43,-172 43,-172 37,-172 31,-166 31,-160 31,-160 31,-134 31,-134 31,-128 37,-122 43,-122 43,-122 278,-122 278,-122 284,-122 290,-128 290,-134 290,-134 290,-160 290,-160 290,-166 284,-172 278,-172"/>
<text text-anchor="start" x="88" y="-151" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">AC intermédiaire</text>
<text text-anchor="start" x="50" y="-136" font-family="Helvetica,sans-Serif" font-size="15.00">(clé racine gardée hors ligne)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M160.5,-243.95C160.5,-224.1 160.5,-200.23 160.5,-181.26"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="163.65,-181.11 160.5,-172.11 157.35,-181.11 163.65,-181.11"/>
<text text-anchor="start" x="160.5" y="-204.6" font-family="Helvetica,sans-Serif" font-size="13.00">signe</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M256,-50C256,-50 65,-50 65,-50 59,-50 53,-44 53,-38 53,-38 53,-12 53,-12 53,-6 59,0 65,0 65,0 256,0 256,0 262,0 268,-6 268,-12 268,-12 268,-38 268,-38 268,-44 262,-50 256,-50"/>
<text text-anchor="start" x="72" y="-29" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Certificat du serveur</text>
<text text-anchor="start" x="100.5" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">www.exemple.fr</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M160.5,-121.72C160.5,-103.82 160.5,-79.27 160.5,-59.51"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="163.65,-59.25 160.5,-50.25 157.35,-59.25 163.65,-59.25"/>
<text text-anchor="start" x="160.5" y="-82.6" font-family="Helvetica,sans-Serif" font-size="13.00">signe</text>
</g>
</g>
</svg>
</figure>

Le navigateur remonte la chaîne : le certificat du serveur est signé par l'intermédiaire, lui-même signé par une racine **présente dans son magasin de confiance**. Il vérifie aussi la **validité**, le **nom** (SAN) et l'état de **révocation**.

> [!NOTE]
> On garde la clé de l'**AC racine hors ligne** et on signe avec une **intermédiaire** : si l'intermédiaire est compromise, on la révoque sans perdre la racine.

### Types de certificats

| Type | Vérification | Usage |
|---|---|---|
| **DV** (*Domain Validated*) | Le demandeur contrôle le domaine | Sites web, automatisable (Let's Encrypt, protocole ACME) |
| **OV** (*Organization Validated*) | Existence de l'organisation | Sites d'entreprise |
| **EV** (*Extended Validation*) | Vérification approfondie | Sites sensibles (le navigateur n'affiche plus de signe particulier) |
| **Auto-signé** | Aucune | Tests, laboratoires : **non reconnu** par défaut |
| **Certificat interne** | AC de l'entreprise | Intranet, VPN, Wi-Fi d'entreprise |

### Cycle de vie

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 391.10 506.60" style="max-width:521px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 495.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M273.5,-485C273.5,-485 91.5,-485 91.5,-485 85.5,-485 79.5,-479 79.5,-473 79.5,-473 79.5,-443 79.5,-443 79.5,-437 85.5,-431 91.5,-431 91.5,-431 273.5,-431 273.5,-431 279.5,-431 285.5,-437 285.5,-443 285.5,-443 285.5,-473 285.5,-473 285.5,-479 279.5,-485 273.5,-485"/>
<text text-anchor="start" x="98.5" y="-463" font-family="Helvetica,sans-Serif" font-size="15.00">Génération de la paire</text>
<text text-anchor="start" x="113.5" y="-446" font-family="Helvetica,sans-Serif" font-size="15.00">et demande (CSR)</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M232.5,-373C232.5,-373 132.5,-373 132.5,-373 126.5,-373 120.5,-367 120.5,-361 120.5,-361 120.5,-331 120.5,-331 120.5,-325 126.5,-319 132.5,-319 132.5,-319 232.5,-319 232.5,-319 238.5,-319 244.5,-325 244.5,-331 244.5,-331 244.5,-361 244.5,-361 244.5,-367 238.5,-373 232.5,-373"/>
<text text-anchor="start" x="140" y="-351" font-family="Helvetica,sans-Serif" font-size="15.00">Vérification</text>
<text text-anchor="start" x="139.5" y="-334" font-family="Helvetica,sans-Serif" font-size="15.00">et émission</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M182.5,-430.93C182.5,-416.52 182.5,-398.39 182.5,-382.68"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="185.65,-382.26 182.5,-373.26 179.35,-382.26 185.65,-382.26"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M238,-261C238,-261 127,-261 127,-261 121,-261 115,-255 115,-249 115,-249 115,-236 115,-236 115,-230 121,-224 127,-224 127,-224 238,-224 238,-224 244,-224 250,-230 250,-236 250,-236 250,-249 250,-249 250,-255 244,-261 238,-261"/>
<text text-anchor="start" x="134" y="-239" font-family="Helvetica,sans-Serif" font-size="15.00">Déploiement</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M182.5,-318.86C182.5,-304.02 182.5,-285.48 182.5,-270.5"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="185.65,-270.24 182.5,-261.24 179.35,-270.24 185.65,-270.24"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M244,-166C244,-166 121,-166 121,-166 115,-166 109,-160 109,-154 109,-154 109,-124 109,-124 109,-118 115,-112 121,-112 121,-112 244,-112 244,-112 250,-112 256,-118 256,-124 256,-124 256,-154 256,-154 256,-160 250,-166 244,-166"/>
<text text-anchor="start" x="135.5" y="-144" font-family="Helvetica,sans-Serif" font-size="15.00">Surveillance</text>
<text text-anchor="start" x="128" y="-127" font-family="Helvetica,sans-Serif" font-size="15.00">de l&#39;expiration</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M182.5,-223.82C182.5,-210.53 182.5,-191.87 182.5,-175.53"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="185.65,-175.24 182.5,-166.24 179.35,-175.24 185.65,-175.24"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M149,-45.5C149,-45.5 12,-45.5 12,-45.5 6,-45.5 0,-39.5 0,-33.5 0,-33.5 0,-20.5 0,-20.5 0,-14.5 6,-8.5 12,-8.5 12,-8.5 149,-8.5 149,-8.5 155,-8.5 161,-14.5 161,-20.5 161,-20.5 161,-33.5 161,-33.5 161,-39.5 155,-45.5 149,-45.5"/>
<text text-anchor="start" x="19" y="-23.5" font-family="Helvetica,sans-Serif" font-size="15.00">Renouvellement</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M158.33,-111.93C141.58,-93.87 119.44,-69.99 103.06,-52.32"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="105.29,-50.1 96.86,-45.64 100.67,-54.39 105.29,-50.1"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M357.5,-54C357.5,-54 213.5,-54 213.5,-54 207.5,-54 201.5,-48 201.5,-42 201.5,-42 201.5,-12 201.5,-12 201.5,-6 207.5,0 213.5,0 213.5,0 357.5,0 357.5,0 363.5,0 369.5,-6 369.5,-12 369.5,-12 369.5,-42 369.5,-42 369.5,-48 363.5,-54 357.5,-54"/>
<text text-anchor="start" x="243.5" y="-32" font-family="Helvetica,sans-Serif" font-size="15.00">Révocation</text>
<text text-anchor="start" x="220.5" y="-15" font-family="Helvetica,sans-Serif" font-size="15.00">(clé compromise)</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M206.91,-111.93C221.17,-96.7 239.31,-77.33 254.57,-61.04"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="257.06,-62.99 260.91,-54.26 252.46,-58.68 257.06,-62.99"/>
</g>
</g>
</svg>
</figure>

Les incidents classiques viennent de la **gestion** : un certificat **expiré** qui coupe un service, une clé privée copiée trop largement, un certificat oublié dans un inventaire. Un technicien tient un **inventaire** des certificats avec leurs dates d'expiration.

## V. Dans TLS

Quand tu ouvres un site en HTTPS :

<figure class="graphe diagramme"><svg viewBox="0 0 825 458" style="max-width:825px" role="img" aria-label="Diagramme de séquence" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="s9662c3" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" orient="auto"><path d="M0,0 L10,5 L0,10 z" class="seq-head"/></marker></defs>
<line class="seq-life" x1="206" y1="62" x2="206" y2="452"/>
<rect class="seq-box" x="141" y="12" width="130" height="40" rx="8"/><text x="206" y="37" text-anchor="middle" class="seq-title">Navigateur</text>
<line class="seq-life" x1="619" y1="62" x2="619" y2="452"/>
<rect class="seq-box" x="554" y="12" width="130" height="40" rx="8"/><text x="619" y="37" text-anchor="middle" class="seq-title">Serveur</text>
<line class="seq-msg" x1="206" y1="96" x2="615" y2="96" marker-end="url(#s9662c3)"/><text x="413" y="88" text-anchor="middle">Bonjour (versions et suites acceptées)</text>
<line class="seq-msg" x1="619" y1="146" x2="210" y2="146" marker-end="url(#s9662c3)"/><text x="413" y="138" text-anchor="middle">Choix de la suite + certificat</text>
<path class="seq-msg" d="M206,188 h34 v22 h-30" marker-end="url(#s9662c3)"/><text x="250" y="204">Vérifie la chaîne, le nom (SAN), la validité</text>
<line class="seq-msg" x1="206" y1="254" x2="615" y2="254" marker-end="url(#s9662c3)"/><text x="413" y="246" text-anchor="middle">Échange de clés éphémère (ECDHE)</text>
<line class="seq-msg" x1="619" y1="304" x2="210" y2="304" marker-end="url(#s9662c3)"/><text x="413" y="296" text-anchor="middle">Preuve de possession de la clé privée (signature)</text>
<rect class="seq-note" x="131" y="338" width="563" height="34" rx="6"/><text x="413" y="360" text-anchor="middle">Les deux calculent la même clé de session</text>
<line class="seq-msg" x1="206" y1="398" x2="615" y2="398" marker-end="url(#s9662c3)"/><text x="413" y="390" text-anchor="middle">Données chiffrées (AES-GCM)</text>
</svg></figure>

On y retrouve **tout le chapitre** : certificat (identité), signature (authenticité), Diffie-Hellman éphémère (secret + confidentialité persistante), chiffrement symétrique authentifié (rapidité + intégrité).

## À retenir

- **Chiffrer** : clé **publique** du destinataire. **Signer** : **sa** clé privée. La clé privée ne se partage pas.
- On chiffre le message en **symétrique**, et la clé de session en **asymétrique** (**hybride**).
- **Diffie-Hellman** crée un secret commun ; en **éphémère**, il apporte la confidentialité persistante.
- Une **signature** garantit intégrité, authenticité et non-répudiation.
- Un **certificat** lie une identité à une clé publique, signé par une **AC** ; la **chaîne de confiance** remonte à une racine connue du système.
- Un certificat se **gère** : inventaire, renouvellement avant l'expiration, révocation en cas de compromission.
