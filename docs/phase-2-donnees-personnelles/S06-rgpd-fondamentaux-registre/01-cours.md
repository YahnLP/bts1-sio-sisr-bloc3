# Cours – RGPD : notions, acteurs, principes et registre des traitements

*BTS SIO SISR 1re année – Bloc 3 – S06 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S01 (confidentialité, intégrité) ; S04 (droits d'accès).
> - **Matériel :** VM Debian de laboratoire ; tableur ou traitement de texte ; modèle de registre (fourni en annexe)

## À la fin de ce cours tu sauras

- [ ] **Définir** donnée à caractère personnel, donnée sensible, traitement, responsable de traitement, sous-traitant et destinataire ;
- [ ] **Situer** les acteurs : CNIL, délégué à la protection des données (DPO), personne concernée ;
- [ ] **Énoncer** les principes de l'article 5 du RGPD et les **illustrer** sur des cas ;
- [ ] **Recenser** les traitements d'une organisation et **renseigner** un registre ;
- [ ] **Retrouver** des données personnelles dans un espace de stockage avec des recherches ciblées ;
- [ ] **Repérer** les écarts de conformité d'une situation décrite et **proposer** une mesure.

## I. Pourquoi le RGPD concerne un technicien

Un administrateur système voit passer des données de personnes : annuaire, messagerie, journaux de connexion, bases clients, paies. Le **Règlement général sur la protection des données** (RGPD, règlement (UE) 2016/679) est **applicable depuis le 25 mai 2018** dans toute l'Union européenne ; en France, il est complété par la **loi Informatique et Libertés** de 1978, modifiée. Il s'applique à toute organisation qui traite des données de personnes qui se trouvent dans l'Union, quelle que soit sa taille.

Le bloc 3 du BTS attend du technicien qu'il sache **recenser** les traitements, **identifier les risques**, **appliquer** la réglementation et **sensibiliser** les utilisateurs.

## II. Les notions de base

| Terme | Définition (d'après l'article 4) | Exemples |
|---|---|---|
| **Donnée à caractère personnel** | Toute information se rapportant à une personne physique **identifiée ou identifiable**, directement ou indirectement | Nom, courriel professionnel, numéro de téléphone, adresse IP, identifiant de compte, photo, plaque d'immatriculation |
| **Donnée sensible** (catégories particulières, article 9) | Données dont le traitement est en principe **interdit** sauf exception : origine raciale ou ethnique, opinions politiques, convictions religieuses ou philosophiques, appartenance syndicale, données génétiques, données biométriques pour identifier une personne, données de santé, vie sexuelle ou orientation sexuelle | Arrêt maladie, empreinte digitale pour le badge, adhésion syndicale |
| **Traitement** | **Toute opération** sur des données : collecte, enregistrement, organisation, conservation, consultation, utilisation, communication, rapprochement, effacement | Tenir un fichier clients, enregistrer les connexions, sauvegarder |
| **Personne concernée** | La personne à qui se rapportent les données | Salarié, client, candidat, visiteur |
| **Responsable de traitement** | Celui qui **détermine les finalités et les moyens** du traitement | L'entreprise qui gère sa paie |
| **Sous-traitant** | Celui qui traite les données **pour le compte** du responsable | L'hébergeur, l'éditeur d'un logiciel en ligne, le prestataire de maintenance |
| **Destinataire** | Celui qui reçoit communication des données | Un service interne, un organisme social |

> [!NOTE]
> Une donnée est **personnelle** dès qu'on peut **raisonnablement** remonter à une personne, même avec un effort ou en croisant d'autres informations. **Une adresse IP** est une donnée personnelle ; un journal de connexions d'un serveur est donc un traitement de données personnelles.

**Je vérifie.** Le journal du serveur web d'une PME contient l'adresse IP et l'heure de chaque visite. S'agit-il d'un traitement de données personnelles ? Qui en est le responsable ?

<details markdown="1">
<summary>Voir la réponse</summary>

Oui : l'adresse IP permet d'identifier indirectement la personne, et l'enregistrement et la conservation sont des opérations de **traitement**. Le **responsable** est l'entreprise qui exploite le site (elle détermine pourquoi et comment on journalise). Si l'hébergement est assuré par un prestataire, celui-ci est **sous-traitant**.

</details>

## III. Les acteurs

| Acteur | Rôle |
|---|---|
| **Le responsable de traitement** | Il est **responsable de la conformité** et doit pouvoir la démontrer |
| **Le sous-traitant** | Il agit sur instruction, assure la sécurité et aide le responsable (voir S08) |
| **Le délégué à la protection des données** (DPO, ou DPD) | Conseille, contrôle la conformité, fait le lien avec la CNIL ; sa désignation est **obligatoire** dans certains cas (organismes publics, suivi régulier et systématique de personnes à grande échelle, données sensibles à grande échelle), facultative mais recommandée sinon |
| **La CNIL** | Autorité française de contrôle : conseille, instruit les plaintes, contrôle, peut **sanctionner** |
| **Le Comité européen de la protection des données** (CEPD) | Coordonne les autorités nationales, publie des lignes directrices |
| **La personne concernée** | Elle a des **droits** (S07) et peut saisir la CNIL |

La CNIL peut prononcer des **amendes administratives** allant jusqu'à **20 millions d'euros ou 4 % du chiffre d'affaires annuel mondial** pour les manquements les plus graves (10 millions ou 2 % pour d'autres), ainsi que des mises en demeure, des limitations ou interdictions de traitement.

## IV. Les principes de l'article 5

| Principe | Idée | Illustration |
|---|---|---|
| **Licéité, loyauté, transparence** | Un fondement juridique, pas de collecte cachée | On informe les personnes de la collecte |
| **Limitation des finalités** | Une **finalité déterminée, explicite et légitime** ; on ne détourne pas | Les adresses collectées pour une livraison ne servent pas à du démarchage |
| **Minimisation** | Seules les données **nécessaires** | Inutile de demander la date de naissance pour une newsletter |
| **Exactitude** | Données à jour, rectifiées si besoin | Mise à jour d'une adresse |
| **Limitation de la conservation** | Pas plus longtemps que nécessaire | Purge des candidatures non retenues |
| **Intégrité et confidentialité** | Sécurité adaptée au risque | Droits d'accès, chiffrement, sauvegardes (S03 à S05) |
| **Responsabilité** (*accountability*, article 5.2) | Le responsable **démontre** sa conformité | Registre, documentation, preuves |

Le dernier principe est celui qui concerne le plus l'administrateur : **la conformité se prouve par des documents et des traces**, pas par des déclarations.

## V. Recenser : le registre des traitements

Le **registre des activités de traitement** (article 30) est un document qui décrit **chaque traitement** de l'organisation. En pratique, toute organisation qui traite des données personnelles de façon non occasionnelle doit en tenir un ; la CNIL fournit un modèle.

| Rubrique | Question |
|---|---|
| **Nom et finalité** | Pourquoi traite-t-on ces données ? |
| **Personnes concernées** | De qui ? (salariés, clients, candidats) |
| **Catégories de données** | Lesquelles ? Y a-t-il des données sensibles ? |
| **Destinataires** | Qui les reçoit ? Quels sous-traitants ? |
| **Transferts hors Union européenne** | Où sont-elles envoyées ? Avec quelle garantie ? |
| **Durée de conservation** | Combien de temps, et pourquoi ? |
| **Mesures de sécurité** | Droits d'accès, chiffrement, sauvegarde, journalisation |
| **Base légale** | Sur quel fondement ? (voir S07) |

Le registre se construit **à partir du système d'information** : on parcourt les applications, les serveurs, les partages, les sauvegardes, les journaux, les équipements (badgeuse, caméras) en se demandant à chaque fois : **quelles données de personnes ? pour quoi ? où ? combien de temps ? qui y accède ?** C'est un travail d'administrateur autant que de juriste.

### Retrouver les données là où elles sont

Les données personnelles ne sont pas seulement dans les bases « officielles » : elles se trouvent aussi dans des **fichiers en vrac** (feuilles de calcul, dossiers de partage, pièces jointes, exports). Des recherches par **motifs** permettent d'en repérer : adresses de courriel, numéros de téléphone, IBAN, numéros de sécurité sociale. C'est un outil d'**inventaire** et de **réduction du risque** : une donnée qu'on ne trouve pas ne peut pas être protégée.

**Je vérifie.** Un partage contient un tableur `export-clients-2019.xlsx` oublié par un ancien salarié. Que faire du point de vue du RGPD ?

<details markdown="1">
<summary>Voir la réponse</summary>

Identifier **qui en est propriétaire** et **à quoi il servait**, vérifier si la **finalité** existe encore et si la **durée de conservation** est dépassée ; si non, **supprimer** (ou archiver avec accès restreint). Dans tous les cas, ce fichier doit apparaître dans le registre ou être supprimé : un traitement **qu'on ignore** ne peut pas être sécurisé.

</details>

## À retenir

- Une **donnée personnelle** permet d'identifier une personne, directement ou indirectement (**adresse IP** comprise) ; les données **sensibles** sont interdites sauf exception.
- Le **responsable de traitement** décide pourquoi et comment ; le **sous-traitant** agit pour son compte.
- Sept principes : **licéité-loyauté-transparence, finalités, minimisation, exactitude, conservation limitée, intégrité-confidentialité, responsabilité**.
- Le **registre des traitements** est la pièce centrale de la **preuve de conformité**.
- Le technicien **recense** (applications, partages, journaux) et **protège**.
- Amendes possibles : jusqu'à **20 M€ ou 4 % du chiffre d'affaires mondial**.
