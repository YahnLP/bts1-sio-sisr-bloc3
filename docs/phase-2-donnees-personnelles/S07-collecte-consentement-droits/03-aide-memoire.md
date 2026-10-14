# Aide-mémoire – Collecte, consentement et droits

*BTS SIO SISR 1re année – Bloc 3 – S07*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les six bases légales (article 6)

| Base | Exemple |
|---|---|
| **Consentement** | Newsletter, cookies de publicité |
| **Contrat** | Livraison d'une commande, paie d'un salarié |
| **Obligation légale** | Conservation des factures, déclarations sociales |
| **Sauvegarde des intérêts vitaux** | Urgence médicale |
| **Mission d'intérêt public** | Service public |
| **Intérêt légitime** | Sécurité du SI, prévention de la fraude (avec mise en balance) |

## Consentement valide

**Libre · spécifique · éclairé · univoque.** Pas de case pré-cochée, une finalité = un choix, retrait **aussi simple** que le don, preuve conservée.

## Mentions d'information

Identité du responsable · finalités · base légale · destinataires · durée · droits · contact (DPO) · droit de réclamation auprès de la **CNIL**.

## Cookies

| Type | Consentement préalable ? |
|---|---|
| Strictement nécessaires (panier, session, sécurité) | Non |
| Mesure d'audience (selon conditions CNIL), publicité, réseaux sociaux | **Oui** (sauf exemptions précises) |

« Refuser » doit être aussi simple et visible que « Accepter ».

## Droits et délai

Accès · rectification · effacement · limitation · portabilité · opposition · décision automatisée. Réponse **sous un mois** (prolongeable de deux mois si complexe, en informant la personne).

## Commandes SQLite utiles

| But | Commande |
|---|---|
| Extraire en CSV | `sqlite3 -header -csv base.db "SELECT … WHERE …;"` |
| Extraire en JSON | `sqlite3 -json base.db "SELECT …;"` |
| Anonymiser | `UPDATE t SET nom='ANONYME', email=NULL WHERE id=…;` |

> [!WARNING]
> Une demande d'accès : **vérifier l'identité** avant de répondre, ne livrer **que** les données du demandeur, chercher dans **tous** les systèmes (y compris sauvegardes), **tracer** la demande.
