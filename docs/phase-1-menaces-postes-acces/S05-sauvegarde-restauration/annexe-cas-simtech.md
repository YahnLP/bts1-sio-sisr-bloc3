# Annexe – Cas SimTech (fictif)

*BTS SIO SISR 1re année – Bloc 3 – S05 – support du [TP](02-tp.md)*

> [!NOTE]
> **SimTech SARL** est une entreprise **fictive**.

## Le contexte

- PME de **25 employés**, développement logiciel.
- Un serveur principal sous Windows Server : **500 Go** de données (code source, documents, bases de données).
- **5 à 10 Go** de données modifiées chaque jour.
- Les développeurs travaillent de 8 h à 19 h ; la sauvegarde ne doit pas ralentir le travail : **fenêtre de sauvegarde de 22 h à 6 h**.
- Budget alloué : **500 €** de matériel (une fois) et **50 € par mois** de stockage en ligne.
- Un seul administrateur, à mi-temps.

## Les besoins exprimés par la direction

| Donnée | Ce que dit la direction |
|---|---|
| Code source | « On ne peut pas perdre plus d'une journée de travail. » |
| Base de données de facturation | « Si la facturation est arrêtée plus d'une demi-journée, on perd des clients. » |
| Documents administratifs | « On peut attendre quelques jours. » |
| Obligations légales | Les factures doivent être conservées 10 ans (à confirmer par le service comptable). |

## Ordres de grandeur pour le chiffrage (à vérifier avant d'acheter)

| Élément | Ordre de prix indicatif |
|---|---|
| Disque dur externe de 2 To | 70 à 100 € |
| NAS 2 baies, sans disques | 200 à 300 € |
| Stockage en ligne objet (par To et par mois) | 5 à 15 € |

> [!WARNING]
> Ces prix sont des **ordres de grandeur d'exercice**, pas des devis : un administrateur relève toujours les prix réels du moment.
