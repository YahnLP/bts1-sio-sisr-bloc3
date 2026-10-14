---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Collecte Légale · Bases Légales · Consentement · Transparence"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 6*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B2.1** | Comprendre les obligations légales liées au traitement de données personnelles |
| **B2.3** | Appliquer les principes du RGPD dans un contexte professionnel |

---

## PARTIE I — Les 6 Bases Légales du Traitement (Approfondissement)

### I.A. Rappel : Pourquoi une Base Légale ?

**Principe :** Tout traitement de données personnelles doit reposer sur **au moins une** des 6 bases légales définies par l'Article 6 du RGPD. Sans base légale, le traitement est **illicite**.

```
   ARTICLE 6 DU RGPD — LES 6 BASES LÉGALES
   ═══════════════════════════════════════════════════════════════

   1. CONSENTEMENT
   2. EXÉCUTION D'UN CONTRAT
   3. OBLIGATION LÉGALE
   4. SAUVEGARDE DES INTÉRÊTS VITAUX
   5. MISSION D'INTÉRÊT PUBLIC
   6. INTÉRÊTS LÉGITIMES DU RESPONSABLE
```

---

### I.B. Base 1 — Le Consentement (Art. 6.1.a)

**Définition :**
> *"La personne concernée a consenti au traitement de ses données à caractère personnel pour une ou plusieurs finalités spécifiques."*

**4 conditions CUMULATIVES du consentement valide :**

```
   ① LIBRE
   ──────────────────────────────────────────────────────────────
   La personne doit avoir un VRAI choix, sans pression ni
   déséquilibre de pouvoir.

   ❌ Refus impossible (ex : pas de service sans cookies)
   ❌ Case pré-cochée (consentement par défaut)
   ❌ Consentement demandé par l'employeur à ses salariés
      (relation de subordination = pas libre)

   ② SPÉCIFIQUE
   ──────────────────────────────────────────────────────────────
   Un consentement distinct pour CHAQUE finalité.

   ❌ "J'accepte que mes données soient utilisées à des fins
      commerciales et partagées avec nos partenaires"
      → 2 finalités groupées = invalide

   ✅ Case 1 : "J'accepte la newsletter mensuelle"
   ✅ Case 2 : "J'accepte le partage avec nos partenaires"
      → 2 cases séparées = valide

   ③ ÉCLAIRÉ
   ──────────────────────────────────────────────────────────────
   La personne doit COMPRENDRE ce qu'elle accepte.

   Informations obligatoires AVANT le consentement :
   → Identité du responsable de traitement
   → Finalité(s) du traitement
   → Types de données collectées
   → Droit de retirer le consentement à tout moment

   ❌ "En cliquant ici, vous acceptez nos conditions"
      (sans lien vers les conditions)

   ④ UNIVOQUE
   ──────────────────────────────────────────────────────────────
   Acte positif et clair (pas d'ambiguïté).

   ❌ "En continuant à naviguer, vous acceptez..."
      → Pas un acte positif (naviguer ≠ consentir)

   ❌ Case pré-cochée
      → Pas un acte positif (ne rien faire ≠ consentir)

   ✅ Cocher une case vide
   ✅ Cliquer "J'accepte" après avoir lu l'information
   ✅ Signer un document
```

---

### I.C. Retrait du Consentement

**Règle :** Le consentement peut être **retiré à tout moment**, aussi facilement qu'il a été donné.

```
   SYMÉTRIE OBLIGATOIRE
   ═══════════════════════════════════════════════════════════════

   DONNER le consentement :     Se désabonner newsletter :
   Cliquer "J'accepte"     →   Cliquer "Se désabonner"
   (1 clic)                    (doit être en 1 clic maximum)

   ❌ S'abonner en 1 clic → Se désabonner par courrier postal
   ❌ S'abonner en ligne → Appeler un numéro surtaxé pour se
      désabonner
   ❌ Désabonnement caché dans les paramètres (7 niveaux de menu)
```

**Conséquences du retrait :**
- L'utilisation des données doit **cesser immédiatement**
- Les données ne peuvent pas être conservées uniquement parce que le consentement existait avant
- Sauf si une autre base légale s'applique (ex : obligation légale)

---

### I.D. Base 2 — Exécution d'un Contrat (Art. 6.1.b)

```
   DÉFINITION
   ═══════════════════════════════════════════════════════════════
   Traitement nécessaire pour exécuter un contrat avec la personne
   OU pour des mesures pré-contractuelles.

   EXEMPLES VALIDES
   ──────────────────────────────────────────────────────────────
   • E-commerce : Adresse de livraison (pour livrer la commande)
   • Employeur : RIB du salarié (pour payer le salaire)
   • Médecin : Données santé (pour soigner le patient)
   • Banque : Données financières (pour gérer le compte)

   ⚠️ ATTENTION : Seulement les données NÉCESSAIRES au contrat
   ──────────────────────────────────────────────────────────────
   ❌ E-commerce : Date de naissance (pas nécessaire pour livrer)
   ❌ Employeur : Opinion politique (pas nécessaire au travail)
```

---

### I.E. Base 3 — Obligation Légale (Art. 6.1.c)

```
   DÉFINITION
   ═══════════════════════════════════════════════════════════════
   Traitement imposé par une loi ou réglementation.

   EXEMPLES
   ──────────────────────────────────────────────────────────────
   • Fiche de paie → Obligation Code du travail
   • Déclaration fiscale → Obligation Code général des impôts
   • Facture avec données client → Obligation comptable (TVA)
   • Registre des accidents du travail → Obligation réglementaire
   • Conservation des logs pendant 1 an → LCEN (Loi pour la
     Confiance dans l'Économie Numérique)

   ⚠️ PAS BESOIN DE DEMANDER LE CONSENTEMENT
   ──────────────────────────────────────────────────────────────
   La loi l'impose → Pas de choix pour la personne
   Mais obligation d'INFORMER la personne
```

---

### I.F. Base 6 — Intérêts Légitimes (Art. 6.1.f)

**La base légale la plus souple (et la plus discutable)**

```
   DÉFINITION
   ═══════════════════════════════════════════════════════════════
   Le traitement est nécessaire pour les intérêts légitimes du
   responsable, SAUF si les droits fondamentaux de la personne
   prévalent.

   → Nécessite une BALANCE D'INTÉRÊTS (test de proportionnalité)

   EXEMPLES VALIDES
   ──────────────────────────────────────────────────────────────
   ✅ Vidéosurveillance des locaux pour la sécurité des biens
   ✅ Prospection commerciale auprès de clients existants
      (pas pour de nouveaux prospects)
   ✅ Détection des fraudes (comportements suspects)
   ✅ IT : Logs de sécurité pour détecter les intrusions

   EXEMPLES INVALIDES
   ──────────────────────────────────────────────────────────────
   ❌ Suivi comportemental des salariés (intérêt salarié prévaut)
   ❌ Vente de données à des tiers (pas "légitime")
   ❌ Profilage intensif pour publicité ciblée sans lien avec
      une relation commerciale existante
```

---

## PARTIE II — La Transparence

### II.A. L'Obligation d'Information

Quand le RT collecte des données, il doit **informer la personne** au moment de la collecte (Articles 13-14 RGPD).

**Informations obligatoires à fournir :**

```
   MENTIONS D'INFORMATION OBLIGATOIRES
   ═══════════════════════════════════════════════════════════════

   ① QUI traite ? (Identité du responsable de traitement)
   ──────────────────────────────────────────────────────────────
   Nom, adresse, coordonnées de contact

   ② POURQUOI ? (Finalité(s) du traitement)
   ──────────────────────────────────────────────────────────────
   Objectif précis et explicite

   ③ SUR QUELLE BASE LÉGALE ?
   ──────────────────────────────────────────────────────────────
   Consentement / Contrat / Obligation légale / Intérêt légitime

   ④ QUELLES DONNÉES ? (Catégories de données collectées)
   ──────────────────────────────────────────────────────────────
   Liste des données collectées

   ⑤ COMBIEN DE TEMPS ? (Durée de conservation)
   ──────────────────────────────────────────────────────────────
   Durée précise ou critères pour la déterminer

   ⑥ QUI Y A ACCÈS ? (Destinataires)
   ──────────────────────────────────────────────────────────────
   Personnes internes habilitées + sous-traitants + partenaires

   ⑦ QUELS DROITS ? (Droits des personnes)
   ──────────────────────────────────────────────────────────────
   Accès, rectification, effacement, portabilité, opposition...

   ⑧ COMMENT EXERCER SES DROITS ?
   ──────────────────────────────────────────────────────────────
   Adresse email / formulaire / courrier postal

   ⑨ TRANSFERTS HORS UE ?
   ──────────────────────────────────────────────────────────────
   Si données envoyées hors de l'UE → Mentionner et les garanties
```

---

### II.B. Modèle de Politique de Confidentialité

**Comment présenter ces informations sur un site web :**

```
   POLITIQUE DE CONFIDENTIALITÉ — MODÈLE
   ═══════════════════════════════════════════════════════════════
   Dernière mise à jour : [DATE]

   1. QUI SOMMES-NOUS ?
   ──────────────────────────────────────────────────────────────
   [Nom de l'entreprise], [adresse], [email DPO ou contact RGPD]

   2. QUELLES DONNÉES COLLECTONS-NOUS ?
   ──────────────────────────────────────────────────────────────
   • Via le formulaire de contact : Prénom, Email, Message
   • Via la navigation : Adresse IP, cookies analytiques
   • Via la commande : Nom, adresse, données bancaires

   3. POURQUOI COLLECTONS-NOUS VOS DONNÉES ?
   ──────────────────────────────────────────────────────────────
   • Formulaire contact → Répondre à votre demande (base : consentement)
   • Commande → Livrer votre colis (base : contrat)
   • Analytics → Améliorer le site (base : intérêt légitime)

   4. COMBIEN DE TEMPS ?
   ──────────────────────────────────────────────────────────────
   • Données clients : 3 ans après dernier achat
   • Données comptables : 10 ans (obligation légale)
   • Cookies : 13 mois maximum

   5. QUI ACCÈDE À VOS DONNÉES ?
   ──────────────────────────────────────────────────────────────
   • Notre équipe commerciale (3 personnes habilitées)
   • Notre hébergeur : [Nom] — serveurs en France
   • Notre prestataire de paiement : [Nom] — certifié PCI-DSS

   6. VOS DROITS
   ──────────────────────────────────────────────────────────────
   Vous pouvez exercer vos droits (accès, rectification,
   effacement, portabilité, opposition) par email :
   [email@entreprise.fr]
   Réponse sous 1 mois.

   Réclamation possible auprès de la CNIL : www.cnil.fr
   ═══════════════════════════════════════════════════════════════
```

---

### II.C. Mentions sur un Formulaire

Tout formulaire de collecte doit comporter une **mention d'information courte** :

```
   EXEMPLE — Formulaire de contact
   ═══════════════════════════════════════════════════════════════

   ┌─────────────────────────────────────────────────────────┐
   │  Prénom : [_______________]                              │
   │  Email  : [_______________]                              │
   │  Message: [                                             ]│
   │           [                                             ]│
   │                                                          │
   │  ℹ️ Les données collectées via ce formulaire sont         │
   │  traitées par MaBoîte SARL pour répondre à votre         │
   │  demande (base : consentement). Elles sont conservées    │
   │  3 ans. Vous disposez d'un droit d'accès, rectification  │
   │  et effacement : rgpd@maboite.fr                         │
   │  En savoir plus : [Politique de confidentialité]         │
   │                                                          │
   │  [ ] J'accepte que mes données soient traitées          │
   │      pour répondre à ma demande ← (si base = consentement│
   │                                    uniquement si nécessaire)│
   │                                                          │
   │              [  ENVOYER  ]                               │
   └─────────────────────────────────────────────────────────┘
```

> 💡 **Note :** Si la base légale est le **contrat** ou l'**intérêt légitime**, pas besoin de case à cocher — mais l'information doit quand même être présente.

---

