---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Mises à Jour · CVE · Cycle de Vie des Logiciels"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 2*

---

## PARTIE VII — Pourquoi Mettre à Jour ?

### VII.A. Les 3 Raisons Critiques

**① CORRIGER LES FAILLES DE SÉCURITÉ**

Chaque logiciel contient des **bugs** (erreurs de programmation). Certains bugs créent des **failles de sécurité** (vulnérabilités) exploitables par des attaquants.

```
   CYCLE DE VIE D'UNE VULNÉRABILITÉ
   ═══════════════════════════════════════════════════════════════
   
   ① DÉCOUVERTE
   ──────────────────────────────────────────────────────────────
   Un chercheur en sécurité ou un hacker découvre une faille
   Ex : Faille dans Windows permettant d'exécuter du code à distance
   
   ② DIVULGATION
   ──────────────────────────────────────────────────────────────
   Le chercheur informe l'éditeur (Microsoft)
   Délai de correction : 90 jours (divulgation responsable)
   
   ③ PATCH (correctif)
   ──────────────────────────────────────────────────────────────
   L'éditeur développe un correctif (patch)
   Publication : Windows Update
   
   ④ FENÊTRE D'EXPLOITATION
   ──────────────────────────────────────────────────────────────
   Entre la publication du patch et l'installation par les utilisateurs
   → Les attaquants savent que la faille existe
   → Ils créent des exploits (codes malveillants)
   → Les PC non mis à jour sont vulnérables
   
   ⚠️ PLUS VOUS ATTENDEZ, PLUS LE RISQUE EST ÉLEVÉ
```

---

**② AMÉLIORER LA STABILITÉ ET LES PERFORMANCES**

Les mises à jour ne corrigent pas que des failles de sécurité. Elles incluent aussi :
- Correction de bugs (plantages, ralentissements)
- Amélioration des performances
- Compatibilité avec de nouveaux matériels
- Nouvelles fonctionnalités

---

**③ RESTER COMPATIBLE**

Les logiciels évoluent constamment. Sans mises à jour :
- Certains sites web ne fonctionneront plus (navigateur obsolète)
- Les fichiers récents ne s'ouvriront pas (Office ancien)
- Les périphériques ne seront pas reconnus (pilotes obsolètes)

---

### VII.B. Le Coût de l'Absence de Mise à Jour

**Cas réel : Equifax (2017)**

```
EQUIFAX — L'UNE DES PIRES CYBERATTAQUES DE L'HISTOIRE
═══════════════════════════════════════════════════════════════

CONTEXTE
─────────────────────────────────────────────────────────────
Equifax : Agence de notation de crédit américaine
Données : 147 millions de personnes (noms, adresses, numéros
          sécu, permis de conduire, cartes bancaires)

CHRONOLOGIE
─────────────────────────────────────────────────────────────
7 MARS 2017
Apache publie un correctif pour une faille critique dans
Apache Struts (CVE-2017-5638)
→ Equifax est informé du patch

MID-MAI 2017
Equifax N'A TOUJOURS PAS INSTALLÉ le patch (2 mois après)
Des hackers découvrent la faille non corrigée
Ils exploitent la vulnérabilité

MAI - JUILLET 2017
Les hackers exfiltrent 147 millions de dossiers
Vol massif de données sensibles pendant 76 jours

29 JUILLET 2017
Equifax découvre l'intrusion (trop tard)

7 SEPTEMBRE 2017
Equifax annonce publiquement la faille

CONSÉQUENCES
─────────────────────────────────────────────────────────────
• 147 millions de personnes exposées
• Action en justice : 700 millions $ de dédommagement
• PDG, DSI, et RSSI démissionnent
• Réputation de l'entreprise détruite
• Cours de l'action : -35%

CAUSE
─────────────────────────────────────────────────────────────
❌ Patch disponible depuis 2 mois
❌ Procédure de mise à jour non appliquée
❌ Surveillance insuffisante

→ Une simple mise à jour aurait empêché cette catastrophe
```

---

## PARTIE VIII — Comprendre les CVE

### VIII.A. Qu'est-ce qu'un CVE ?

**CVE** = **C**ommon **V**ulnerabilities and **E**xposures

C'est un **identifiant unique** attribué à chaque vulnérabilité de sécurité découverte.

```
   FORMAT D'UN CVE
   ═══════════════════════════════════════════════════════════════
   
   CVE-ANNÉE-NUMÉRO
   
   Exemples :
   CVE-2017-0144 → EternalBlue (faille Windows SMB - WannaCry)
   CVE-2017-5638 → Apache Struts (faille Equifax)
   CVE-2021-44228 → Log4Shell (faille Java Log4j)
```

---

### VIII.B. Base de Données CVE

Toutes les CVE sont référencées publiquement sur :
- **CVE.org** (base officielle)
- **NVD** (National Vulnerability Database - NIST)

**Informations contenues :**
- Identifiant (ex : CVE-2021-44228)
- Description de la vulnérabilité
- Logiciels affectés (ex : Log4j versions 2.0 à 2.14.1)
- Niveau de criticité (CVSS score : 0 à 10)
- Date de publication
- Correctifs disponibles

---

### VIII.C. Score CVSS (Criticité)

**CVSS** = **C**ommon **V**ulnerability **S**coring **S**ystem

C'est une échelle de **0 à 10** qui évalue la gravité d'une vulnérabilité.

```
   ÉCHELLE CVSS
   ═══════════════════════════════════════════════════════════════
   
   0.0         Aucun (pas de risque)
   
   0.1 - 3.9   🟢 FAIBLE
               Impact limité, exploitation difficile
   
   4.0 - 6.9   🟡 MOYEN
               Impact modéré, exploitation possible
   
   7.0 - 8.9   🟠 ÉLEVÉ
               Impact important, exploitation facile
   
   9.0 - 10.0  🔴 CRITIQUE
               Impact catastrophique, exploitation triviale
               
   Exemples :
   CVE-2017-0144 (EternalBlue) : 9.3 (CRITIQUE)
   CVE-2021-44228 (Log4Shell) : 10.0 (CRITIQUE)
```

**Priorité d'installation des patchs :**
- 🔴 **Critique (9-10)** : Installation **IMMÉDIATE** (même heure)
- 🟠 **Élevé (7-8.9)** : Installation sous **24-48 heures**
- 🟡 **Moyen (4-6.9)** : Installation sous **1 semaine**
- 🟢 **Faible (0.1-3.9)** : Installation lors de la maintenance planifiée

---

## PARTIE IX — Types de Mises à Jour

### IX.A. Classification par Contenu

**① MISES À JOUR DE SÉCURITÉ (Security Updates)**

```
CARACTÉRISTIQUES
─────────────────────────────────────────────────────────────
• Corrigent des failles de sécurité (CVE)
• Publiées dès que possible (parfois hors cycle)
• Marquées comme "critiques" ou "importantes"
• DOIVENT être installées en priorité

EXEMPLES
─────────────────────────────────────────────────────────────
Windows : "Mise à jour de sécurité pour Windows (KB5012345)"
Adobe : "Adobe Flash Player Security Update"
Chrome : "Chrome 120.0.6099.130 (Security Fix)"
```

**② MISES À JOUR FONCTIONNELLES (Feature Updates)**

```
CARACTÉRISTIQUES
─────────────────────────────────────────────────────────────
• Ajoutent de nouvelles fonctionnalités
• Améliorent l'interface utilisateur
• Publiées selon un calendrier régulier
• Optionnelles (mais recommandées)

EXEMPLES
─────────────────────────────────────────────────────────────
Windows : "Windows 11 23H2" (version semestrielle)
macOS : "macOS Sonoma 14.3" (mise à jour majeure)
Office : "Microsoft 365 - Nouvelles fonctionnalités Excel"
```

**③ CORRECTIFS (Bug Fixes)**

```
CARACTÉRISTIQUES
─────────────────────────────────────────────────────────────
• Corrigent des bugs (plantages, dysfonctionnements)
• N'ajoutent pas de fonctionnalités
• Améliorent la stabilité

EXEMPLES
─────────────────────────────────────────────────────────────
"Correction d'un problème de plantage au démarrage"
"Résolution d'un bug d'affichage dans Excel"
```

---

### IX.B. Classification par Logiciel

**① SYSTÈME D'EXPLOITATION**

```
WINDOWS
─────────────────────────────────────────────────────────────
• Windows Update (automatique ou manuel)
• "Patch Tuesday" : 2ème mardi de chaque mois
• Mises à jour cumulatives (incluent tous les patchs précédents)

LINUX
─────────────────────────────────────────────────────────────
• Ubuntu : apt update && apt upgrade
• Red Hat / CentOS : yum update
• Fréquence : Continue (rolling release) ou ponctuelle

macOS
─────────────────────────────────────────────────────────────
• Préférences Système > Mise à jour logicielle
• Fréquence : Mensuelle ou selon les besoins
```

**② NAVIGATEURS WEB**

```
CHROME / EDGE (Chromium)
─────────────────────────────────────────────────────────────
• Mise à jour automatique
• Nouvelle version toutes les 4 semaines
• Redémarrage du navigateur requis

FIREFOX
─────────────────────────────────────────────────────────────
• Mise à jour automatique
• Nouvelle version toutes les 4 semaines
```

**③ APPLICATIONS**

```
MICROSOFT OFFICE
─────────────────────────────────────────────────────────────
• Microsoft 365 : Mises à jour automatiques
• Office 2021/2019 : Mises à jour via Windows Update

ADOBE
─────────────────────────────────────────────────────────────
• Adobe Creative Cloud : Mises à jour automatiques
• Acrobat Reader : Mises à jour mensuelles

JAVA
─────────────────────────────────────────────────────────────
• Oracle publie des mises à jour trimestrielles (Critical Patch Update)
• ⚠️ Très ciblé par les attaquants → Mettre à jour impérativement
```

**④ ANTIVIRUS**

```
MISE À JOUR DES DÉFINITIONS (Signatures)
─────────────────────────────────────────────────────────────
• Fréquence : QUOTIDIENNE (voire plusieurs fois par jour)
• Contenu : Nouvelles signatures de virus découverts
• Essentiel : Un antivirus non à jour ne détecte pas les nouvelles menaces

MISE À JOUR DU MOTEUR
─────────────────────────────────────────────────────────────
• Fréquence : Mensuelle ou trimestrielle
• Contenu : Amélioration du moteur d'analyse
```

---

## PARTIE X — Cycle de Support (EOL)

### X.A. Qu'est-ce que l'EOL ?

**EOL** = **E**nd **O**f **L**ife = Fin de vie d'un logiciel

Quand un logiciel atteint son EOL :
- ❌ Plus de mises à jour de sécurité
- ❌ Plus de correctifs
- ❌ Plus de support technique
- ⚠️ **Le logiciel devient DANGEREUX** à utiliser

```
   CYCLE DE VIE D'UN LOGICIEL
   ═══════════════════════════════════════════════════════════════
   
   ① LANCEMENT (Release)
   ──────────────────────────────────────────────────────────────
   Le logiciel est publié
   Support complet : mises à jour, correctifs, nouvelles fonctionnalités
   
   ② SUPPORT MAINSTREAM (5-10 ans)
   ──────────────────────────────────────────────────────────────
   Mises à jour de sécurité régulières
   Ajout de nouvelles fonctionnalités
   Support technique disponible
   
   ③ SUPPORT ÉTENDU (Extended Support - 2-5 ans)
   ──────────────────────────────────────────────────────────────
   Mises à jour de sécurité uniquement (pas de nouvelles fonctionnalités)
   Support technique payant
   
   ④ FIN DE VIE (EOL)
   ──────────────────────────────────────────────────────────────
   ❌ PLUS AUCUNE MISE À JOUR
   ❌ PLUS DE SUPPORT
   ⚠️ DANGEREUX À UTILISER
```

---

### X.B. Exemples de Systèmes en EOL

| **Système** | **Date de sortie** | **Date EOL** | **Statut** |
|---|---|---|---|
| Windows XP | 2001 | 8 avril 2014 | ❌ EOL (10 ans) |
| Windows 7 | 2009 | 14 janvier 2020 | ❌ EOL (4 ans) |
| Windows 8.1 | 2013 | 10 janvier 2023 | ❌ EOL (1 an) |
| Windows 10 | 2015 | 14 octobre 2025 | ⚠️ Bientôt EOL |
| Windows 11 | 2021 | ~ 2031 | ✅ Supporté |

**Risques d'utiliser un système en EOL :**
- Failles de sécurité non corrigées
- Cible privilégiée des attaquants (savent qu'il n'y a plus de patch)
- Incompatibilité avec les logiciels récents
- Non-conformité (RGPD, normes ISO)

---

## XI. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Malware** | Logiciel malveillant (terme générique) |
| **Virus** | Malware qui s'attache à un fichier hôte et se réplique |
| **Ver (Worm)** | Malware autonome qui se propage automatiquement par le réseau |
| **Trojan** | Malware qui se fait passer pour un logiciel légitime |
| **Spyware** | Malware qui espionne l'utilisateur et vole des données |
| **Ransomware** | Malware qui chiffre les données et demande une rançon |
| **CVE** | Common Vulnerabilities and Exposures — identifiant de vulnérabilité |
| **CVSS** | Common Vulnerability Scoring System — score de criticité (0-10) |
| **Patch** | Correctif de sécurité publié par un éditeur |
| **EOL** | End Of Life — fin de vie d'un logiciel (plus de support) |
| **Backdoor** | Porte dérobée permettant un accès distant non autorisé |
| **Botnet** | Réseau de machines zombies contrôlées par un attaquant |
| **Payload** | Charge utile — action malveillante d'un malware |

---
