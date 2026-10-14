---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "RGPD · Contexte · Définitions Fondamentales"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 5*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B2.1** | Comprendre les obligations légales liées au traitement de données personnelles |
| **B2.2** | Identifier les acteurs de la protection des données |

---

## PARTIE I — Contexte et Historique du RGPD

### I.A. Avant le RGPD : La Directive de 1995

Avant le RGPD, la protection des données personnelles en Europe était régie par une **directive de 1995** (Directive 95/46/CE).

```
   PROBLÈMES DE LA DIRECTIVE 1995
   ═══════════════════════════════════════════════════════════════
   
   ① FRAGMENTÉE
   ──────────────────────────────────────────────────────────────
   Chaque pays l'appliquait différemment
   → 28 lois nationales différentes
   → Entreprises : "On s'installe en Irlande, réglementation plus souple"
   
   ② OBSOLÈTE
   ──────────────────────────────────────────────────────────────
   Rédigée en 1995 → Avant Google, Amazon, Facebook, smartphone
   → Ne prenait pas en compte le Big Data, les réseaux sociaux,
     le profilage, le cloud
   
   ③ SANCTIONS INSUFFISANTES
   ──────────────────────────────────────────────────────────────
   Maximum : quelques milliers d'euros selon les pays
   → Facebook, Google : Pas dissuasif du tout
```

---

### I.B. Le RGPD : Naissance et Adoption

**RGPD** = **R**èglement **G**énéral sur la **P**rotection des **D**onnées

En anglais : **GDPR** (General Data Protection Regulation)

```
   CHRONOLOGIE
   ═══════════════════════════════════════════════════════════════
   
   2012 : La Commission européenne propose le RGPD
   ──────────────────────────────────────────────────────────────
   Après les révélations Snowden (2013) sur la surveillance
   massive de la NSA → Réactions européennes
   
   27 AVRIL 2016 : RGPD adopté par le Parlement européen
   ──────────────────────────────────────────────────────────────
   Règlement n°2016/679 — publié au Journal Officiel de l'UE
   
   MAI 2016 : Entrée en vigueur (publication)
   ──────────────────────────────────────────────────────────────
   Période de transition : 2 ans pour se mettre en conformité
   
   25 MAI 2018 : APPLICATION OBLIGATOIRE
   ──────────────────────────────────────────────────────────────
   Toutes les organisations concernées DOIVENT être conformes
   → Début des contrôles et sanctions
```

---

### I.C. Portée du RGPD

**Qui est concerné ?**

```
   CHAMP D'APPLICATION TERRITORIAL
   ═══════════════════════════════════════════════════════════════
   
   ① Toute organisation ÉTABLIE dans l'UE
   ──────────────────────────────────────────────────────────────
   Exemple : Une PME française, une multinationale allemande,
             une startup belge
   
   ② Toute organisation HORS UE qui traite des données
      de personnes SE TROUVANT dans l'UE
   ──────────────────────────────────────────────────────────────
   Exemple : Amazon USA qui vend en France
             Google Californie qui collecte données d'internautes français
             Netflix qui propose des services en Europe
   
   → Le RGPD a une portée MONDIALE pour toute activité
     ciblant les résidents européens
```

**Résumé :**
- ✅ PME française → RGPD
- ✅ Multinationale américaine avec clients en France → RGPD
- ✅ Association loi 1901 qui gère des adhérents → RGPD
- ✅ Auto-entrepreneur avec liste clients → RGPD
- ❌ Fichier purement personnel (carnet d'adresses privé) → Pas RGPD

---

## PARTIE II — Qu'est-ce qu'une Donnée Personnelle ?

### II.A. Définition Officielle

**Article 4 du RGPD :**

> *"Toute information se rapportant à une personne physique identifiée ou identifiable."*

**Décomposons :**

```
   ANALYSE DE LA DÉFINITION
   ═══════════════════════════════════════════════════════════════
   
   "TOUTE INFORMATION"
   ──────────────────────────────────────────────────────────────
   Peu importe le format :
   • Texte (nom, adresse, email)
   • Image (photo, vidéo)
   • Son (enregistrement vocal)
   • Données techniques (IP, cookie, géolocalisation)
   • Données biologiques (ADN, empreinte)
   
   "PERSONNE PHYSIQUE"
   ──────────────────────────────────────────────────────────────
   Uniquement les HUMAINS (pas les entreprises)
   • Une personne vivante (les morts : règles spéciales)
   • Un individu (pas une organisation)
   
   "IDENTIFIÉE OU IDENTIFIABLE"
   ──────────────────────────────────────────────────────────────
   ① IDENTIFIÉE : On sait directement qui c'est
      Exemple : Nom + Prénom
   
   ② IDENTIFIABLE : On peut retrouver qui c'est en croisant des infos
      Exemple : Plaque d'immatriculation → fichier SIV → nom du propriétaire
```

---

### II.B. Exemples : Donnée Personnelle ou Non ?

```
   EXEMPLES
   ═══════════════════════════════════════════════════════════════

   ✅ DONNÉES PERSONNELLES
   ──────────────────────────────────────────────────────────────
   • Nom et prénom                     → Direct (identifié)
   • Adresse email                     → Direct (identifié)
   • Numéro de téléphone               → Direct (identifié)
   • Adresse postale                   → Direct (identifié)
   • Date de naissance                 → Combiné = identifiable
   • Photo de visage                   → Identifié (reconnaissance)
   • Adresse IP                        → Identifiable (fournisseur)
   • Numéro de sécurité sociale        → Direct (unique)
   • Plaque d'immatriculation          → Identifiable (SIV)
   • Données de géolocalisation        → Identifiable (domicile/travail)
   • Cookie de navigation              → Identifiable (profil)
   • Prénom uniquement (Monsieur Jean) → Identifiable (contexte)
   • Voix enregistrée                  → Identifiable (reconnaissance)

   ❌ PAS DES DONNÉES PERSONNELLES
   ──────────────────────────────────────────────────────────────
   • "Homme, 35-40 ans, Paris" (non identifiable sans autre info)
   • Données anonymisées irréversiblement
     (impossible de retrouver la personne)
   • Données d'une entreprise (SIRET, raison sociale)
   • Statistiques globales ("70% des Français...")
```

---

### II.C. L'Anonymisation vs la Pseudonymisation

**Deux techniques, deux niveaux de protection :**

```
   ANONYMISATION
   ═══════════════════════════════════════════════════════════════
   
   Définition : Modification irréversible des données
               → Impossible de retrouver la personne
   
   Exemple :
   AVANT : Jean Dupont, né le 12/03/1985, Paris 75012
   APRÈS : Personne de sexe masculin, 39 ans, habitant Paris
   
   Conditions strictes :
   ① Individualisation impossible (isoler une personne)
   ② Liaison impossible (relier deux enregistrements)
   ③ Inférence impossible (déduire des infos sur une personne)
   
   Résultat : PLUS soumis au RGPD (données non personnelles)
   
   ⚠️ L'anonymisation vraie est TRÈS difficile à atteindre
      Des études ont montré que 87% des Américains sont
      identifiables uniquement avec code postal + date naissance + sexe
   
   
   PSEUDONYMISATION
   ═══════════════════════════════════════════════════════════════
   
   Définition : Remplacement des identifiants par un pseudonyme
               → Possible de retrouver la personne avec la clé
   
   Exemple :
   AVANT : Jean Dupont, jean.dupont@email.fr
   APRÈS : ID_48291, user_a7x@temp.local
   
   La clé de correspondance est stockée séparément et sécurisée.
   
   Résultat : TOUJOURS soumis au RGPD (mais risque réduit)
              Bonne pratique recommandée par le RGPD
```

---

### II.D. Les Données Sensibles (Catégories Particulières)

**Certaines données méritent une protection RENFORCÉE** car leur divulgation peut causer des préjudices graves.

```
   ARTICLE 9 DU RGPD — CATÉGORIES PARTICULIÈRES
   ═══════════════════════════════════════════════════════════════
   
   LES 9 CATÉGORIES INTERDITES (en principe)
   ──────────────────────────────────────────────────────────────
   
   ① Origines raciales ou ethniques
   ② Opinions politiques
   ③ Convictions religieuses ou philosophiques
   ④ Appartenance syndicale
   ⑤ Données génétiques (ADN)
   ⑥ Données biométriques (empreintes, reconnaissance faciale)
   ⑦ Données de santé
   ⑧ Vie sexuelle ou orientation sexuelle
   ⑨ Données relatives aux condamnations pénales
   
   RÈGLE : INTERDITES par défaut
   SAUF si l'une des exceptions légales s'applique
   (consentement explicite, nécessité médicale, recherche...)
   
   EXEMPLES CONCRETS
   ──────────────────────────────────────────────────────────────
   • Médecin collectant le groupe sanguin d'un patient → Donnée santé ✅ Exception médicale
   • Employeur demandant les opinions politiques d'un candidat → ❌ INTERDIT
   • Syndicat gérant ses membres → Appartenance syndicale ✅ Exception (organisation)
   • Application de rencontres → Orientation sexuelle ✅ Exception (consentement explicite)
   • Logiciel RH avec mesure biométrique (badge empreinte) → ❌ Besoin accord CNIL
```

---

## PARTIE III — Les 6 Principes Fondamentaux du RGPD

**Article 5 du RGPD — Les données personnelles doivent être :**

### Principe 1 — Licéité, Loyauté, Transparence

```
   LICÉITÉ : La collecte doit avoir une BASE LÉGALE
   ──────────────────────────────────────────────────────────────
   6 bases légales possibles :
   1. Consentement de la personne
   2. Exécution d'un contrat
   3. Obligation légale
   4. Sauvegarde des intérêts vitaux
   5. Mission d'intérêt public
   6. Intérêts légitimes du responsable
   
   LOYAUTÉ : Pas de tromperie sur l'usage des données
   ──────────────────────────────────────────────────────────────
   ❌ Collecter des données pour "améliorer le service"
      mais les revendre en réalité
   
   TRANSPARENCE : La personne doit être informée
   ──────────────────────────────────────────────────────────────
   ✅ Politique de confidentialité claire et accessible
   ✅ Information au moment de la collecte
```

---

### Principe 2 — Limitation des Finalités

```
   Données collectées pour une finalité précise
   NE PEUVENT PAS être utilisées pour autre chose
   
   ❌ EXEMPLE DE VIOLATION
   ──────────────────────────────────────────────────────────────
   Clinique collecte adresses email pour envoyer des rappels de RDV
   → Revend ces emails à une société pharmaceutique pour publicité
   → VIOLATION (finalité différente de celle annoncée)
   
   ✅ EXEMPLE CONFORME
   ──────────────────────────────────────────────────────────────
   E-commerce collecte adresse pour livraison
   → Utilise l'adresse uniquement pour livrer la commande
   → OK (finalité respectée)
```

---

### Principe 3 — Minimisation des Données

```
   Collecter uniquement ce qui est STRICTEMENT NÉCESSAIRE
   
   ❌ EXEMPLE DE VIOLATION
   ──────────────────────────────────────────────────────────────
   Formulaire d'inscription newsletter :
   • Nom ✅ (nécessaire)
   • Prénom ✅ (nécessaire)
   • Email ✅ (nécessaire)
   • Date de naissance ❌ (pas nécessaire pour newsletter)
   • Numéro de téléphone ❌ (pas nécessaire pour newsletter)
   • Adresse postale ❌ (pas nécessaire pour newsletter)
   
   ✅ EXEMPLE CONFORME
   ──────────────────────────────────────────────────────────────
   Formulaire d'inscription newsletter :
   • Prénom ✅ (pour personnaliser "Bonjour Jean")
   • Email ✅ (pour envoyer la newsletter)
   
   → SEULEMENT 2 champs suffisent
```

---

### Principe 4 — Exactitude

```
   Les données doivent être EXACTES et à JOUR
   
   Obligations :
   ✅ Mettre à jour les données qui changent
   ✅ Effacer les données incorrectes
   ✅ Permettre aux personnes de corriger leurs données
   
   Exemple : Base clients d'un e-commerce
   → Si un client change d'adresse, l'ancienne doit être mise à jour
   → Garder une ancienne adresse inexacte = violation
```

---

### Principe 5 — Limitation de Conservation

```
   Les données ne peuvent pas être conservées INDÉFINIMENT
   → Durée de conservation proportionnelle à la finalité
   
   EXEMPLES DE DURÉES LÉGALES
   ──────────────────────────────────────────────────────────────
   Données clients (e-commerce) : 3 ans après dernier achat
   Données RH (fiches salaire) : 5 ans après fin contrat
   Données comptables : 10 ans (obligation légale)
   Vidéosurveillance : 30 jours maximum
   Logs système : 1 an (recommandation CNIL)
   Cookies : 13 mois maximum
   
   OBLIGATION
   ──────────────────────────────────────────────────────────────
   Définir une durée de conservation AVANT de collecter
   → Et respecter cette durée (purger les données expirées)
```

---

### Principe 6 — Intégrité et Confidentialité (Sécurité)

```
   Les données doivent être PROTÉGÉES contre :
   • Accès non autorisé
   • Divulgation accidentelle
   • Perte / Destruction
   • Altération
   
   MESURES TECHNIQUES ET ORGANISATIONNELLES
   ──────────────────────────────────────────────────────────────
   ✅ Chiffrement des données (AES-256)
   ✅ Contrôle des accès (droits minimaux)
   ✅ Sauvegardes régulières
   ✅ Politique de mots de passe robustes
   ✅ Formation des employés
   ✅ Tests de pénétration réguliers
   
   → CE PRINCIPE CONCERNE DIRECTEMENT LES TECHNICIENS IT !
```

---
