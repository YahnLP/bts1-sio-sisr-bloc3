# Annexe – Cas de violation MédiaGroup (fictif)

*Entreprise, personnes, adresses et chiffres sont **inventés**.*

**MédiaGroup** est une société fictive de 120 salariés qui édite un site d'actualités locales avec un espace abonné. Elle sert environ **12 000 abonnés**.

## Chronologie

| Moment | Événement |
|---|---|
| Lundi 08 h 30 | Un salarié de l'assistance signale que le site est lent. |
| Lundi 10 h 15 | L'administrateur système constate des **exportations massives** de la table `abonnes` depuis un compte d'application, vers une adresse IP étrangère. |
| Lundi 10 h 40 | Le compte est désactivé ; l'accès est coupé. L'administrateur prévient le DPO. |
| Lundi 11 h 00 | Début de l'analyse : l'attaquant est entré par une **injection SQL** sur un formulaire de recherche, présente depuis une mise à jour de **trois semaines**. |

## Données de la table `abonnes`

| Champ | Contenu | Protection |
|---|---|---|
| nom, prénom | Identité | En clair |
| email | Courriel | En clair |
| adresse postale | Adresse | En clair |
| date de naissance | Date | En clair |
| mot de passe | Mot de passe | Hachage **MD5 sans sel** |
| numéro de carte bancaire | **Non stocké** (traité par un prestataire de paiement) | — |

Le nombre de lignes exportées est de **12 000 environ**. Les journaux montrent des exportations sur **trois jours**.

## Éléments connus

- L'entreprise dispose d'un DPO à temps partiel.
- Le site est hébergé chez un prestataire (sous-traitant) lié par un contrat.
- Aucune alerte n'avait été configurée sur les exportations.
- Une sauvegarde de la veille est saine.

## Rappel

Cette annexe est un exercice : tout rapprochement avec une entreprise réelle serait fortuit.
