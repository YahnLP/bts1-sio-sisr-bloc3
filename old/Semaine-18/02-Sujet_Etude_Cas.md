---
author: YLP
title: 📝 ÉTUDE DE CAS - ÉPREUVE E6
---

---

# 📝 ÉTUDE DE CAS - ÉPREUVE E6
## Entreprise TechServices SARL

**Durée : 2 heures**
**Documents autorisés : AUCUN**

---

## CONSIGNES

- Répondez aux 4 questions sur feuilles blanches
- Numérotez clairement vos réponses
- Justifiez toutes vos propositions
- Soignez l'orthographe et la présentation
- Gestion du temps conseillée : 30 min/question

---

# CONTEXTE ENTREPRISE

## Présentation Générale

**TechServices SARL** est une entreprise de services informatiques créée en 2018.

| **Information** | **Détail** |
|-----------------|------------|
| **Secteur** | Services IT (infogérance, support, conseil) |
| **Effectif** | 80 salariés |
| **Sites** | • Siège social Lyon (60 personnes)<br>• Agence Paris (15 personnes)<br>• 5 commerciaux itinérants |
| **Clients** | PME (20-200 salariés), secteurs variés |
| **CA** | 8 M€ (2025) |

---

## Infrastructure IT Actuelle

### Serveurs (Lyon)

| **Serveur** | **Rôle** | **OS** | **Localisation réseau** |
|-------------|----------|--------|-------------------------|
| SRV-DC-01 | Contrôleur domaine (AD) | Windows Server 2019 | LAN (10.0.10.10) |
| SRV-FILES-01 | Serveur fichiers | Windows Server 2019 | LAN (10.0.10.20) |
| SRV-WEB-01 | Site vitrine entreprise | Ubuntu 20.04 | LAN (10.0.10.30) |
| SRV-APP-01 | CRM interne (SugarCRM) | Ubuntu 20.04 | LAN (10.0.10.40) |

### Postes Utilisateurs

- 75 PC Windows 10/11
- 5 MacBook (direction)
- 20 laptops nomades (commerciaux + télétravail)

### Réseau

- Réseau LAN : 10.0.10.0/24
- Box opérateur Fibre (1 Gb/s symétrique)
- Switch manageable HP (48 ports)
- 2 bornes Wi-Fi (SSID : "TechServices", WPA2)
- Pas de firewall dédié (seulement box opérateur)

---

## Situation Actuelle

### Contexte

TechServices connaît une **croissance rapide** (+30% effectif en 2 ans). L'infrastructure IT a été montée "au fil de l'eau" sans vision globale de sécurité.

**Un audit de sécurité externe** réalisé en janvier 2026 révèle de **nombreuses failles critiques**.

---

### Extrait Rapport d'Audit (10 pages)

**SYNTHÈSE EXÉCUTIVE**

| **Domaine** | **Note** | **Criticité** |
|-------------|----------|---------------|
| Gestion des accès | 3/10 | 🔴 CRITIQUE |
| Sauvegardes | 4/10 | 🔴 CRITIQUE |
| Sécurité réseau | 2/10 | 🔴 CRITIQUE |
| Protection données (RGPD) | 5/10 | 🟠 ÉLEVÉE |
| Sensibilisation utilisateurs | 3/10 | 🟠 ÉLEVÉE |

**PRINCIPALES FAILLES IDENTIFIÉES**

1. **Gestion des accès**
   - Pas de GPO (Stratégie de Groupe) configurée
   - Mots de passe faibles autorisés (ex: "azerty", "123456")
   - Comptes inactifs non désactivés (15 comptes d'anciens salariés actifs)
   - Partages réseau sans droits NTFS (tout le monde accède à tout)
   - Pas d'authentification multi-facteurs (MFA)

2. **Sauvegardes**
   - Sauvegardes manuelles (USB externe, irrégulières)
   - Dernière sauvegarde complète : **3 mois**
   - Pas de test de restauration
   - Sauvegarde stockée dans même local que serveurs (risque incendie/inondation)

3. **Sécurité réseau**
   - Serveur web accessible depuis Internet **sans protection** (pas de DMZ)
   - Site vitrine en **HTTP** (pas de certificat SSL/TLS)
   - Wi-Fi avec mot de passe faible ("techservices2024")
   - Pas de segmentation réseau (tout dans 10.0.10.0/24)
   - Pas de firewall périmétrique
   - VPN absent (accès RDP direct depuis Internet, port 3389 ouvert)

4. **Conformité RGPD**
   - Base CRM contient données personnelles clients
   - Pas de registre des traitements
   - Pas de DPO (Délégué Protection Données) nommé
   - Politique confidentialité site web obsolète (2020)

5. **Sensibilisation**
   - Aucune formation sécurité depuis 2 ans
   - Incidents phishing récents (3 employés ont cliqué)
   - Pas de procédure signalement incident

---

### Incident Récent (Février 2026)

Le **12 février 2026**, un employé (service compta) reçoit un email de phishing :

```
De : facturation@techservices-invoice.com
Objet : [URGENT] Facture impayée #45782
Pièce jointe : Facture_45782.zip

Bonjour,

Veuillez régler la facture ci-jointe sous 48h.
En cas de non-paiement, poursuites judiciaires engagées.

Cordialement,
Service Comptabilité
```

L'employé **ouvre le fichier ZIP** → Ransomware **CryptoLocker** s'exécute.

**Conséquences** :
- 1 200 fichiers comptabilité chiffrés (irrécupérables sans sauvegarde)
- Perte de données : **6 semaines** de compta (janvier-février 2026)
- Rançon demandée : **50 000 € en Bitcoin**
- Activité comptabilité **interrompue 3 jours**
- Reconstitution données : **2 semaines** (saisie manuelle)

**Décision DSI** : Ne PAS payer la rançon (recommandation ANSSI).

---

## Mission

**Vous êtes consultant(e) cybersécurité externe** mandaté(e) par TechServices pour proposer un **plan d'action sécurité prioritaire**.

La direction vous demande des propositions **concrètes, justifiées et réalistes** (budget limité : 30 000 € matériel + 20 jours/homme).

---

# QUESTIONS

## Question 1 — Analyse de l'Existant (5 points)

Analysez l'infrastructure actuelle de TechServices et identifiez les **5 principales vulnérabilités critiques**. Pour chaque vulnérabilité, précisez :
- En quoi consiste la faille
- Quel risque elle représente (impact potentiel)
- Quel incident récent ou futur elle pourrait causer

*(Attendu : 1 page minimum)*

---

## Question 2 — Conformité RGPD (4 points)

L'entreprise traite des **données personnelles clients** dans son CRM (nom, prénom, email, téléphone, coordonnées bancaires pour facturation).

2.1. Listez les **5 obligations RGPD** que TechServices ne respecte pas actuellement (citez les articles RGPD).

2.2. Proposez un **plan d'action RGPD** en 3 étapes prioritaires pour se mettre en conformité.

*(Attendu : 3/4 page)*

---

## Question 3 — Propositions Techniques Sécurité (7 points)

La direction vous demande de **sécuriser l'infrastructure** sur 3 axes :

### 3.1 — Gestion des accès (2 points)

Proposez **2 mesures techniques** pour renforcer la gestion des accès (GPO, droits, authentification). Précisez pour chaque mesure :
- Description technique
- Mise en œuvre (comment, sur quels serveurs/postes)
- Bénéfice sécurité

### 3.2 — Sauvegardes (2 points)

Concevez une **stratégie de sauvegarde automatisée** respectant la règle 3-2-1. Précisez :
- Fréquence des sauvegardes (complète, incrémentielle/différentielle)
- Support de stockage (local, distant, cloud)
- Procédure test restauration

### 3.3 — Segmentation réseau (3 points)

Proposez une **architecture réseau sécurisée** avec segmentation en 3 zones (LAN, DMZ, Internet). Fournissez :
- Schéma réseau (dessin ou description précise)
- Placement des serveurs dans chaque zone (justifié)
- 5 règles firewall principales (source, destination, port, action, justification)

*(Attendu : 2 pages minimum)*

---

## Question 4 — Justification et Priorisation (4 points)

4.1. Parmi toutes les mesures proposées en Q3, classez-les par **ordre de priorité** (1 = plus urgent). Justifiez votre classement en fonction :
- Du risque couvert
- De l'urgence (incident récent)
- De la faisabilité (délai, budget, complexité)

4.2. La direction hésite entre **2 options** pour la segmentation réseau :
- **Option A** : Firewall matériel pro (FortiGate 60F, ~5 000 €, complexe à configurer)
- **Option B** : Firewall logiciel open source (pfSense sur VM, gratuit, formation nécessaire)

Réalisez un **tableau comparatif** (avantages/inconvénients) et **recommandez une option** en justifiant.

*(Attendu : 1 page)*

---

# ANNEXES

## Annexe 1 — Extrait Active Directory

```
OU=TechServices
├── OU=Utilisateurs
│   ├── OU=Direction (5 utilisateurs)
│   ├── OU=Comptabilité (8 utilisateurs)
│   ├── OU=Technique (25 utilisateurs)
│   ├── OU=Commercial (15 utilisateurs)
│   └── OU=RH (4 utilisateurs)
└── OU=Ordinateurs
    ├── OU=Serveurs (4 serveurs)
    └── OU=Postes (75 postes)

Groupes de sécurité :
- Admins du domaine (3 membres)
- Utilisateurs du domaine (80 membres)
```

---

## Annexe 2 — Partages Réseau Actuels

| **Partage** | **Chemin** | **Droits actuels** | **Contenu** |
|-------------|------------|--------------------|-------------|
| \\SRV-FILES-01\Public | D:\Partages\Public | Tout le monde : Modification | Docs généraux |
| \\SRV-FILES-01\Compta | D:\Partages\Compta | Tout le monde : Lecture | Fichiers comptables |
| \\SRV-FILES-01\RH | D:\Partages\RH | Tout le monde : Lecture | Fiches paie, contrats |
| \\SRV-FILES-01\Direction | D:\Partages\Direction | Admins : Contrôle total | Docs confidentiels |

---

## Annexe 3 — Budget Disponible

| **Poste** | **Budget** |
|-----------|------------|
| Matériel (firewall, NAS...) | 30 000 € |
| Prestations externes (consultant) | 20 jours/homme (400 €/jour) |
| Formation utilisateurs | 5 000 € |
| **TOTAL** | **43 000 €** |

---

*Fin du Sujet*

**Bon courage !**
