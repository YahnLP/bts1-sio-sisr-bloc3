---
author: YLP
title: 📖 FICHE DE COURS ÉLÈVE
---

# Semaine 19 — BLOC 3
## 📖 FICHE DE COURS ÉLÈVE
### Audit de Vulnérabilités (Introduction) · Scans Basiques · Interprétation des Résultats

---

> **Compétences travaillées :** B3.1 · B3.2 · B3.3 · B3.4
> **Semaine :** S19 — Année 1 — BTS SIO SISR

---

## Partie 1 — L'Audit de Vulnérabilités : Pourquoi et Pour Qui ?

### 1.1 Définition

Un **audit de vulnérabilités** est une analyse technique structurée d'un système informatique (serveur, réseau, poste de travail, application) qui vise à **identifier les failles de sécurité** avant qu'un attaquant ne les exploite.

> 💡 **Analogie :** Un audit de vulnérabilités, c'est comme faire inspecter la sécurité incendie d'un bâtiment. On cherche les portes non verrouillées, les extincteurs périmés, les issues de secours bloquées — AVANT qu'un incendie ne se déclare.

```
┌─────────────────────────────────────────────────────────┐
│              CYCLE DE L'AUDIT DE SÉCURITÉ               │
│                      (vision ITIL)                      │
│                                                         │
│   PLANIFIER  ──►  SCANNER  ──►  ANALYSER                │
│       ▲                              │                  │
│       │                              ▼                  │
│   RECOMMENCER ◄── CORRIGER  ◄── PRIORISER               │
│                                                         │
│   ↑ Ce cycle = Amélioration Continue des Services       │
└─────────────────────────────────────────────────────────┘
```
*[Illustration : Cycle en boucle de l'audit de sécurité selon la logique ITIL d'amélioration continue. Chaque étape s'enchaîne de façon régulière et répétée.]*

### 1.2 L'Audit dans la Gestion de Services (ITIL)

Dans le référentiel ITIL (Information Technology Infrastructure Library), l'audit de vulnérabilités s'inscrit dans plusieurs processus :

| **Processus ITIL** | **Lien avec l'audit** |
|---|---|
| **Gestion des incidents** | L'audit aide à comprendre comment un incident a pu se produire |
| **Gestion des problèmes** | L'audit identifie les causes racines des vulnérabilités récurrentes |
| **Gestion des changements** | Avant tout changement majeur, un audit vérifie l'impact sécuritaire |
| **Amélioration continue** | L'audit régulier mesure la progression du niveau de sécurité |

### 1.3 Qui Peut Réaliser un Audit ? Le Cadre Légal

⚠️ **ATTENTION — POINT JURIDIQUE ESSENTIEL**

```
┌─────────────────────────────────────────────────────────────┐
│  ARTICLE 323-1 DU CODE PÉNAL (France)                       │
│                                                             │
│  "Le fait d'accéder ou de se maintenir, frauduleusement,   │
│  dans tout ou partie d'un système de traitement automatisé  │
│  de données est puni de deux ans d'emprisonnement et de     │
│  60 000 euros d'amende."                                    │
│                                                             │
│  → Scanner un réseau sans autorisation = INFRACTION PÉNALE  │
└─────────────────────────────────────────────────────────────┘
```

**Règle absolue :** Un scan ne peut être effectué que sur :
- Votre propre infrastructure
- Une infrastructure pour laquelle vous avez une **autorisation écrite explicite**
- Un environnement de laboratoire (VMs, réseau isolé)

**En entreprise :** L'audit est mandaté par la direction, documenté, et effectué dans un cadre défini. Le technicien SISR qui réalise l'audit dispose d'un **bon de commande ou lettre de mission** signée.

---

## Partie 2 — Les Types de Scans

### 2.1 Vue d'Ensemble

```
┌────────────────────────────────────────────────────────────────┐
│                     TYPES DE SCANS                             │
│                                                                │
│  SCAN RÉSEAU         SCAN DE PORTS       SCAN DE SERVICES      │
│  "Qui est là ?"      "Quelles portes     "Quel logiciel        │
│                       sont ouvertes ?"    écoute ?"            │
│       │                    │                   │               │
│       ▼                    ▼                   ▼               │
│  SCAN DE VULNÉRABILITÉS                                        │
│  "Est-ce que ce service a des failles connues ?"               │
│                                                                │
│  Complexité et profondeur croissantes  ──────────────────►     │
└────────────────────────────────────────────────────────────────┘
```
*[Illustration : Pyramide ou progression horizontale des types de scans, du plus simple (découverte réseau) au plus approfondi (vulnérabilités). Montre que chaque niveau s'appuie sur le précédent.]*

| **Type de scan** | **Ce qu'il détecte** | **Outil courant** |
|---|---|---|
| **Scan réseau (ping sweep)** | Hôtes actifs sur le réseau | Nmap, `ping` |
| **Scan de ports** | Ports ouverts / fermés / filtrés | Nmap |
| **Scan de services** | Logiciels et versions en écoute | Nmap `-sV` |
| **Scan OS** | Système d'exploitation de la cible | Nmap `-O` |
| **Scan de vulnérabilités** | CVE connues sur les versions détectées | OpenVAS, Nessus, Nmap NSE |

### 2.2 Les États d'un Port

| **État** | **Signification** |
|---|---|
| **open** | Un service écoute et répond sur ce port |
| **closed** | Aucun service n'écoute, mais le port est accessible |
| **filtered** | Un pare-feu ou filtre bloque les sondes (on ne sait pas) |

> 💡 **À retenir pour l'examen :** Un port `open` n'est pas forcément dangereux (le port 443 HTTPS est normal sur un serveur web). C'est la **version du service** qui détermine si une faille existe.

---

## Partie 3 — Nmap : L'Outil de Référence

### 3.1 Présentation

**Nmap** (Network Mapper) est un outil open-source gratuit, créé en 1997, utilisé dans le monde entier pour l'exploration réseau et l'audit de sécurité. Il fonctionne sous Linux, Windows et macOS.

```
┌────────────────────────────────────────┐
│          NMAP EN UNE IMAGE             │
│                                        │
│  VOUS                   CIBLE          │
│  [PC]  ──── sondes ──► [Serveur]       │
│        ◄── réponses ──              │
│                                        │
│  Nmap interprète les réponses          │
│  et dresse un portrait de la cible     │
└────────────────────────────────────────┘
```
*[Illustration : Schéma simple montrant un poste émettant des "sondes" (paquets réseau) vers un serveur cible, qui répond ou non. Nmap analyse ces réponses pour dresser le portrait de la cible.]*

### 3.2 Commandes Essentielles à Connaître

```bash
# 1. Scan de découverte réseau (quels hôtes sont actifs ?)
nmap -sn 192.168.1.0/24

# 2. Scan des ports les plus courants (top 1000 ports)
nmap 192.168.1.10

# 3. Scan de tous les ports (0-65535)
nmap -p- 192.168.1.10

# 4. Scan avec détection de services ET versions
nmap -sV 192.168.1.10

# 5. Scan avec détection du système d'exploitation
nmap -O 192.168.1.10

# 6. Scan complet (services + OS + scripts de base)
nmap -A 192.168.1.10

# 7. Scan de ports spécifiques
nmap -p 22,80,443,3389 192.168.1.10
```

> ⚠️ **Rappel :** En TP, ces commandes ne s'utilisent que sur votre VM cible en environnement isolé.

### 3.3 Exemple de Résultat Nmap Annoté

```
Starting Nmap 7.94 at 2024-06-01 09:15
Nmap scan report for 192.168.1.50
Host is up (0.00050s latency).           ← La cible répond bien

PORT     STATE  SERVICE    VERSION
22/tcp   open   ssh        OpenSSH 7.2p2  ← SSH ouvert — version ancienne !
80/tcp   open   http       Apache 2.4.7   ← Serveur web — version ancienne !
443/tcp  open   https      Apache 2.4.7
3389/tcp open   ms-wbt-server Microsoft Remote Desktop  ← RDP exposé !
445/tcp  open   microsoft-ds Windows 7 / Server 2008    ← SMB sur Windows 7 !

OS detection: Microsoft Windows 7 (96%)  ← OS obsolète non supporté !

Nmap done: 1 IP address (1 host up) scanned in 12.34 seconds
```

**Analyse de ce résultat :**

| **Observation** | **Risque** | **Action recommandée** |
|---|---|---|
| OpenSSH 7.2p2 | Versions vulnérables connues (CVE multiples) | Mettre à jour SSH |
| Apache 2.4.7 | Nombreuses CVE critiques sur cette version | Mettre à jour Apache |
| RDP (3389) ouvert | Attaques par force brute, BlueKeep | Fermer ou filtrer par IP |
| SMB (445) + Windows 7 | EternalBlue / WannaCry exploitable | Isoler ou migrer immédiatement |
| Windows 7 détecté | OS en fin de vie, aucun correctif de sécurité | Migration urgent |

---

## Partie 4 — Le Score CVSS : Prioriser les Risques

### 4.1 Qu'est-ce que le CVSS ?

Le **CVSS (Common Vulnerability Scoring System)** est un standard international qui permet de mesurer la gravité d'une vulnérabilité de sécurité. Il produit un score de **0 à 10**.

Chaque vulnérabilité connue est répertoriée dans une base publique sous un identifiant **CVE** (Common Vulnerabilities and Exposures) — ex : **CVE-2017-0144** (EternalBlue / WannaCry).

### 4.2 Tableau de Criticité CVSS

```
╔═══════════════════════════════════════════════════════════════╗
║                   ÉCHELLE DE CRITICITÉ CVSS                   ║
╠═══════════════╦═══════════════╦═══════════════════════════════╣
║ Score         ║ Niveau        ║ Action                        ║
╠═══════════════╬═══════════════╬═══════════════════════════════╣
║ 9.0 – 10.0    ║ 🔴 CRITIQUE   ║ Corriger IMMÉDIATEMENT        ║
║ 7.0 – 8.9     ║ 🟠 ÉLEVÉ      ║ Corriger dans la semaine      ║
║ 4.0 – 6.9     ║ 🟡 MOYEN      ║ Planifier une correction      ║
║ 0.1 – 3.9     ║ 🟢 FAIBLE     ║ Surveiller                    ║
║ 0.0           ║ ⚪ AUCUN      ║ Information seulement         ║
╚═══════════════╩═══════════════╩═══════════════════════════════╝
```

> 💡 **Exemple réel :** CVE-2017-0144 (EternalBlue, exploité par WannaCry) → Score CVSS : **9.3 (CRITIQUE)**. Cette faille affecte SMBv1 sur Windows. Action immédiate : désactiver SMBv1, appliquer MS17-010.

### 4.3 La Notion de CVE

```
┌────────────────────────────────────────────────────────────┐
│  CVE-2017-0144                                             │
│   │    │    │                                              │
│   │    │    └── Numéro d'ordre (ordre de découverte)       │
│   │    └─────── Année de découverte                        │
│   └──────────── Préfixe standardisé (Common Vulnerability) │
│                                                            │
│  Où chercher ? → https://nvd.nist.gov (base NVD)           │
│                  https://cve.mitre.org                     │
└────────────────────────────────────────────────────────────┘
```
*[Illustration : Décomposition d'un identifiant CVE avec flèches annotées vers chaque partie de l'identifiant. En dessous, logos ou URL des deux bases de référence NVD et MITRE.]*

---

## Partie 5 — La Fiche d'Audit : Documenter les Résultats

Un audit n'a de valeur que s'il est **documenté**. Le technicien SISR produit une **fiche d'audit** (ou rapport) qui sera remise au responsable ou au client.

### 5.1 Structure d'une Fiche d'Audit Basique

```
═══════════════════════════════════════════════════════════════
        FICHE D'AUDIT DE VULNÉRABILITÉS
═══════════════════════════════════════════════════════════════
Date de l'audit    : ___________________________________
Auditeur           : ___________________________________
Cible auditée      : ___________________________________
Périmètre          : ___________________________________
Autorisation       : ☐ Oui  (Réf. document : ___________)
═══════════════════════════════════════════════════════════════

SECTION 1 — DÉCOUVERTE RÉSEAU
----------------------------------------------
Plage réseau scannée   : ___________________
Nombre d'hôtes actifs  : ___________________
Hôtes détectés         :
  - _____________________________________________
  - _____________________________________________

SECTION 2 — ANALYSE DES PORTS ET SERVICES
----------------------------------------------
| Hôte IP     | Port | Service | Version | État |
|-------------|------|---------|---------|------|
|             |      |         |         |      |
|             |      |         |         |      |

SECTION 3 — VULNÉRABILITÉS IDENTIFIÉES
----------------------------------------------
| CVE          | Service concerné | Score CVSS | Criticité | Action recommandée |
|--------------|-----------------|------------|-----------|--------------------|
|              |                 |            |           |                    |
|              |                 |            |           |                    |

SECTION 4 — SYNTHÈSE ET PRIORITÉS
----------------------------------------------
Nombre de vulnérabilités critiques  : ______
Nombre de vulnérabilités élevées    : ______
Nombre de vulnérabilités moyennes   : ______
Nombre de vulnérabilités faibles    : ______

RECOMMANDATION PRINCIPALE : ____________________________
_______________________________________________________

Signature auditeur : _________________ Date : _________
═══════════════════════════════════════════════════════════════
```

---

## Partie 6 — Synthèse Bloc 3 Année 1 : Carte des Connaissances

### 6.1 Vue d'Ensemble du Bloc 3 A1

```
                        ┌─────────────────────┐
                        │  BLOC 3 — SÉCURITÉ  │
                        │  DES SERVICES IT    │
                        └─────────┬───────────┘
                                  │
           ┌──────────────────────┼──────────────────────┐
           ▼                      ▼                      ▼
   ┌───────────────┐     ┌────────────────┐    ┌──────────────────┐
   │   MENACES &   │     │   PROTECTION   │    │   RÉGLEMENTATION │
   │  ATTAQUES     │     │   TECHNIQUE    │    │   (RGPD)         │
   └───────┬───────┘     └───────┬────────┘    └────────┬─────────┘
           │                     │                      │
  • Ransomware          • Mots de passe          • Principes (7)
  • Phishing            • MFA / 2FA              • Bases légales (6)
  • Ingénierie sociale  • Mises à jour           • Droits personnes
  • DDoS                • Sauvegardes 3-2-1      • Rôles (RT / ST)
  • Intrusion réseau    • Pare-feu               • Sanctions CNIL
                        • VPN                    • Registre traitements
                        • Chiffrement            • Violation de données
                        • Audit de vulnérabilités
```
*[Illustration : Carte mentale (mind map) en arborescence avec le Bloc 3 au centre, trois branches principales (Menaces, Protection, Réglementation), et les sous-thèmes associés. Idéalement en couleurs : rouge pour les menaces, vert pour la protection, bleu pour la réglementation.]*

### 6.2 Tableau de Révision RGPD Essentiel

| **Concept** | **Définition à retenir** |
|---|---|
| **Donnée personnelle** | Toute information permettant d'identifier directement ou indirectement une personne physique |
| **Traitement** | Toute opération sur des données personnelles (collecte, stockage, utilisation, suppression) |
| **Responsable de traitement (RT)** | Entité qui détermine les finalités et moyens du traitement |
| **Sous-traitant (ST)** | Entité qui traite les données pour le compte du RT |
| **Consentement** | Accord libre, spécifique, éclairé et univoque de la personne concernée |
| **Droit à l'effacement** | Droit de demander la suppression de ses données (dit "droit à l'oubli") |
| **Violation de données** | Tout incident affectant la confidentialité, disponibilité ou intégrité des données |
| **Notification CNIL** | Obligation de notifier une violation grave dans les **72 heures** |
| **Sanction maximale** | 20 millions € ou **4 % du CA mondial** (la plus élevée des deux) |
| **DPO** | Délégué à la Protection des Données — obligatoire pour certains organismes |

### 6.3 Tableau de Révision Sécurité de Base

| **Mesure** | **Pourquoi c'est important** | **Standard/Règle de référence** |
|---|---|---|
| **Mot de passe robuste** | Résiste aux attaques par dictionnaire et force brute | 12+ caractères, complexe, unique par service |
| **MFA / 2FA** | Un mot de passe seul peut être volé — le second facteur protège | Google Authenticator, TOTP |
| **Mises à jour** | Les failles sont publiées — les correctifs bouchent les trous | Délai recommandé : < 72h pour critiques |
| **Sauvegardes 3-2-1** | Seule protection efficace contre le ransomware | 3 copies, 2 supports, 1 hors site |
| **Pare-feu** | Filtre les connexions non autorisées | Règles : tout bloquer par défaut, n'autoriser que le nécessaire |
| **VPN** | Chiffre les communications sur réseaux non maîtrisés | Utilisation obligatoire sur Wi-Fi public |
| **Chiffrement des données** | Protège la confidentialité même en cas de vol physique | BitLocker, VeraCrypt, TLS/HTTPS |
| **Audit de vulnérabilités** | Détecte les failles avant les attaquants | Nmap, OpenVAS — cycle régulier |
| **Sensibilisation** | Le facteur humain reste la principale cause d'incidents | Formation régulière des utilisateurs |

---

## Vocabulaire Clé à Maîtriser pour l'Examen

| **Terme** | **Définition** |
|---|---|
| **Audit de vulnérabilités** | Analyse technique structurée visant à identifier les failles de sécurité d'un système |
| **Nmap** | Outil open-source de scan réseau permettant de découvrir les hôtes, ports ouverts et services |
| **CVE** | Common Vulnerabilities and Exposures — identifiant unique d'une vulnérabilité connue |
| **CVSS** | Common Vulnerability Scoring System — score de 0 à 10 mesurant la gravité d'une vulnérabilité |
| **Port** | Point de communication logique sur un système (0 à 65535) |
| **Service** | Logiciel qui écoute sur un port et répond aux requêtes |
| **Scan de ports** | Technique permettant de déterminer quels ports d'un hôte sont ouverts, fermés ou filtrés |
| **Vulnérabilité** | Faiblesse dans un système pouvant être exploitée par un attaquant |
| **Exploit** | Programme ou technique permettant d'exploiter une vulnérabilité |
| **Patch** | Correctif logiciel comblant une vulnérabilité |
| **Rapport d'audit** | Document structuré listant les vulnérabilités trouvées, leur criticité et les actions recommandées |
| **NVD** | National Vulnerability Database — base de données de référence des CVE et scores CVSS |

---

*Fiche de Cours Élève S19 BLOC 3 — BTS SIO SISR — Année 1 — Version 1.0*
*Compétences : B3.1 · B3.2 · B3.3 · B3.4*
