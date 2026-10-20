# Corrigé S06

## Partie A (éléments)

| Rubrique | Paie | Recrutement | Journaux |
|---|---|---|---|
| Finalité | Payer les salariés, obligations ​sociales | Sélectionner des candidats | Sécurité et diagnostic du système |
| Base légale | Exécution du contrat ; obligation légale | Mesures précontractuelles ; intérêt légitime | Intérêt légitime (sécurité) ; obligation légale pour certains journaux |
| ​Personnes | Salariés | Candidats | Visiteurs du site, salariés |
| Données | Identité, adresse, NIR, IBAN, salaire, arrêts | CV, lettre, coordonnées | Adresses IP, horodatage |
| Sensibles ? | Arrêts maladie : oui (santé) ; le NIR n'est pas une donnée de l'article 9 mais est très encadré | Non en principe | Non |
| Destinataires | DRH, comptable, éditeur (sous-traitant), organismes sociaux | DRH, éditeur | ​Administrateurs |
| Conservation | Durées légales (à confirmer avec le service juridique) | Quelques mois à deux ans après le dernier contact (la CNIL recommande de ne pas conserver indéfiniment ; à vérifier) | Durée à fixer et à justifier (la CNIL préconise de ne pas conserver sans limite) |
| Écarts | Contrat de sous-traitance à ​vérifier | Durée « tant que le logiciel est utilisé » | Aucune purge |

## Partie A questions

1. Le NIR n'est pas dans la liste de l'article 9 mais bénéficie d'un régime strict. Les arrêts maladie sont des données de **santé**, donc sensibles.
2. Responsable : InnoTech. Sous-traitant : l'éditeur du logiciel de paie. Lien : un **contrat de sous-traitance** (article 28).
3. Oui : nom + heures d'entrée et sortie. Finalité : sécurité des locaux ; durée courte ; éviter de l'utiliser pour ​surveiller le temps de travail sans information.

## Partie B

| Fichier | Données | Catégorie |
|---|---|---|
| `clients-2019.csv` | noms, courriels, téléphones | ordinaire |
| `notes-appel.txt` | un nom, un courriel, un téléphone | ordinaire |
| `arrets.txt` | **arrêt maladie** | **sensible (santé)** |
| `fiche-paie-modele.txt` | **NIR**, IBAN, nom | ​ordinaire, très encadrée |
| `virements-fournisseurs.txt` | IBAN d'entreprises, courriel générique | non personnelles, sauf entreprise individuelle |

Questions : (1) ça dépend si le fournisseur est une **personne physique** (entrepreneur individuel) ou une société ; (2) la ​supprimer ou l'archiver avec accès restreint si la durée de conservation est dépassée ; (3) un fichier hors registre, sans durée, accessible à beaucoup de monde, donne lieu à des fuites sans que personne ne le sache.

## Partie C

Non-conformités possibles : **mails non chiffrés** de données de santé (intégrité et confidentialité) ; **NAS sans ​chiffrement ni sauvegarde** (sécurité, disponibilité) ; **données de santé sans mesures renforcées** (article 9) ; éventuellement absence de contrat avec l'éditeur et d'information des patients.
