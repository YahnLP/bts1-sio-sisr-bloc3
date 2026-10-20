# S12 – Mini-PKI et site en HTTPS

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S12 (séance 12 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Parcours** | **Complément** – Mini-PKI et HTTPS en pratique : aucune séance ne s'appuie sur son TP ; les notions de certificat restent vues en S11. Voir le [parcours cœur et complément](../../ressources/parcours-coeur-complement.md). |
| **Prérequis** | S11 (certificats, chaîne de confiance, signature). |
| **Matériel** | VM Debian de laboratoire (`openssl`, `nginx`, `curl`) ; droits `sudo` |
| **Compétences travaillées** | B3.2 · B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment faire pour qu'un site interne soit en HTTPS sans avertissement, et comment diagnostiquer une erreur de certificat ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Créer** une autorité de certification interne et en **protéger** la clé privée ;
2. **Émettre** un certificat de serveur à partir d'une demande de signature (CSR) avec noms alternatifs ;
3. **Configurer** un serveur web en HTTPS et **faire reconnaître** l'autorité par un client ;
4. **Diagnostiquer** les trois erreurs courantes : nom, expiration, chaîne non reconnue ;
5. **Révoquer** un certificat, **publier** la liste de révocation et vérifier son effet.

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – Déployer des certificats : AC interne, serveur HTTPS et révocation](01-cours.md) | Cours |
| [TP – Construire une mini-PKI, publier un site en HTTPS et diagnostiquer les erreurs de certificat](02-tp.md) | TP |
| [Aide-mémoire – Mini-PKI et HTTPS](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S11) : que contient un certificat ? | Oral |
| 0 h 15 – 0 h 55 | **Cours** : AC interne, CSR, configuration TLS, erreurs, révocation | Cours et questions |
| 0 h 55 – 1 h 55 | **TP parties A et B** : autorité de certification et certificat de serveur | Binôme |
| 1 h 55 – 2 h 55 | **TP partie C** : site HTTPS avec nginx et confiance du client | Binôme |
| 2 h 55 – 3 h 40 | **TP parties D et E** : erreurs de certificat et révocation | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Fichiers de configuration, sorties de commandes et réponses aux questions, nommés `RENDU-B3-S12-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- Les commandes OpenSSL (création d'AC, émission, expiration forcée, révocation, CRL, vérification) ont été **testées** avec OpenSSL 3.0. La configuration nginx est standard mais **non exécutée** pendant la rédaction : à tester sur la VM de laboratoire.
- L'AC est à **un seul niveau** pour simplifier. Défi facultatif : ajouter une AC intermédiaire (voir le cours) et vérifier la chaîne à trois niveaux.
- Insister sur le **retrait** de l'AC de laboratoire du magasin de confiance en fin de séance.

</details>
