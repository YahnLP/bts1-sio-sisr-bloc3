# Corrigé S09

## Partie A

**A1.** Critères appliqués : 1 (score), 3 (suivi continu et géolocalisation), 4 (santé, géolocalisation), 5 (30 000 patients), 7 (patients, personnes âgées), 8 (apprentissage automatique). Le 2 est discutable (le score recommande, il ne décide pas seul) ; 6 et 9 non démontrés. **AIPD obligatoire.**

**A2.**

| Point | Évaluation | Action |
|---|---|---|
| Base légale | **Non conforme** : un consentement global pour des finalités différentes n'est pas spécifique ; la statistique pour des laboratoires n'est pas nécessaire au soin | Séparer : soin (base adaptée), alertes ; **consentement distinct** pour l'amélioration du score et pour les statistiques |
| Minimisation | Partiel | Géolocalisation **uniquement lors d'une alerte** ou à la demande du patient |
| Durée | **Non conforme** | Fixer une durée justifiée (et prévoir la suppression au retrait de l'application) |
| Droits | **Non conforme** | Procédure de demande, opposition au score, intervention humaine |
| Sous-traitance | **Non conforme** | Contrats (article 28), vérification des transferts hors UE et de leurs garanties |

**A3.** (exemples de valeurs ; l'essentiel est la justification)

| Événement | Sources | G | V | Score | Mesures | Résiduel |
|---|---|---|---|---|---|---|
| Accès illégitime | Mot de passe patient seul, sauvegardes non chiffrées, compte médecin volé | 4 | 3 | 12 | **MFA patient**, chiffrement des sauvegardes, alerte sur export, droits minimaux | 4 × 2 = 8 |
| Modification non désirée | Compte compromis, erreur d'intégration capteur | 3 | 2 | 6 | Journalisation, contrôle d'intégrité, validation médicale du score | 3 × 1 = 3 |
| Disparition | Rançongiciel, erreur d'administration | 3 | 2 | 6 | Sauvegardes 3-2-1 testées (S05), plan de reprise | 3 × 1 = 3 |

1. Les données de santé révèlent des informations très intimes et durables ; une fuite peut entraîner discrimination, atteinte à la vie privée, pression : les conséquences peuvent être irréversibles.
2. **Vraisemblance** : MFA, droits minimaux, chiffrement, alertes. **Gravité** : minimisation, pseudonymisation, durées courtes.
3. Un risque résiduel de 8 (moyen) peut être jugé acceptable avec le plan d'action et l'avis du DPO ; si un risque **élevé** persiste malgré les mesures, la **consultation préalable de la CNIL** est obligatoire.

**A4.** Exemple : MFA patient (RSSI, 2 mois) ; chiffrement des sauvegardes (admin, 1 mois) ; contrats avec les sous-traitants (juridique, 1 mois) ; séparation des consentements et procédure de droits (DPO, 2 mois) ; durées de conservation et purge (admin, 3 mois).

## Partie B

| Point | Type | Preuves | Réaction immédiate | Durable |
|---|---|---|---|---|
| 1 | Typosquatting / contrefaçon | Captures datées, URL, whois, commandes reçues | Signaler au **bureau d'enregistrement** et à l'hébergeur ; prévenir les clients | Surveillance de domaines proches, enregistrement de variantes |
| 2 | Usurpation d'expéditeur / fraude au virement | **En-têtes complets** du message, copies des messages | Informer les clients ; vérifier la messagerie ; plainte | **SPF, DKIM, DMARC** ; procédure de vérification par un second canal des changements d'IBAN |
| 3 | Faux compte (usurpation d'identité numérique, 226-4-1) | Captures, URL du profil | Signalement à la plateforme | Compte officiel certifié, mention sur le site |
| 4 | Droit à l'image, donnée personnelle | Captures du site | Demande de retrait ; informer la salariée | Procédure d'autorisation pour toute photo |

4. Le faux site : bureau d'enregistrement et hébergeur ; le faux compte : plateforme ; escroquerie : **Thésée** / plainte ; assistance : **Cybermalveillance.gouv.fr** ; données personnelles : **CNIL** si fuite.
5. Pour éviter que d'autres clients paient ou donnent des données : le préjudice augmente avec le temps.
6. L'enregistrement **SPF** (de type TXT), complété par **DKIM** (signature) et **DMARC** (politique).

## Partie C

| # | Licite ? | Qualification | Bonne pratique |
|---|---|---|---|
| 1 | **Non** | Accès frauduleux (323-1) : pas d'autorisation, même avec un mot de passe disponible | Ne jamais utiliser des identifiants qui ne sont pas les siens ; demander une autorisation écrite |
| 2 | **Non** (sans autorisation) | Risque d'accès ou d'entrave selon l'effet (323-1, 323-2) ; l'intention n'efface pas l'infraction | S'entraîner sur son **labo isolé** ; obtenir une autorisation écrite |
| 3 | **Discutable, plutôt non** | Les fichiers identifiés « personnel » ne s'ouvrent pas en l'absence du salarié, sauf risque ou événement particulier ; atteinte à la vie privée | Prévenir le salarié, ouvrir en sa présence, ou le justifier par un risque grave et le documenter |
| 4 | **Non** | Maintien frauduleux (323-1) et extraction de données (323-3) ; atteinte au secret des affaires | **Désactiver** les accès au départ (S04) ; journaliser ; alerter la direction |

7. L'absence d'**autorisation** ou le dépassement de celle-ci : on sait ou on doit savoir qu'on n'a pas le droit.
8. La **charte informatique**, annexée au règlement intérieur.
