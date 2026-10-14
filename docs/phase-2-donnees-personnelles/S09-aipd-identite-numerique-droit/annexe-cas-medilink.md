# Annexe – Cas MediLink (fictif)

*La société, l'application et les chiffres sont **inventés**.*

**MediLink SAS** (80 salariés) développe une application mobile de **suivi du diabète**. Le patient saisit ou transmet automatiquement, depuis un capteur de glycémie, ses mesures. Son médecin suit les courbes et reçoit des alertes. Un module d'**analyse automatique** attribue à chaque patient un **score de risque** (faible, moyen, élevé) et recommande une consultation.

## Description du traitement

| Rubrique | Détail |
|---|---|
| Responsable de traitement | MediLink SAS ; un DPO est désigné |
| Personnes concernées | Environ **30 000 patients** adultes, dont des personnes âgées ; 800 médecins |
| Données | Identité, date de naissance, courriel, **mesures de glycémie**, traitements, **score de risque**, géolocalisation du téléphone (pour les alertes d'urgence) |
| Finalités | 1. Suivi médical par le médecin ; 2. Alertes d'urgence ; 3. **Amélioration du score** par apprentissage automatique ; 4. Statistiques pour des laboratoires partenaires |
| Base légale annoncée | Consentement du patient (case à l'inscription) pour les finalités 1 à 4, en une seule fois |
| Hébergement | Serveurs d'un hébergeur de données de santé certifié, en France |
| Sous-traitants | Hébergeur ; prestataire d'envoi de SMS (hors UE) ; éditeur du module d'analyse (États-Unis) |
| Durée de conservation | « Tant que l'application est installée » ; aucune purge |
| Mesures existantes | Connexion HTTPS ; mot de passe seul pour les patients ; **double authentification** pour les médecins ; base de données chiffrée au repos ; journalisation des accès des médecins |
| Mesures absentes | Pas de MFA patient ; pas de chiffrement des sauvegardes ; pas de contrat de sous-traitance avec le prestataire de SMS ; aucune alerte sur l'export de données |
| Droits des personnes | Un formulaire de contact, sans procédure ; pas de possibilité de s'opposer au score |

## Mission

Le DPO te demande d'évaluer si une AIPD est nécessaire, puis d'en conduire une version réduite.
