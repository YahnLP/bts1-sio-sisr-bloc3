---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Violations de Données · Procédure de Notification · Cas Concrets"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 7*

---

## PARTIE III — Qu'est-ce qu'une Violation de Données ?

### III.A. Définition (Art. 4.12 RGPD)

> *"Une violation de la sécurité entraînant, de manière accidentelle ou illicite, la destruction, la perte, l'altération, la divulgation non autorisée de données à caractère personnel transmises, conservées ou traitées d'une autre manière, ou l'accès non autorisé à de telles données."*

**3 types de violations (triade CIA) :**

```
   TYPES DE VIOLATIONS
   ═══════════════════════════════════════════════════════════════

   ① VIOLATION DE CONFIDENTIALITÉ
   ──────────────────────────────────────────────────────────────
   Des données sont accédées ou divulguées sans autorisation

   Exemples :
   • Cyberattaque → Données clients exposées sur le dark web
   • Email envoyé à la mauvaise personne (client → concurrent)
   • Disque dur contenant données perso volé
   • Employé qui accède aux données de collègues sans autorisation
   • Publication accidentelle d'un fichier confidentiel sur un site web

   ② VIOLATION DE DISPONIBILITÉ
   ──────────────────────────────────────────────────────────────
   Des données sont perdues ou inaccessibles de manière permanente
   ou temporaire

   Exemples :
   • Ransomware chiffre toutes les données (inaccessibles)
   • Serveur incendié sans sauvegarde (perte définitive)
   • Suppression accidentelle de la base de données
   • Panne prolongée d'un service médical (dossiers inaccessibles)

   ③ VIOLATION D'INTÉGRITÉ
   ──────────────────────────────────────────────────────────────
   Des données sont modifiées de manière non autorisée

   Exemples :
   • Attaquant modifie des données bancaires dans la BDD
   • Employé malveillant altère des dossiers médicaux
   • Malware modifie des fichiers de configuration
   • Erreur humaine → Mauvaises données importées dans la BDD
```

---

### III.B. Pas Toutes les Violations Ne Sont Pas Égales

**Tous les incidents ne nécessitent pas de notification CNIL.** L'obligation dépend du **niveau de risque** pour les personnes.

```
   ARBRE DE DÉCISION — Dois-je notifier ?
   ═══════════════════════════════════════════════════════════════

   Y a-t-il eu une violation de données personnelles ?
   ──────────────────────────────────────────────────────────────
   NON → Pas de notification requise (documenter quand même)
   OUI → Continuer ↓

   Quel est le risque pour les personnes concernées ?
   ──────────────────────────────────────────────────────────────

   RISQUE FAIBLE
   ──────────────────────────────────────────────────────────────
   • Données non sensibles
   • Peu de personnes concernées
   • Impact limité / réversible
   • Données chiffrées (attaquant ne peut pas lire)

   → Documenter en interne (registre des violations)
   → Pas de notification CNIL obligatoire
   → Pas de notification aux personnes
   Exemple : Email envoyé au mauvais destinataire (1 personne,
             données non sensibles, rappelé immédiatement)

   RISQUE ÉLEVÉ
   ──────────────────────────────────────────────────────────────
   • Données sensibles (santé, bancaires, identifiants)
   • Nombreuses personnes concernées
   • Impact grave (discrimination, usurpation d'identité...)
   • Données en clair (lisibles par l'attaquant)

   → NOTIFIER LA CNIL sous 72h
   → Documenter en interne
   Exemple : Fuite base de données clients (email + CB)

   RISQUE TRÈS ÉLEVÉ
   ──────────────────────────────────────────────────────────────
   • Risque grave et immédiat pour les personnes
   • Usurpation d'identité probable
   • Préjudice financier imminent
   • Données de santé, biométriques...

   → NOTIFIER LA CNIL sous 72h
   → NOTIFIER LES PERSONNES CONCERNÉES (sans délai)
   → Documenter en interne
   Exemple : Ransomware + données bancaires volées en clair
```

---

### III.C. La Procédure de Notification CNIL (72h)

**Article 33 RGPD :** Obligation de notifier l'autorité de contrôle **dans les meilleurs délais et au plus tard 72 heures après** avoir pris connaissance de la violation.

```
   PROCÉDURE DE NOTIFICATION — ÉTAPE PAR ÉTAPE
   ═══════════════════════════════════════════════════════════════

   ① PRENDRE CONSCIENCE DE LA VIOLATION
   ──────────────────────────────────────────────────────────────
   L'horloge démarre à ce moment précis.
   → Documenter immédiatement : date et heure de découverte

   ② ÉVALUATION D'URGENCE (< 1 heure)
   ──────────────────────────────────────────────────────────────
   • Quelles données ? (type, sensibilité)
   • Combien de personnes ?
   • Violation confirmée ou suspectée ?
   • Données chiffrées ou en clair ?
   • Violation toujours en cours ?

   ③ CONFINEMENT (< 2 heures)
   ──────────────────────────────────────────────────────────────
   • Stopper la violation si possible (isoler serveur, changer MDP)
   • Préserver les preuves (logs, captures)
   • NE PAS effacer les traces (besoin pour l'enquête + notification)

   ④ INFORMER EN INTERNE (< 4 heures)
   ──────────────────────────────────────────────────────────────
   • Informer le DPO (si existant)
   • Informer la direction
   • Alerter l'équipe IT

   ⑤ ÉVALUER LE RISQUE (< 12 heures)
   ──────────────────────────────────────────────────────────────
   • Analyser l'impact : confidentialité / disponibilité / intégrité
   • Estimer le nombre de personnes affectées
   • Déterminer la gravité du risque

   ⑥ NOTIFIER LA CNIL (< 72 heures)
   ──────────────────────────────────────────────────────────────
   Via le portail : https://notifications.cnil.fr

   CONTENU OBLIGATOIRE DE LA NOTIFICATION
   ──────────────────────────────────────────────────────────────
   A) Nature de la violation
      (confidentialité / disponibilité / intégrité)

   B) Catégories et nombre approximatif de personnes concernées
      ("Environ 45 000 clients")

   C) Catégories et nombre approximatif d'enregistrements
      ("Noms, adresses emails, historiques d'achats")

   D) Coordonnées du DPO ou point de contact

   E) Conséquences probables de la violation
      ("Risque d'hameçonnage ciblé des clients")

   F) Mesures prises ou envisagées
      ("Réinitialisation des mots de passe, surveillance renforcée")

   ⑦ NOTIFIER LES PERSONNES (si risque élevé)
   ──────────────────────────────────────────────────────────────
   "Dans les meilleurs délais" (pas de délai précis, mais urgent)

   CONTENU DE LA NOTIFICATION AUX PERSONNES
   ──────────────────────────────────────────────────────────────
   • Nature de la violation (sans détail technique dangereux)
   • Données concernées
   • Conséquences probables
   • Mesures prises
   • Contact DPO / service RGPD
   • Conseils pratiques (changer MDP, surveiller comptes bancaires...)

   ⑧ DOCUMENTER EN INTERNE (TOUJOURS)
   ──────────────────────────────────────────────────────────────
   Même si pas de notification CNIL → Registre des violations

   Contenu du registre :
   • Date et heure de la violation
   • Nature et faits
   • Évaluation du risque
   • Mesures prises
   • Décision de notification (motivée)
```

---

### III.D. Notification Tardive

```
   QUE SE PASSE-T-IL SI ON DÉPASSE LES 72h ?
   ═══════════════════════════════════════════════════════════════

   NOTIFICATION TARDIVE ACCEPTÉE si :
   → On peut justifier le retard par la complexité de l'analyse
   → La notification est accompagnée d'une explication des raisons

   FORMULE POUR NOTIFICATION TARDIVE :
   "En vertu de l'article 33.1 du RGPD, cette notification
   intervient après le délai de 72 heures en raison de [motif].
   Les informations complètes sont maintenant disponibles..."

   SANCTIONS CNIL EN CAS DE NON-NOTIFICATION
   ──────────────────────────────────────────────────────────────
   • Avertissement
   • Mise en demeure
   • Amende administrative jusqu'à 10 M€ ou 2% du CA mondial

   EXEMPLES DE SANCTIONS POUR NOTIFICATION TARDIVE :
   • H&M (2020) : 35 M€ (surveillance abusive + violation non notifiée)
   • British Airways (2021) : 22 M£ (fuite 500 000 clients, notification tardive)
```

---

## PARTIE IV — Cas Concrets de Violations en France

### IV.A. Free — Fuite de Données (Octobre 2024)

```
   FREE — VIOLATION DE DONNÉES MASSIVE
   ═══════════════════════════════════════════════════════════════

   DATE : Octobre 2024
   ORGANISATION : Free (opérateur télécom, 22 millions d'abonnés)

   VIOLATION
   ──────────────────────────────────────────────────────────────
   Type : CONFIDENTIALITÉ (accès non autorisé)

   Données exposées :
   • Noms, prénoms, adresses postales
   • Emails, numéros de téléphone
   • Données contractuelles (offres, dates)
   • Pour certains abonnés : IBAN (coordonnées bancaires)

   Nombre de personnes : 19,2 millions d'abonnés concernés

   CHRONOLOGIE
   ──────────────────────────────────────────────────────────────
   Octobre 2024 : Intrusion détectée
   → Free notifie la CNIL (sous 72h)
   → Free notifie les abonnés par email

   MESSAGE AUX ABONNÉS
   ──────────────────────────────────────────────────────────────
   "Nous avons récemment été victimes d'une cyberattaque ayant
   conduit à un accès non autorisé à certaines de vos données
   personnelles. [...] Nous vous recommandons de rester vigilants
   face à d'éventuelles tentatives de phishing."

   CONSEILS DONNÉS AUX CLIENTS
   ──────────────────────────────────────────────────────────────
   • Méfiance accrue face aux emails/SMS/appels suspects
   • Ne jamais communiquer ses mots de passe
   • Surveiller ses relevés bancaires

   LEÇONS
   ──────────────────────────────────────────────────────────────
   ✅ Free a notifié la CNIL et les personnes (bonne pratique)
   ❌ La violation aurait-elle pu être évitée ?
      → Contrôle d'accès insuffisant sur les systèmes de gestion
      → Surveillance des accès anormaux insuffisante
```

---

### IV.B. Pôle Emploi — Fuite de Données (Août 2023)

```
   PÔLE EMPLOI — VIOLATION VIA SOUS-TRAITANT
   ═══════════════════════════════════════════════════════════════

   DATE : Août 2023
   ORGANISATION : Pôle Emploi (France Travail depuis 2024)

   ORIGINE
   ──────────────────────────────────────────────────────────────
   La violation ne vient PAS directement de Pôle Emploi
   mais d'un prestataire informatique : Majorel

   → Illustration du risque SOUS-TRAITANT (vu en S5)

   VIOLATION
   ──────────────────────────────────────────────────────────────
   Type : CONFIDENTIALITÉ

   Données exposées :
   • Noms, prénoms
   • Numéros de sécurité sociale
   • Identifiants France Travail
   • Emails, téléphones

   Nombre de personnes : 10 millions de demandeurs d'emploi

   CONSÉQUENCES
   ──────────────────────────────────────────────────────────────
   • Risque élevé d'usurpation d'identité
   • Risque de phishing ciblé (données très précises)
   • Numéros de sécurité sociale = données très sensibles

   LEÇONS RGPD
   ──────────────────────────────────────────────────────────────
   ① Vérifier la sécurité des sous-traitants (Art. 28)
   ② Auditer régulièrement leurs pratiques
   ③ Contrat obligatoire précisant les mesures de sécurité
   ④ La responsabilité du RT (Pôle Emploi) n'est pas effacée
      par la faute du sous-traitant
```

---

### IV.C. Hôpital de Versailles — Ransomware (Décembre 2022)

```
   HÔPITAL DE VERSAILLES — RANSOMWARE + VIOLATION
   ═══════════════════════════════════════════════════════════════

   DATE : 3 décembre 2022
   ORGANISATION : Centre Hospitalier de Versailles (André-Mignot)

   VIOLATION
   ──────────────────────────────────────────────────────────────
   Type : DISPONIBILITÉ + CONFIDENTIALITÉ

   ① DISPONIBILITÉ : Ransomware chiffre les systèmes
      → Dossiers patients inaccessibles
      → Systèmes de soins paralysés

   ② CONFIDENTIALITÉ : Données de patients volées
      → Mises en ligne par le groupe Lockbit sur le dark web
      → Données médicales (ultra sensibles) exposées

   Nombre de personnes : Des milliers de patients

   RÉACTION
   ──────────────────────────────────────────────────────────────
   → Notification CNIL effectuée (obligation)
   → ANSSI (Agence Nationale Sécurité Systèmes d'Info) déployée
   → 6 patients transférés (soins critiques impossibles)
   → Retour partiel à normale : plusieurs semaines

   LEÇONS RGPD + SÉCURITÉ
   ──────────────────────────────────────────────────────────────
   ① Double violation = notification CNIL obligatoire
   ② Secteur santé = données ultra sensibles = risque très élevé
   ③ Les personnes concernées DOIVENT être notifiées
      (données de santé + risque grave)
   ④ PRA insuffisant pour secteur critique
   ⑤ Sauvegardes non connectées au réseau = INDISPENSABLE
```

---

## V. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Conservation active** | Données utilisées régulièrement dans les systèmes opérationnels |
| **Archivage intermédiaire** | Conservation pour obligations légales, accès rare et restreint |
| **Purge** | Suppression définitive ou anonymisation des données dont la durée est dépassée |
| **Privacy by Design** | Protection des données intégrée dès la conception d'un système |
| **Privacy by Default** | Paramètres les plus protecteurs activés par défaut |
| **AIPD / PIA** | Analyse d'Impact relative à la Protection des Données — obligatoire pour traitements à risque élevé |
| **Violation de données** | Incident de sécurité entraînant destruction, perte, altération ou accès non autorisé à des données perso |
| **Violation de confidentialité** | Accès ou divulgation non autorisé(e) |
| **Violation de disponibilité** | Perte ou inaccessibilité des données |
| **Violation d'intégrité** | Modification non autorisée des données |
| **Notification CNIL** | Obligation de signaler une violation sous 72h |
| **Registre des violations** | Document interne obligatoire listant tous les incidents, même non notifiés |
| **ANSSI** | Agence Nationale de la Sécurité des Systèmes d'Information |

---
