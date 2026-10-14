# Annexe – Le système d'information d'InnoTech et modèle de registre

*BTS SIO SISR 1re année – Bloc 3 – S06 – support de la partie A du [TP](02-tp.md)*

> [!NOTE]
> **InnoTech SARL** (30 salariés) est une entreprise **fictive**, déjà rencontrée en S04.

## Ce que l'administrateur découvre en parcourant le système d'information

| Élément | Description |
|---|---|
| **Logiciel de paie** (en ligne, éditeur externe) | Nom, adresse, numéro de sécurité sociale, IBAN, salaire, arrêts maladie des 30 salariés ; accès : DRH et comptable |
| **Logiciel de recrutement** (en ligne, éditeur externe) | CV, lettres de motivation, coordonnées des candidats ; conservé « tant que le logiciel est utilisé » |
| **Outil de gestion de la relation client** | Nom, courriel, téléphone et historique d'échanges des contacts des clients ; accès : service commercial |
| **Annuaire Active Directory et messagerie** | Identifiants, noms, courriels, appartenance aux groupes des 30 salariés |
| **Journaux du pare-feu et du serveur web** | Adresses IP, dates et heures de connexion ; conservés indéfiniment faute de purge |
| **Système de badges du bâtiment** | Nom du salarié, heures d'entrée et de sortie ; badge sans contact simple |
| **Sauvegarde quotidienne** | Copie chiffrée de tous les serveurs, conservée 30 jours |
| **Serveur de fichiers** | Dossiers de service (S04), dont des fichiers anciens non rangés |

## Modèle de fiche de registre (une fiche par traitement)

```text
Nom du traitement : ................................................
Finalité : .........................................................
Base légale : ......................................................
Personnes concernées : .............................................
Catégories de données (dont données sensibles ?) : .................
Destinataires et sous-traitants : ..................................
Transfert hors Union européenne : (non / oui : où, quelle garantie) ...
Durée de conservation (et justification) : .........................
Mesures de sécurité : ..............................................
```
