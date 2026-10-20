# Parcours « cœur » et « complément »

Les 19 séances de 4 h représentent **76 h** par an. Le volume prévu pour ce bloc en première année dans la grille sous statut scolaire est de **120 h** (2 × 60 h, annexe III.A du référentiel) : le parcours en apprentissage en offre environ les deux tiers. Quand le temps manque, ce parcours indique **quelles séances garder en priorité**.

> [!NOTE]
> Il ne retire rien du site : chaque séance reste disponible, et son statut est rappelé dans sa fiche.

## Pourquoi un seul complément

Le bloc est conçu comme une **chaîne** : la phase 2 (données personnelles) alimente S17, la phase 3 (chiffrement et réseau) alimente S14 à S16, et S16 et S17 reprennent S05, S08, S09, S14 et S15. Presque chaque séance est soit la seule à porter un savoir de l'épreuve E7, soit le prérequis d'une autre. Une seule séance peut être sautée sans casser le reste : **S12**.

## Principe

Une séance est **cœur** si l'une au moins de ces conditions est vraie :

1. elle est la **seule** à porter une compétence ou un savoir du bloc ;
2. elle est un **prérequis** d'une autre séance cœur (le site l'indique dans chaque fiche) ;
3. elle prépare directement **l'épreuve E7** (S18 et S19).

Sinon elle est **complément** : utile, mais le reste de la progression se déroule sans elle, à condition de lire la consigne ci-dessous.

## Résultat

- **18 séances cœur** (72 h) ;
- **1 séance complément** (4 h) : S12.

| Séance | Thème | Parcours | Pourquoi |
|---|---|---|---|
| S01 | Menaces et hygiène numérique | **Cœur** | Menaces, risque et hygiène numérique : prérequis de S02, S03 et S05. |
| S02 | Logiciels malveillants et protection du poste | **Cœur** | Logiciels malveillants et défense en profondeur : seule séance sur le poste (B3.3, B3.5A) ; S03 en reprend les notions. |
| S03 | Authentification : mots de passe et MFA | **Cœur** | Authentification et MFA : prérequis de S04, S10 (empreintes) et S15 (force brute). |
| S04 | Droits d'accès et moindre privilège | **Cœur** | Droits et moindre privilège : prérequis de S05, S06 et S14. |
| S05 | Sauvegarde, supports amovibles et restauration | **Cœur** | Sauvegarde et restauration : prérequis de S10 et S17 ; seule séance sur ce point. |
| S06 | RGPD : notions, acteurs, principes et registre des traitements | **Cœur** | RGPD et registre : B3.1 ; prérequis de S07 à S09. |
| S07 | Collecte, consentement et droits des personnes | **Cœur** | Consentement et droits des personnes : seule séance sur ce point (B3.1) ; prérequis de S08. |
| S08 | Conservation, sécurité, sous-traitance et violations de données | **Cœur** | Conservation, sécurité et violations : prérequis de S09 et S17. |
| S09 | AIPD, identité numérique et responsabilités juridiques | **Cœur** | AIPD, identité numérique et responsabilités juridiques : prérequis de S16 (autorisation, infractions) et S17 (preuve, plainte). |
| S10 | Chiffrement symétrique, hachage et intégrité | **Cœur** | Chiffrement symétrique et hachage : prérequis de S11 et S13. |
| S11 | Chiffrement asymétrique, signature et certificats | **Cœur** | Asymétrique, signature, certificats : prérequis de S13 et de S14 ; couvre la chaîne de confiance. |
| S12 | Mini-PKI et site en HTTPS | **Complément** | Mini-PKI et HTTPS en pratique : aucune séance ne s'appuie sur son TP ; les notions de certificat restent vues en S11. |
| S13 | VPN : protéger les échanges entre sites et utilisateurs nomades | **Cœur** | VPN : seule séance sur ce point, et prérequis de S14. |
| S14 | Architecture sécurisée et durcissement des systèmes | **Cœur** | Architecture et durcissement : prérequis de S15 et S16. |
| S15 | Journaux, détection et réaction automatique | **Cœur** | Journaux et détection : prérequis de S16 et S17. |
| S16 | Audit de vulnérabilités | **Cœur** | Audit de vulnérabilités : seule séance sur ce point (B3.4, B3.5A). |
| S17 | Gérer un incident de sécurité et préserver les preuves | **Cœur** | Incident et preuves : réutilise S05, S08, S09 et S15 ; prépare l'étude de cas. |
| S18 | Méthode de l'étude de cas E7 | **Cœur** | Méthode de l'étude de cas E7 : prépare directement l'épreuve. |
| S19 | Épreuve blanche E7 (4 h) | **Cœur** | Épreuve blanche E7. |

## Les compétences restent couvertes

Compétences travaillées par les séances cœur (S18 et S19, qui entraînent à toutes, ne sont pas comptées) :

| Compétence | Séances cœur | Nombre |
|---|---|---|
| B3.1 | S06, S07, S08, S09 | 4 |
| B3.2 | S09, S10, S11, S17 | 4 |
| B3.3 | S01, S02, S03, S04, S05, S14 | 6 |
| B3.4 | S01, S04, S05, S08, S10, S11, S13, S14, S15, S16, S17 | 11 |
| B3.5A | S02, S10, S11, S13, S14, S15, S16, S17 | 8 |

## Si l'on saute S12

- Les notions (certificat, chaîne de confiance, signature) sont vues en **S11**.
- Ce qui disparaît : la création pratique d'une autorité interne, la configuration HTTPS de nginx, le diagnostic des trois erreurs de certificat (nom, expiration, chaîne) et la révocation. Ces points peuvent être demandés dans une étude de cas : donner à lire le **cours** et l'**aide-mémoire** de S12 (environ 1 h), sans le TP.
- Aucune autre séance ne réutilise le contenu de S12. La fiche de S14 cite « S11 à S13 » comme prérequis, mais seuls les notions TLS de S11 et le VPN de S13 y servent ; S16 installe son propre nginx.

## Pour aller plus loin si le temps manque encore

Un seul complément libère 4 h. Au-delà, il faut alléger **à l'intérieur** des séances cœur (par exemple ne faire que certaines parties d'un TP) ou regrouper des séances. Les séances S16 et S17, qui rassemblent des briques de tout le bloc, sont les plus délicates à toucher.

## Utilisation

- Si **toutes** les séances sont faites, rien ne change.
- Si le temps manque, retirer d'abord S12 en appliquant la consigne ci-dessus.
- Les prérequis écrits dans chaque fiche ont été relus pour que ce classement ne casse aucune dépendance entre séances cœur.
