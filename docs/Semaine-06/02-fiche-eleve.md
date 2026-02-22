---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Droits des Personnes : Procédures et Implémentation Technique"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 6*

---

## PARTIE III — Le Droit d'Accès (Art. 15)

### III.A. Définition

**Droit d'accès :** Toute personne peut demander à un responsable de traitement :
- La **confirmation** que des données la concernant sont traitées
- Une **copie** de ces données
- Des **informations** sur le traitement (finalité, destinataires, durée...)

**Délai de réponse :** 1 mois (prorogeable à 3 mois si complexe, avec information sous 1 mois)

---

### III.B. Implémentation Technique

```
   PROCÉDURE TECHNIQUE — Traiter une demande d'accès
   ═══════════════════════════════════════════════════════════════

   ① IDENTIFIER la personne (vérification d'identité)
   ──────────────────────────────────────────────────────────────
   • Demander une preuve d'identité (pour éviter fraudes)
   • ⚠️ Ne pas demander plus que nécessaire
     (copie pièce d'identité seulement si vraiment nécessaire)

   ② RECENSER toutes les données dans tous les systèmes
   ──────────────────────────────────────────────────────────────
   • Base de données principale
   • Sauvegardes (si accessibles facilement)
   • Emails échangés
   • Logs d'activité
   • CRM / ERP
   • Fichiers sur serveur

   ③ EXTRAIRE les données
   ──────────────────────────────────────────────────────────────
   Exemple SQL :
   SELECT u.*, o.*, a.*
   FROM users u
   LEFT JOIN orders o ON u.id = o.user_id
   LEFT JOIN addresses a ON u.id = a.user_id
   WHERE u.email = 'jean.dupont@email.fr'

   ④ FORMATER la réponse
   ──────────────────────────────────────────────────────────────
   • Format lisible (PDF, CSV, JSON)
   • Langage compréhensible pour la personne
   • PAS de dump SQL brut !

   ⑤ TRANSMETTRE de manière sécurisée
   ──────────────────────────────────────────────────────────────
   • Email chiffré OU lien sécurisé (HTTPS, lien expirant)
   • Jamais en clair par email non chiffré (données perso !)

   ⑥ TRACER la demande
   ──────────────────────────────────────────────────────────────
   • Enregistrer : Date demande, date réponse, contenu fourni
   • Conserver la preuve pendant minimum 5 ans
```

---

### III.C. Exemple de Réponse à une Demande d'Accès

```
   EMAIL DE RÉPONSE
   ═══════════════════════════════════════════════════════════════

   De     : rgpd@maboite.fr
   À      : jean.dupont@email.fr
   Objet  : Réponse à votre demande d'accès RGPD — Réf #2024-042

   Madame, Monsieur Dupont,

   Suite à votre demande d'accès reçue le [DATE], nous vous
   adressons ci-joint les données personnelles vous concernant
   traitées par MaBoîte SARL.

   DONNÉES TRANSMISES
   ──────────────────────────────────────────────────────────────
   • Vos informations de compte (voir fichier joint : données.pdf)
   • Historique de vos commandes (3 commandes)
   • Adresses de livraison enregistrées (2 adresses)

   INFORMATIONS SUR LE TRAITEMENT
   ──────────────────────────────────────────────────────────────
   • Responsable : MaBoîte SARL, 12 rue du Commerce, Paris
   • Finalités : Gestion des commandes, relation client
   • Durée de conservation : 3 ans après dernier achat
   • Destinataires : Équipe commerciale, transporteur, hébergeur
   • Droits : Vous pouvez demander rectification, effacement,
     portabilité à l'adresse ci-dessus.

   Cordialement,
   Le DPO — MaBoîte SARL
   ═══════════════════════════════════════════════════════════════
```

---

## PARTIE IV — Le Droit de Rectification (Art. 16)

### IV.A. Définition

**Droit de rectification :** Toute personne peut demander la **correction** de données inexactes ou incomplètes.

**Délai de réponse :** 1 mois

**Obligation de propagation :**
> Si les données rectifiées ont été communiquées à des tiers (partenaires, sous-traitants), le RT doit les **informer de la rectification**.

---

### IV.B. Implémentation Technique

```
   PROCÉDURE TECHNIQUE — Traiter une demande de rectification
   ═══════════════════════════════════════════════════════════════

   ① VÉRIFIER l'identité et la demande
   ──────────────────────────────────────────────────────────────
   • Confirmer que la donnée est bien inexacte
   • Demander preuve si nécessaire (ex : nouvelle adresse)

   ② METTRE À JOUR dans TOUS les systèmes
   ──────────────────────────────────────────────────────────────
   UPDATE users
   SET adresse = 'Nouvelle adresse',
       date_modification = NOW(),
       modifie_par = 'RGPD_request_#045'
   WHERE id = 12345

   Systèmes à mettre à jour :
   • BDD principale
   • CRM / ERP
   • Système de messagerie (carnet d'adresses)
   • Archives si accessibles

   ③ INFORMER LES TIERS si nécessaire
   ──────────────────────────────────────────────────────────────
   • Hébergeur, sous-traitant, partenaire ayant reçu les données

   ④ CONFIRMER la rectification à la personne
   ──────────────────────────────────────────────────────────────
   Email de confirmation avec la donnée corrigée

   ⑤ TRACER
   ──────────────────────────────────────────────────────────────
   • Enregistrer : ancienne valeur, nouvelle valeur, date, demande
```

---

## PARTIE V — Le Droit d'Opposition (Art. 21)

### V.A. Définition

**Droit d'opposition :** Toute personne peut s'**opposer à tout moment** au traitement de ses données pour des raisons tenant à sa situation particulière.

**2 cas distincts :**

```
   CAS 1 — PROSPECTION COMMERCIALE (droit ABSOLU)
   ═══════════════════════════════════════════════════════════════
   La personne peut s'opposer à la prospection commerciale
   SANS justification ET SANS exception possible.

   → Le responsable DOIT cesser immédiatement le traitement.

   Exemples :
   • Se désabonner d'une newsletter
   • Demander à ne plus recevoir de publicités personnalisées
   • Refuser le démarchage téléphonique

   Implémentation :
   ✅ Lien "Se désabonner" dans chaque email commercial
   ✅ Option dans les paramètres du compte
   ✅ Blocage en base de données (table opt-out)


   CAS 2 — AUTRES TRAITEMENTS (base : intérêt légitime)
   ═══════════════════════════════════════════════════════════════
   La personne peut s'opposer en invoquant des raisons
   personnelles liées à sa situation.

   Le responsable PEUT refuser si :
   → Motifs légitimes impérieux prévalant sur les intérêts de
     la personne
   → Nécessité de constater, exercer ou défendre des droits en
     justice

   Exemples :
   • S'opposer à l'utilisation de données pour de la
     recherche statistique
   • S'opposer au traitement de données de navigation pour
     amélioration du service
```

---

### V.B. Implémentation Technique (Prospection)

```
   GESTION DES OPT-OUT EN BDD
   ═══════════════════════════════════════════════════════════════

   TABLE opt_out_commerciale
   ──────────────────────────────────────────────────────────────
   id | user_id | date_optout     | canal       | source
   ───┼─────────┼─────────────────┼─────────────┼──────────────
   1  | 12345   | 2024-03-15 14h  | email       | lien email
   2  | 67890   | 2024-03-20 09h  | telephone   | appel entrant

   VÉRIFICATION AVANT ENVOI CAMPAGNE EMAIL
   ──────────────────────────────────────────────────────────────
   SELECT email FROM users u
   WHERE u.id NOT IN (
     SELECT user_id FROM opt_out_commerciale
     WHERE canal = 'email'
   )

   ⚠️ DÉLAI MAXIMAL
   ──────────────────────────────────────────────────────────────
   Opposition par email reçue →
   Personne retirée de toutes les listes dans les 24 heures
   (pas dans 1 mois — le droit d'opposition est immédiat pour
    la prospection)
```

---

## PARTIE VI — Le Droit à la Portabilité (Art. 20)

### VI.A. Définition

**Droit à la portabilité :** Toute personne peut récupérer ses données dans un **format structuré, couramment utilisé, lisible par machine** et les transmettre à un autre responsable.

**Conditions d'application :**
- La base légale est le **consentement** ou le **contrat** (pas obligation légale)
- Le traitement est **automatisé** (pas les fichiers papier)

---

### VI.B. Formats Acceptables

```
   FORMATS CONFORMES AU DROIT DE PORTABILITÉ
   ═══════════════════════════════════════════════════════════════

   ✅ JSON (recommandé — lisible par machines et humains)
   {
     "utilisateur": {
       "prenom": "Jean",
       "email": "jean@email.fr",
       "commandes": [
         {"id": 1, "date": "2024-01-15", "total": 59.90},
         {"id": 2, "date": "2024-02-20", "total": 129.00}
       ]
     }
   }

   ✅ CSV (simple, lisible par tableur)
   prenom,email,date_commande,total
   Jean,jean@email.fr,2024-01-15,59.90
   Jean,jean@email.fr,2024-02-20,129.00

   ✅ XML (structuré, interopérable)
   <utilisateur>
     <prenom>Jean</prenom>
     <email>jean@email.fr</email>
   </utilisateur>

   ❌ PDF (non lisible par machine pour import)
   ❌ Image scannée
   ❌ Dump SQL brut (non standard, illisible sans outil)
```

---

### VI.C. Exemples Réels de Portabilité

```
   EXEMPLES DE PORTABILITÉ DISPONIBLES
   ═══════════════════════════════════════════════════════════════

   GOOGLE TAKEOUT (https://takeout.google.com)
   ──────────────────────────────────────────────────────────────
   → Exporter toutes les données Google :
     Gmail, Drive, Photos, Calendrier, Contacts, YouTube...
   → Formats : ZIP contenant JSON + CSV + XML
   → Temps : quelques heures à quelques jours

   FACEBOOK / META DATA DOWNLOAD
   ──────────────────────────────────────────────────────────────
   → Paramètres > Vos informations Facebook > Transférer
   → Données : publications, photos, amis, messages...
   → Format : HTML ou JSON

   LINKEDIN ARCHIVE
   ──────────────────────────────────────────────────────────────
   → Paramètres > Données de confidentialité > Obtenir une copie
   → Données : connexions, messages, profil...
   → Format : CSV

   → Ces outils existent grâce au RGPD et au droit à la portabilité
```

---

## PARTIE VII — Récapitulatif des Droits et Procédures

```
   TABLEAU SYNTHÈSE DES 4 DROITS PRINCIPAUX
   ═══════════════════════════════════════════════════════════════

   DROIT        │ QUI PEUT    │ DÉLAI  │ EXCEPTIONS    │ TECHNIQUE
   ─────────────┼─────────────┼────────┼───────────────┼──────────────────
   ACCÈS        │ Toute       │ 1 mois │ Abus (demandes│ SQL SELECT + export
   (Art. 15)    │ personne    │ (3 si  │ répétées)     │ CSV/JSON/PDF
                │             │ complexe)              │
   ─────────────┼─────────────┼────────┼───────────────┼──────────────────
   RECTIFICATION│ Toute       │ 1 mois │ Aucune        │ SQL UPDATE +
   (Art. 16)    │ personne    │        │               │ informer tiers
   ─────────────┼─────────────┼────────┼───────────────┼──────────────────
   OPPOSITION   │ Toute       │ Immédiat│ Motifs légitimes│ Table opt-out +
   (Art. 21)    │ personne    │(prospec.)│(sauf prospec.)│ filtre campagnes
   ─────────────┼─────────────┼────────┼───────────────┼──────────────────
   PORTABILITÉ  │ Base légale │ 1 mois │ Obligation    │ Export JSON/CSV
   (Art. 20)    │ = consent.  │        │ légale exclue │ standardisé
                │ ou contrat  │        │               │
   ─────────────┴─────────────┴────────┴───────────────┴──────────────────

   RÈGLE D'OR : Répondre TOUJOURS dans le délai légal (1 mois)
               Tracer TOUTES les demandes et réponses
               Vérifier l'identité AVANT de fournir des données
```

---

## VIII. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Base légale** | Fondement juridique autorisant un traitement (parmi les 6 de l'Art. 6) |
| **Consentement libre** | Donné sans pression, avec vrai choix (refus possible sans pénalité) |
| **Consentement spécifique** | Un consentement distinct par finalité |
| **Consentement éclairé** | La personne comprend ce qu'elle accepte |
| **Consentement univoque** | Acte positif et clair (pas case pré-cochée) |
| **Dark pattern** | Conception trompeuse visant à manipuler le consentement |
| **Mentions d'information** | Informations obligatoires à fournir lors de la collecte |
| **Opt-out** | Mécanisme permettant de s'opposer ou de se désabonner |
| **Droit d'accès** | Obtenir une copie de ses données (délai 1 mois) |
| **Droit de rectification** | Corriger des données inexactes (délai 1 mois) |
| **Droit d'opposition** | S'opposer à un traitement (immédiat pour prospection) |
| **Droit à la portabilité** | Récupérer ses données en format structuré réutilisable |
| **Propagation** | Obligation d'informer les tiers d'une modification/suppression |

---

