---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
# AIPD / PIA — Définition, Méthode, Évaluation des Risques

## Définition (Art. 35 RGPD)

Avant de lancer un traitement à risque élevé, démontrer systématiquement quon maîtrise les risques.

Analogie : Comme une étude dimpact environnementale avant de construire une autoroute.
→ Identifier les zones protégées, proposer des mesures, décider si on peut construire.
→ Identifier les risques RGPD, proposer des mesures de sécurité, décider si on peut lancer.

## Les 9 Critères Déclencheurs (2 critères = AIPD obligatoire)

① Évaluation ou scoring (profilage, notation)
② Décision automatisée avec effet significatif
③ Surveillance systématique (monitoring, CCTV, GPS)
④ Données sensibles ou hautement personnelles (santé, biométrie...)
⑤ Grande échelle (beaucoup de personnes)
⑥ Croisement ou combinaison de données (plusieurs sources)
⑦ Personnes vulnérables (enfants, patients, détenus, employés)
⑧ Usage innovant / nouvelles technologies (IA, IoT, reconnaissance faciale)
⑨ Transferts hors UE vers pays sans niveau adéquat

→ 2 critères ou plus = AIPD OBLIGATOIRE
→ 0 critère = AIPD non requise (documenter quand même dans le registre)

## La Méthode CNIL en 4 Étapes

ÉTAPE 1 → Décrire le traitement
ÉTAPE 2 → Apprécier la nécessité et la proportionnalité
ÉTAPE 3 → Identifier et évaluer les risques
ÉTAPE 4 → Valider lAIPD

### Étape 1 — Décrire le Traitement

Contenu :
A. Contexte général (RT, DPO, sous-traitants, secteur)
B. Finalités et bases légales pour chaque finalité
C. Données et personnes concernées (catégories, sensibles ?, nombre, vulnérables ?)
D. Processus et flux de données (collecte, stockage, accès, circulation, suppression)
E. Supports techniques (infra, apps, protocoles, mécanismes existants)

### Étape 2 — Nécessité et Proportionnalité

Vérifier grille de conformité Art. 5 :
- Finalités : déterminées, explicites, légitimes ? Base légale ?
- Droits : personnes informées ? Peuvent exercer leurs droits ? Consentement valide ?
- Durées : conservation définie et proportionnelle ? Procédure de purge ?
- Sous-traitants : contrats Art. 28 signés ? Garanties suffisantes ? Transferts hors UE encadrés ?

### Étape 3 — Identifier et Évaluer les Risques

3 types de risques sur la vie privée :
① ACCÈS ILLÉGITIME → Atteinte à la confidentialité
   (intrusion externe, accès interne non autorisé, vol matériel, interception réseau)
② MODIFICATION NON DÉSIRÉE → Atteinte à lintégrité + disponibilité
   (malware, erreur humaine, injection SQL, ransomware)
③ DISPARITION → Atteinte à la disponibilité
   (panne matérielle sans sauvegarde, catastrophe, faillite sous-traitant)

### La Grille de Cotation : Vraisemblance × Gravité

VRAISEMBLANCE (probabilité que la menace se réalise) :
1 FAIBLE : Mesures préventives solides, menace peu fréquente
2 MODÉRÉE : Mesures partielles, lacunes identifiées, menace courante
3 ÉLEVÉE : Peu de mesures, système très exposé, menace très fréquente

GRAVITÉ (sévérité des impacts sur les personnes) :
1 FAIBLE : Impact limité, facilement surmontable (email exposé, désagrément mineur)
2 MODÉRÉE : Impact significatif (usurpation partielle, atteinte réputation, difficultés financières)
3 ÉLEVÉE : Impact grave, difficile à surmonter (menace physique, préjudice majeur irréversible,
            discrimination grave, mise en danger de la vie)

SCORE = VRAISEMBLANCE × GRAVITÉ

         | Grav. 1 | Grav. 2 | Grav. 3
---------|---------|---------|--------
Vraism 1 |  1 Faib |  2 Faib |  3 Moy
Vraism 2 |  2 Faib |  4 Moy  |  6 Elev
Vraism 3 |  3 Moy  |  6 Elev |  9 Elev

Score 1-2 → FAIBLE  : Mesures standard suffisantes
Score 3-4 → MOYEN   : Mesures renforcées requises
Score 6-9 → ÉLEVÉ   : Mesures maximales + réévaluation
                       Si risque résiduel reste élevé → Consultation CNIL Art. 36

### Étape 4 — Valider lAIPD

Risque brut : avant mesures
Risque résiduel : après mesures

3 conclusions possibles :
✅ AIPD FAVORABLE : Tous risques résiduels faibles ou moyens acceptables → Lancer
⚠️ AIPD FAVORABLE AVEC RÉSERVES : Conditions à remplir avant lancement
❌ AIPD DÉFAVORABLE → Consultation CNIL obligatoire (Art. 36) si risque résiduel élevé
   → Délai CNIL : 8 semaines (prorogeable 14 semaines)
   → CNIL peut interdire, modifier ou autoriser sous conditions

Règles des données de santé : Gravité TOUJOURS ≥ 2 (souvent 3)

---

# CAS FICTIF : SmartCare — MedTech Solutions SAS

## Présentation

SmartCare : Application mobile pour patients diabétiques (Type 2)
suivis par des médecins généralistes partenaires.

Fonctionnalités :
- Suivi glycémique via Bluetooth (FreeStyle, Dexcom)
- Algorithme IA : Recommandations automatiques + Score de risque cardiovasculaire (0-100)
- Journal alimentaire (photo ou texte, analyse nutritionnelle IA)
- Portail médecin (consultation données patient, accès login + SMS OTP)
- Géolocalisation optionnelle lors des crises hypoglycémiques

## Données Collectées

| Catégorie | Données | Sensibles Art.9 ? |
|-----------|---------|---------------------|
| Identité | Nom, prénom, date naissance, email, téléphone | Non |
| Médicales | Glycémies, HbA1c, traitements, antécédents | OUI |
| Comportementales | Journal alimentaire, activité, sommeil | Oui (indirect) |
| Techniques | ID appareil, version OS, logs | Non |
| Géolocalisation | Position GPS lors alertes | Sensible en contexte |
| Score IA | Risque cardiovasculaire 0-100 | OUI (santé + décision auto) |

## Architecture Technique

Backend : Node.js sur AWS EC2 us-east-1 (Virginie, USA)
BDD : PostgreSQL chiffré RDS AWS (us-east-1)
Stockage : AWS S3 us-east-1 (NON chiffré — oubli équipe dev !)
IA : Modèle ML Google Cloud us-central1 (USA)
App mobile : React Native iOS + Android

Mesures de sécurité prévues (état initial) :
✓ HTTPS TLS 1.2
✓ Mots de passe hachés bcrypt
✓ 2FA SMS pour les médecins
✗ PAS de 2FA pour les patients (jugé trop contraignant)
✓ Chiffrement BDD RDS AES-256
✗ PAS de chiffrement S3 (oubli !)
✓ Logs API (conservés 30 jours)
✗ PAS de politique de purge des données médicales définie

Sous-traitants : AWS (USA), Google Cloud (USA), Twilio (USA)
DPO : Non désigné (en cours)
Personnes concernées : 50 000 patients (pilote : 2 000)
Age moyen : 58 ans — Personnes malades, souvent âgées = VULNÉRABLES
Médecins : 150 généralistes partenaires

Durées de conservation prévues :
- Données glycémiques : DURÉE INDÉFINIE pour améliorer lIA ← PROBLÈME
- Journal alimentaire : 2 ans
- Logs API : 30 jours

---
