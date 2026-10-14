---
author: YLP
title: 🖥️ FICHE DE TP
---

# 🖥️ TP — CAPTURE ET DÉPLOIEMENT D'IMAGE SYSTÈME
# MINI-PIA SMARTCARE — 

Durée : 60 minutes — Individuel ou binôme

## ÉTAPE 1 — DESCRIPTION DU TRAITEMENT (10 min)

A. CONTEXTE
Responsable de traitement : MedTech Solutions SAS
DPO désigné ? ☐ Oui ☐ Non — Commentaire : ___
Sous-traitants (3) :
1. ________ (pays : ___) 2. ________ (pays : ___) 3. ________ (pays : ___)

B. FINALITÉS ET BASES LÉGALES
Finalité 1 : _______ Base légale : _______
Finalité 2 : _______ Base légale : _______
Finalité 3 (algorithme IA) : _______ Base légale : _______

C. DONNÉES ET PERSONNES CONCERNÉES
Catégories de données sensibles Art. 9 présentes : ___
Nombre de personnes concernées : ___
Personnes vulnérables ? ☐ Oui → Lesquelles : ___

D. SUPPORTS ET FLUX
Localisation des données : ☐ France/UE ☐ USA (AWS) ☐ USA (Google Cloud)
Transfert hors UE ? ☐ Oui ☐ Non
Si oui, garanties prévues : ___

## ÉTAPE 2 — NÉCESSITÉ ET PROPORTIONNALITÉ (10 min)

Évaluer : ✅ Conforme / ⚠️ Partiel / ❌ Non conforme

La collecte durée indéfinie pour améliorer lIA est-elle proportionnée ? ___
Quelle durée proposeriez-vous ? ___
DPO désigné ? ___
Droit dopposition au scoring IA prévu ? ___
Contrats sous-traitance Art. 28 mentionnés ? ___
Transferts AWS/Google USA encadrés ? ___

## ÉTAPE 3 — ÉVALUATION DES RISQUES (25 min)

### RISQUE R1 — Accès illégitime aux données médicales

Menaces : Intrusion externe sur AWS / Accès AWS par Amazon / Vol smartphone patient /
          Interception réseau Wi-Fi public / Compte médecin compromis

Mesures existantes : HTTPS TLS 1.2 / BDD chiffrée / 2FA médecins
Mesures ABSENTES : ✗ 2FA patients / ✗ Chiffrement S3

Évaluation risque brut :
Vraisemblance : ___ Justification : ___
Gravité :       ___ Justification : ___
SCORE BRUT :    ___ × ___ = ___

Mesures supplémentaires à proposer :
1. ___ 2. ___ 3. ___

Évaluation risque résiduel :
Vraisemblance : ___ Gravité : ___ SCORE RÉSIDUEL : ___
Niveau : ☐ Faible ☐ Moyen ☐ Élevé

### RISQUE R2 — Décision automatisée sans contrôle humain

Lalgorithme génère des recommandations médicales et un score cardiovasculaire
sans validation humaine systématique.

Problèmes RGPD : Art. 22 décision automatisée / Droit dopposition /
               Transparence algorithme / Biais potentiels

Évaluation brut : Vraisemblance : ___ Gravité : ___ SCORE : ___
Mesures : 1. ___ 2. ___ 3. ___
Résiduel : Vraisemblance : ___ Gravité : ___ SCORE : ___ Niveau : ___

### RISQUE R3 — Transfert données médicales hors UE

Toutes les données médicales hébergées AWS + Google Cloud USA.
CLOUD Act 2018 : autorités américaines peuvent exiger laccès.

Garanties actuelles : AUCUNE MENTIONNÉE dans le dossier ← PROBLÈME

Évaluation brut : Vraisemblance : ___ Gravité : ___ SCORE : ___
Mesures : 1. CCT (Clauses Contractuelles Types UE) 2. ___
Résiduel : Vraisemblance : ___ Gravité : ___ SCORE : ___ Niveau : ___

### RISQUE R4 — Perte / indisponibilité des données

Sauvegardes AWS quotidiennes existent mais non testées.
Pas de RPO/RTO défini pour alertes hypoglycémiques.

Évaluation brut : Vraisemblance : ___ Gravité : ___ SCORE : ___
Mesures : 1. Tests restauration réguliers 2. ___
Résiduel : Vraisemblance : ___ Gravité : ___ SCORE : ___ Niveau : ___

## ÉTAPE 4 — CONCLUSION ET DÉCISION (15 min)

TABLEAU DE SYNTHÈSE :
R1 Accès illégitime  | Score brut : /9 | Score résiduel : /9 | Niveau : ___
R2 Décision auto IA  | Score brut : /9 | Score résiduel : /9 | Niveau : ___
R3 Transfert hors UE | Score brut : /9 | Score résiduel : /9 | Niveau : ___
R4 Perte données     | Score brut : /9 | Score résiduel : /9 | Niveau : ___

CRITÈRES DÉCLENCHEURS SmartCare (cochez) :
☐ Scoring (score cardiovasculaire)       ☐ Décision automatisée
☐ Données sensibles santé                ☐ Grande échelle (50 000 patients)
☐ Croisement données                     ☐ Personnes vulnérables (patients âgés)
☐ Usage innovant IA médicale             ☐ Transfert hors UE

Nombre de critères : ___ → AIPD obligatoire ? ☐ Oui ☐ Non

MANQUEMENTS DE CONFORMITÉ identifiés : 1.___ 2.___ 3.___ 4.___

DÉCISION FINALE :
☐ AIPD FAVORABLE → Le projet peut être lancé tel quel
☐ AIPD FAVORABLE AVEC RÉSERVES → Conditions :
  1.___ 2.___ 3.___ Délai : ___
☐ AIPD DÉFAVORABLE → Consultation CNIL (Art. 36) requise
  Risques concernés : ___

Votre conclusion argumentée (5-8 lignes) :
___

---
