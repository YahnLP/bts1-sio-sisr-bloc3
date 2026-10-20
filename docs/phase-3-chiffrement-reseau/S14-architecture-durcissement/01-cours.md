# Cours – Architecture réseau sécurisée et durcissement

*BTS SIO SISR 1re année – Bloc 3 – S14 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S04 (droits), S11 à S13 (TLS, VPN) ; notions d'adressage IP et de pare-feu.
> - **Matériel :** Deux VM Debian de laboratoire (`openssh-server`, `ufw`, `lynis`) ; éditeur de schémas ou papier

## À la fin de ce cours tu sauras

- [ ] **Appliquer** les principes de défense en profondeur et de cloisonnement à un réseau d'entreprise ;
- [ ] **Concevoir** des zones (LAN, DMZ, administration) et **écrire** la matrice de flux autorisés ;
- [ ] **Durcir** un serveur Linux : services, SSH par clés, pare-feu, mises à jour ;
- [ ] **Mesurer** le durcissement avec un outil d'audit (Lynis) avant et après ;
- [ ] **Citer** les référentiels de bonnes pratiques (ANSSI, CIS) et leur usage.

## I. Principes d'une architecture sécurisée

| Principe | Idée | Exemple |
|---|---|---|
| **Défense en profondeur** | Plusieurs couches : une défaillance ne suffit pas à tout compromettre | Pare-feu + durcissement + droits + sauvegardes + supervision |
| **Moindre privilège** (S04) | Chaque élément n'a que ce qui lui est nécessaire | Le serveur web n'accède pas à la base RH |
| **Cloisonnement** | Séparer les zones pour limiter la propagation | Un poste infecté n'atteint pas les serveurs |
| **Refus par défaut** | Tout est interdit sauf ce qui est explicitement autorisé | Règle finale du pare-feu : *deny all* |
| **Réduction de la surface d'attaque** | Moins de services, moins de ports, moins de logiciels | Désinstaller ce qui ne sert pas |
| **Séparation des rôles** | Administration séparée de l'utilisation | Réseau d'administration dédié |

## II. Zones et flux

On découpe le réseau en **zones de confiance** et on contrôle les flux entre elles avec un **pare-feu**.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 1119.10 289.60" style="max-width:1492px;min-width:900px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 278.8)">
<g class="node n&#45;stadium">
<path fill="none" stroke="black" stroke-width="1.8" d="M414,-268C414,-268 339,-268 339,-268 333,-268 327,-262 327,-256 327,-256 327,-243 327,-243 327,-237 333,-231 339,-231 339,-231 414,-231 414,-231 420,-231 426,-237 426,-243 426,-243 426,-256 426,-256 426,-262 420,-268 414,-268"/>
<text text-anchor="start" x="346" y="-246" font-family="Helvetica,sans-Serif" font-size="15.00">Internet</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M444,-173C444,-173 309,-173 309,-173 303,-173 297,-167 297,-161 297,-161 297,-135 297,-135 297,-129 303,-123 309,-123 309,-123 444,-123 444,-123 450,-123 456,-129 456,-135 456,-135 456,-161 456,-161 456,-167 450,-173 444,-173"/>
<text text-anchor="start" x="340" y="-152" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Pare&#45;feu</text>
<text text-anchor="start" x="316" y="-137" font-family="Helvetica,sans-Serif" font-size="15.00">refus par défaut</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M376.5,-230.71C376.5,-217.35 376.5,-198.65 376.5,-182.51"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="379.65,-182.36 376.5,-173.36 373.35,-182.36 379.65,-182.36"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M237,-65C237,-65 12,-65 12,-65 6,-65 0,-59 0,-53 0,-53 0,-12 0,-12 0,-6 6,0 12,0 12,0 237,0 237,0 243,0 249,-6 249,-12 249,-12 249,-53 249,-53 249,-59 243,-65 237,-65"/>
<text text-anchor="start" x="104.5" y="-44" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">DMZ</text>
<text text-anchor="start" x="55" y="-29" font-family="Helvetica,sans-Serif" font-size="15.00">serveurs exposés :</text>
<text text-anchor="start" x="19" y="-14" font-family="Helvetica,sans-Serif" font-size="15.00">web, messagerie, relais VPN</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M323.06,-122.93C288.12,-107.2 241.9,-86.38 202.84,-68.78"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="204.12,-65.91 194.62,-65.08 201.54,-71.65 204.12,-65.91"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M452,-57.5C452,-57.5 301,-57.5 301,-57.5 295,-57.5 289,-51.5 289,-45.5 289,-45.5 289,-19.5 289,-19.5 289,-13.5 295,-7.5 301,-7.5 301,-7.5 452,-7.5 452,-7.5 458,-7.5 464,-13.5 464,-19.5 464,-19.5 464,-45.5 464,-45.5 464,-51.5 458,-57.5 452,-57.5"/>
<text text-anchor="start" x="308" y="-36.5" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">LAN utilisateurs</text>
<text text-anchor="start" x="314" y="-21.5" font-family="Helvetica,sans-Serif" font-size="15.00">postes de travail</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M363.98,-122.93C361.16,-106.53 360.75,-84.6 362.73,-66.56"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="365.86,-66.88 363.98,-57.54 359.62,-66.02 365.86,-66.88"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M797,-57.5C797,-57.5 516,-57.5 516,-57.5 510,-57.5 504,-51.5 504,-45.5 504,-45.5 504,-19.5 504,-19.5 504,-13.5 510,-7.5 516,-7.5 516,-7.5 797,-7.5 797,-7.5 803,-7.5 809,-13.5 809,-19.5 809,-19.5 809,-45.5 809,-45.5 809,-51.5 803,-57.5 797,-57.5"/>
<text text-anchor="start" x="557" y="-36.5" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Zone serveurs internes</text>
<text text-anchor="start" x="523" y="-21.5" font-family="Helvetica,sans-Serif" font-size="15.00">fichiers, base de données, annuaire</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M435.88,-122.93C480.61,-104.8 542,-79.91 588.67,-61"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="590.05,-63.84 597.2,-57.54 587.68,-58 590.05,-63.84"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M1085.5,-57.5C1085.5,-57.5 861.5,-57.5 861.5,-57.5 855.5,-57.5 849.5,-51.5 849.5,-45.5 849.5,-45.5 849.5,-19.5 849.5,-19.5 849.5,-13.5 855.5,-7.5 861.5,-7.5 861.5,-7.5 1085.5,-7.5 1085.5,-7.5 1091.5,-7.5 1097.5,-13.5 1097.5,-19.5 1097.5,-19.5 1097.5,-45.5 1097.5,-45.5 1097.5,-51.5 1091.5,-57.5 1085.5,-57.5"/>
<text text-anchor="start" x="910" y="-36.5" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">Administration</text>
<text text-anchor="start" x="868.5" y="-21.5" font-family="Helvetica,sans-Serif" font-size="15.00">postes d&#39;admin, supervision</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M456.04,-133.5C546.63,-117.92 699.01,-91.07 829.5,-65 838.34,-63.23 847.48,-61.36 856.66,-59.43"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="857.32,-62.51 865.47,-57.58 856.02,-56.35 857.32,-62.51"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M389.02,-57.54C391.83,-73.93 392.25,-95.86 390.28,-113.9"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="387.14,-113.58 389.02,-122.93 393.38,-114.45 387.14,-113.58"/>
</g>
</g>
</svg>
</figure>

| Zone | Contenu | Règles typiques |
|---|---|---|
| **Internet** (non sûre) | Le monde extérieur | Aucun accès direct au réseau interne |
| **DMZ** (zone démilitarisée) | Services **exposés** à Internet | Entrées limitées aux ports du service ; **pas d'accès libre** vers l'interne |
| **LAN utilisateurs** | Postes de travail | Sorties contrôlées ; accès aux serveurs limités |
| **Serveurs internes** | Données et services | Accessibles seulement depuis les zones qui en ont besoin |
| **Administration** | Postes et outils des administrateurs | Seuls ces postes administrent (SSH, RDP, supervision) |

Les zones se matérialisent par des **VLAN** et des sous-réseaux distincts, reliés par un routeur ou un pare-feu qui applique la **matrice de flux**.

### La matrice de flux

C'est un tableau qui dit **qui peut parler à qui, sur quel port**. Tout ce qui n'y figure pas est refusé.

| De ↓ / Vers → | Internet | DMZ | Serveurs | Administration |
|---|---|---|---|---|
| **Internet** | — | 443 (web) | ✗ | ✗ |
| **LAN** | 80, 443 | 443 | 445 (partage), 53 (DNS) | ✗ |
| **DMZ** | 53, mises à jour | — | 3306 (base, depuis le web seulement) | ✗ |
| **Administration** | ✔ | 22 | 22, 3389 | — |

Une matrice **courte et justifiée** est plus sûre qu'une liste de règles accumulées sans explication. Chaque ligne doit avoir un **propriétaire** et une **raison**.

### Quelques bonnes pratiques de réseau

- **Segmenter** l'accès Wi-Fi invités, les imprimantes, les objets connectés et les **équipements personnels** (BYOD) dans des zones à part.
- **Désactiver les ports inutilisés** des commutateurs et utiliser l'authentification 802.1X quand c'est possible.
- Un **bastion** (poste d'administration unique, journalisé) pour l'accès aux serveurs.
- **Superviser** le trafic entre zones (S15).

## III. Durcir un système

Le **durcissement** (*hardening*) consiste à **réduire la surface d'attaque** d'un système en le configurant au plus juste.

### Les familles de mesures

| Famille | Mesures |
|---|---|
| **Services et logiciels** | Ne garder que ce qui est nécessaire ; supprimer les services inutiles ; ports ouverts connus (`ss -tlnp`) |
| **Mises à jour** | Correctifs de sécurité appliqués rapidement (automatiques si possible) |
| **Comptes et accès** | Pas de connexion directe de `root` ; authentification par clé ; mots de passe forts ; comptes inutiles supprimés |
| **Pare-feu local** | Refus par défaut, ouverture des seuls ports utiles |
| **Journalisation** | Journaux activés, centralisés et horodatés (S15) |
| **Chiffrement** | Disques (S05), communications (TLS, SSH) |
| **Configuration de base** | Mêmes paramètres sur toutes les machines (modèle, automatisation) |

### SSH, la porte d'administration d'un serveur Linux

| Réglage | Valeur | Effet |
|---|---|---|
| `PermitRootLogin` | `no` | Pas de connexion directe en administrateur |
| `PasswordAuthentication` | `no` | Seulement par **clé** : plus de mot de passe à deviner |
| `PubkeyAuthentication` | `yes` | Authentification par clé publique |
| `MaxAuthTries` | `3` | Peu d'essais par connexion |
| `AllowUsers` | liste | Seuls les comptes cités peuvent se connecter |
| `X11Forwarding` | `no` | Moins de fonctionnalités exposées |

### Windows

Sous Windows, le durcissement se déploie par **stratégie de groupe** (GPO) : politique de mots de passe, verrouillage de compte, désactivation de **SMBv1** et d'anciens protocoles, restriction des administrateurs locaux, journalisation avancée, pare-feu activé, **AppLocker**/contrôle des applications. Les paramètres se rassemblent dans un **modèle de base** appliqué à toutes les machines d'un même type.

## IV. Les référentiels

On ne durcit pas « de mémoire » : on s'appuie sur des guides reconnus.

| Référentiel | Éditeur | Contenu |
|---|---|---|
| **Guide d'hygiène informatique** | ANSSI | Mesures de sécurité essentielles pour toute organisation |
| **Recommandations de configuration** (Linux, Windows, TLS, SSH, réseau…) | ANSSI | Guides techniques par sujet |
| **CIS Benchmarks** | Center for Internet Security | Listes détaillées de réglages par système, avec niveaux |
| **Lynis**, **OpenSCAP**, **audits de conformité** | Outils libres | Vérifient la configuration d'un système et proposent des améliorations |

> [!NOTE]
> Un référentiel est un **point de départ**, pas une liste à appliquer sans réfléchir : chaque réglage est évalué selon le **contexte** (exposition du serveur, impact sur les utilisateurs). On documente les **écarts assumés**.

## V. Durcir sans se couper l'accès

Quelques réflexes évitent les pannes de configuration :

1. Garder une **seconde session** ouverte avant de modifier SSH ou le pare-feu ;
2. **Tester** la configuration avant de recharger (`sshd -t`, `nginx -t`) ;
3. Ouvrir la règle d'accès (par exemple le port 22) **avant** d'activer le pare-feu ;
4. Garder une **console** hors réseau (console de la VM) pour le dépannage ;
5. Procéder par étapes, **une mesure à la fois**, et noter ce qui change.

## À retenir

- **Défense en profondeur**, **moindre privilège**, **cloisonnement**, **refus par défaut**.
- Zones : Internet, **DMZ**, LAN, serveurs, administration ; la **matrice de flux** liste ce qui est autorisé, le reste est refusé.
- Durcir = réduire la **surface d'attaque** : services, correctifs, comptes, SSH par clés, pare-feu local.
- S'appuyer sur les guides de l'**ANSSI** et les **CIS Benchmarks**, mesurer avec un outil (Lynis).
- Toujours pouvoir revenir en arrière : session de secours, test avant rechargement.
