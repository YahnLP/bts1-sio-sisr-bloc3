# Cours – Réponse à incident : méthode, communication et preuves

*BTS SIO SISR 1re année – Bloc 3 – S17 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S05 (sauvegardes), S08 (violations), S09 (preuve, plainte), S15 (journaux).
> - **Matériel :** VM Debian de laboratoire ; fiches papier ou traitement de texte

## À la fin de ce cours tu sauras

- [ ] **Décrire** les phases d'une réponse à incident (préparation, détection, qualification, confinement, éradication, restauration, retour d'expérience) ;
- [ ] **Qualifier** un incident et décider des premières actions dans l'ordre ;
- [ ] **Identifier** qui prévenir (direction, DPO, CNIL, assureur, police, clients) et dans quel délai ;
- [ ] **Collecter** des informations volatiles avec un script et en garantir l'intégrité par une empreinte ;
- [ ] **Rédiger** une main courante et un retour d'expérience.

## I. Un incident, une méthode

Un **incident de sécurité** est un événement qui compromet ou menace la confidentialité, l'intégrité ou la disponibilité d'un système ou de données : rançongiciel, compte compromis, fuite, déni de service, perte d'un matériel. Face à la pression, on suit une **méthode** pour ne pas improviser.

<figure class="graphe diagramme">
<svg viewBox="0.00 0.00 309.60 626.60" style="max-width:413px" role="img" aria-label="Schéma" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<g class="graph" transform="scale(1 1) rotate(0) translate(10.8 615.8)">
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M276,-605C276,-605 100,-605 100,-605 94,-605 88,-599 88,-593 88,-593 88,-552 88,-552 88,-546 94,-540 100,-540 100,-540 276,-540 276,-540 282,-540 288,-546 288,-552 288,-552 288,-593 288,-593 288,-599 282,-605 276,-605"/>
<text text-anchor="start" x="139.5" y="-584" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">1. Préparer</text>
<text text-anchor="start" x="107" y="-569" font-family="Helvetica,sans-Serif" font-size="15.00">procédures, contacts,</text>
<text text-anchor="start" x="111" y="-554" font-family="Helvetica,sans-Serif" font-size="15.00">sauvegardes testées</text>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M180,-482C180,-482 68,-482 68,-482 62,-482 56,-476 56,-470 56,-470 56,-444 56,-444 56,-438 62,-432 68,-432 68,-432 180,-432 180,-432 186,-432 192,-438 192,-444 192,-444 192,-470 192,-470 192,-476 186,-482 180,-482"/>
<text text-anchor="start" x="75" y="-461" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">2. Détecter</text>
<text text-anchor="start" x="77" y="-446" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">et qualifier</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M170.17,-539.88C161.5,-524.5 151.08,-506.02 142.34,-490.52"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="144.84,-488.54 137.67,-482.25 139.35,-491.64 144.84,-488.54"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M198,-374C198,-374 12,-374 12,-374 6,-374 0,-368 0,-362 0,-362 0,-336 0,-336 0,-330 6,-324 12,-324 12,-324 198,-324 198,-324 204,-324 210,-330 210,-336 210,-336 210,-362 210,-362 210,-368 204,-374 198,-374"/>
<text text-anchor="start" x="57" y="-353" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">3. Contenir</text>
<text text-anchor="start" x="19" y="-338" font-family="Helvetica,sans-Serif" font-size="15.00">stopper la propagation</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M119.69,-431.95C117.11,-417.55 113.79,-399.04 110.96,-383.25"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="114.05,-382.63 109.36,-374.32 107.85,-383.74 114.05,-382.63"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M190.5,-266C190.5,-266 33.5,-266 33.5,-266 27.5,-266 21.5,-260 21.5,-254 21.5,-254 21.5,-228 21.5,-228 21.5,-222 27.5,-216 33.5,-216 33.5,-216 190.5,-216 190.5,-216 196.5,-216 202.5,-222 202.5,-228 202.5,-228 202.5,-254 202.5,-254 202.5,-260 196.5,-266 190.5,-266"/>
<text text-anchor="start" x="59.5" y="-245" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">4. Éradiquer</text>
<text text-anchor="start" x="40.5" y="-230" font-family="Helvetica,sans-Serif" font-size="15.00">supprimer la cause</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M106.59,-323.95C107.53,-309.68 108.74,-291.38 109.77,-275.69"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="112.94,-275.51 110.39,-266.32 106.66,-275.1 112.94,-275.51"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M195,-158C195,-158 37,-158 37,-158 31,-158 25,-152 25,-146 25,-146 25,-120 25,-120 25,-114 31,-108 37,-108 37,-108 195,-108 195,-108 201,-108 207,-114 207,-120 207,-120 207,-146 207,-146 207,-152 201,-158 195,-158"/>
<text text-anchor="start" x="63" y="-137" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">5. Restaurer</text>
<text text-anchor="start" x="44" y="-122" font-family="Helvetica,sans-Serif" font-size="15.00">reprendre l&#39;activité</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M112.91,-215.95C113.45,-201.68 114.14,-183.38 114.73,-167.69"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="117.89,-167.44 115.08,-158.32 111.59,-167.2 117.89,-167.44"/>
</g>
<g class="node n&#45;rect">
<path fill="none" stroke="black" stroke-width="1.8" d="M254,-50C254,-50 130,-50 130,-50 124,-50 118,-44 118,-38 118,-38 118,-12 118,-12 118,-6 124,0 130,0 130,0 254,0 254,0 260,0 266,-6 266,-12 266,-12 266,-38 266,-38 266,-44 260,-50 254,-50"/>
<text text-anchor="start" x="152" y="-29" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">6. Retour</text>
<text text-anchor="start" x="137" y="-14" font-family="Helvetica,sans-Serif" font-weight="bold" font-size="15.00">d&#39;expérience</text>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M133.25,-107.95C143.86,-93.14 157.59,-73.99 169.11,-57.93"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="171.88,-59.47 174.56,-50.32 166.76,-55.8 171.88,-59.47"/>
</g>
<g class="edge">
<path fill="none" stroke="black" stroke-width="1.8" d="M207.42,-50.28C230.41,-88.89 271,-167.33 271,-240 271,-350 271,-350 271,-350 271,-417.13 237.16,-488.84 212.69,-531.91"/>
<polygon fill="black" stroke="black" stroke-width="1.8" points="209.87,-530.51 208.09,-539.87 215.32,-533.66 209.87,-530.51"/>
</g>
</g>
</svg>
</figure>

| Phase | Objectif | Exemples |
|---|---|---|
| **Préparer** | Être prêt avant | Liste des contacts, procédure écrite, sauvegardes hors ligne et **testées** (S05), journaux (S15) |
| **Détecter et qualifier** | Savoir ce qui se passe | Alerte, signalement d'un utilisateur ; **périmètre**, **gravité**, données touchées ? |
| **Contenir** | Limiter les dégâts | Isoler les machines du réseau, couper les comptes compromis, bloquer l'adresse malveillante |
| **Éradiquer** | Supprimer la cause | Retirer le logiciel malveillant, corriger la faille, changer les mots de passe |
| **Restaurer** | Reprendre | Restaurer depuis une sauvegarde **saine**, vérifier, surveiller de près |
| **Retour d'expérience** | Apprendre | Réunion, rapport, actions d'amélioration |

> [!NOTE]
> Avant de **restaurer**, il faut **éradiquer** : restaurer sur un système encore compromis, c'est se faire attaquer à nouveau.

## II. Les premières heures

### Qui fait quoi ?

| Rôle | Mission |
|---|---|
| **Responsable de crise** (direction) | Décide, arbitre, porte la responsabilité |
| **Pilote technique** | Coordonne l'analyse et les actions |
| **Techniciens** | Exécutent (isolement, collecte, restauration) |
| **DPO** | Évalue l'atteinte aux données personnelles (S08) |
| **Communication** | Informe clients, partenaires, salariés |
| **Scribe** | Tient la **main courante** (qui, quoi, quand) |

Même dans une petite structure, on **désigne** ces rôles : un administrateur seul ne peut pas à la fois réparer, décider et communiquer.

### La main courante

Un journal **horodaté** de tout ce qui est constaté et décidé : « 08:25 – 3 postes affichent un message de rançon ; décision de couper le réseau (J. Martin) ». Elle sert à comprendre, à rendre compte, à prouver et à faire le retour d'expérience.

### Réflexes face à un rançongiciel

| À faire | À éviter |
|---|---|
| **Isoler** les machines touchées du réseau (câble, Wi-Fi) | Éteindre sans réfléchir : on perd la mémoire vive (indices), mais cela peut aussi stopper un chiffrement en cours : **décision** à prendre en connaissance de cause |
| **Préserver** les sauvegardes (les débrancher ou les isoler avant qu'elles ne soient chiffrées) | Se connecter avec un compte administrateur sur une machine infectée |
| **Prévenir** la direction et le contact sécurité | Supprimer ou « nettoyer » avant d'avoir collecté les preuves |
| **Noter** l'heure et les symptômes | Payer la rançon sans analyse : le paiement ne garantit ni la restitution ni l'absence de revente des données, et finance les attaquants. Les autorités déconseillent de payer |
| **Déposer plainte** | Communiquer sur le sujet avant d'avoir qualifié les faits |

## III. Qui prévenir ?

| Destinataire | Quand | Pourquoi |
|---|---|---|
| **Direction** | Tout de suite | Décision, ressources |
| **DPO / responsable données** | Tout de suite | Violation de données ? (S08) |
| **CNIL** | Sous **72 h** si des données personnelles sont touchées avec un risque | Obligation légale (S08) |
| **Personnes concernées** | Si le risque pour elles est **élevé** | Obligation légale (S08) |
| **Assureur** (cyber) | Dans les délais du contrat | Prise en charge, experts |
| **Police ou gendarmerie** | Rapidement | Plainte : nécessaire pour l'assurance et l'enquête |
| **ANSSI / CERT-FR** | Selon le statut de l'organisation (opérateurs essentiels, entités réglementées) | Obligations sectorielles, appui |
| **Cybermalveillance.gouv.fr** | Pour les entreprises et collectivités victimes | Diagnostic, mise en relation avec des prestataires |
| **Clients, partenaires** | Après qualification et décision de la direction | Transparence, éviter la propagation |

## IV. La préservation des preuves

Pour qu'une trace serve en justice ou auprès de l'assurance, elle doit être **authentique** et **intègre** (S09). Les règles :

1. **Ne pas altérer** : travailler sur des **copies**, jamais sur l'original quand c'est possible.
2. **Respecter l'ordre de volatilité** : collecter d'abord ce qui disparaît le plus vite.
3. **Garantir l'intégrité** : calculer l'**empreinte SHA-256** de chaque élément collecté (S10).
4. **Documenter** : qui a collecté, quand, comment, avec quel outil.
5. **Conserver la chaîne** de possession : où est la preuve, qui l'a manipulée.
6. **Stocker** les preuves sur un support **externe** à la machine analysée.

| Ordre de volatilité | Exemple | Commande Linux |
|---|---|---|
| 1. Mémoire, état du système | Connexions réseau, processus, utilisateurs connectés | `ss -tupan`, `ps`, `who` |
| 2. Fichiers temporaires | `/tmp`, caches | `ls -la /tmp` |
| 3. Disque | Fichiers, journaux | Copie du disque, `journalctl` |
| 4. Journaux distants et sauvegardes | Serveur de journaux, pare-feu | Export, copie |

> [!WARNING]
> Un administrateur qui « nettoie » une machine avant la collecte détruit des preuves. Dans le doute : **isoler, collecter, puis agir**.

## V. Le retour d'expérience

Après la crise, une réunion (sans recherche de coupable) répond à : que s'est-il passé ? comment l'a-t-on détecté ? qu'a-t-on bien/mal fait ? quelle a été la cause racine ? Quelles **actions** pour que cela ne se reproduise pas (avec un responsable et une échéance) ?

## À retenir

- Méthode : **préparer → détecter/qualifier → contenir → éradiquer → restaurer → retour d'expérience**.
- Désigner des **rôles** et tenir une **main courante** horodatée.
- Rançongiciel : **isoler**, préserver les sauvegardes, **ne pas payer sans analyse**, collecter les preuves.
- Prévenir : direction, DPO, **CNIL sous 72 h** si données touchées, assureur, police, selon le cas.
- Preuves : **copies**, **ordre de volatilité**, **empreintes**, documentation, chaîne de possession.
