---
author: YLP
title: 📖 FICHE DE PRÉPARATION ÉLÈVE
---

# Semaine 20 — BLOC 3
## 📖 FICHE DE PRÉPARATION ÉLÈVE
### Comment Réussir l'Épreuve E6 — Méthodologie de l'Étude de Cas

---

> **Cette fiche est distribuée AVANT l'examen blanc.** Lisez-la attentivement pendant le briefing de 20 minutes. Elle ne sera pas autorisée pendant l'épreuve.

---

## Qu'est-ce que l'Épreuve E6 ?

L'épreuve **E6 — Parcours de professionnalisation** évalue votre capacité à :
- **Analyser** une situation professionnelle réelle ou simulée
- **Mobiliser** les compétences techniques et réglementaires acquises
- **Proposer** des solutions argumentées, priorisées et réalistes
- **Communiquer** de façon professionnelle, claire et structurée

> 💡 L'E6 ne teste pas uniquement ce que vous savez — elle teste **comment vous raisonnez et comment vous vous exprimez** en situation professionnelle.

---

## La Méthode en 5 Étapes — À Appliquer pour Chaque Question

```
╔════════════════════════════════════════════════════════════════╗
║  ÉTAPE 1 → LIRE LA QUESTION DEUX FOIS                         ║
║  Identifiez : Que demande-t-on exactement ?                   ║
║  Quel(s) document(s) utiliser ?                               ║
╠════════════════════════════════════════════════════════════════╣
║  ÉTAPE 2 → SITUER DANS LE CONTEXTE                            ║
║  Reliez la question à l'entreprise du sujet.                  ║
║  "Dans le cas de CLINOVA SANTÉ..."                            ║
╠════════════════════════════════════════════════════════════════╣
║  ÉTAPE 3 → NOMMER LA COMPÉTENCE MOBILISÉE                     ║
║  "Cette situation relève de la compétence B3.X..."            ║
║  (B3.1 menaces / B3.2 mesures / B3.3 RGPD / B3.4 audit)      ║
╠════════════════════════════════════════════════════════════════╣
║  ÉTAPE 4 → RÉPONDRE AVEC PRÉCISION TECHNIQUE                  ║
║  Utilisez le vocabulaire exact : CVE, CVSS, RDP, DPO...       ║
║  Citez des outils réels, des articles de loi précis.          ║
╠════════════════════════════════════════════════════════════════╣
║  ÉTAPE 5 → CONCLURE PAR L'IMPACT / LA RECOMMANDATION          ║
║  Chaque réponse doit finir par une action ou un résultat.     ║
╚════════════════════════════════════════════════════════════════╝
```

---

## Gestion du Temps — 2 heures (120 minutes)

| **Phase** | **Durée** | **Ce que vous faites** |
|---|---|---|
| Lecture du sujet et annotation | 15 min | Soulignez les mots-clés, repérez les documents à utiliser par question |
| **Partie A** — Analyse technique | 45 min | A1 : 12 min / A2 : 10 min / A3 : 8 min / A4 : 10 min / A5 : 5 min |
| **Partie B** — RGPD | 30 min | B1 : 10 min / B2 : 8 min / B3 : 12 min |
| **Partie C** — Synthèse | 25 min | C1 : 18 min / C2 : 7 min |
| Relecture | 5 min | Vérifiez les numéros de questions, l'orthographe, les oublis |

> ⚠️ **Ne restez jamais bloqué(e) plus de 5 minutes sur une question.** Passez à la suivante et revenez si le temps le permet.

---

## Ce que les Correcteurs Valorisent

### ✅ Formulations qui font la différence

| **Mauvaise formulation** | **Bonne formulation** |
|---|---|
| "C'est dangereux" | "Cette configuration expose le service à une attaque par force brute sur RDP, rendue possible par l'absence de politique de complexité des mots de passe." |
| "Il faut mettre à jour" | "Il convient d'appliquer le correctif MS17-010 pour combler la vulnérabilité EternalBlue (CVE-2017-0144, CVSS 9.3) sur le service SMBv1." |
| "C'est une donnée personnelle" | "Les dossiers médicaux constituent des données de santé au sens de l'article 9 du RGPD, catégorie de données sensibles dont le traitement est en principe interdit sauf exceptions." |
| "Il faut notifier la CNIL" | "En application de l'article 33 du RGPD, CLINOVA SANTÉ doit notifier la CNIL dans les 72 heures suivant la découverte de la violation." |

### ✅ Structure d'une bonne note de synthèse (Question C1)

```
STRUCTURE RECOMMANDÉE POUR LA NOTE DE SYNTHÈSE

[En-tête]
À : M./Mme [Directeur Général]
De : [Votre nom], Technicien SISR — DSI
Objet : État de la sécurité du SI et plan de mise en conformité
Date : ...

[Paragraphe 1 — Introduction]
"Suite à l'audit de sécurité réalisé le [date], ce rapport présente..."

[Paragraphe 2 — Constats]
"Notre système d'information présente plusieurs vulnérabilités..."
→ Rédigez en langage clair, évitez le jargon brut

[Paragraphe 3 — Risques majeurs]
"Ces failles exposent notre établissement à trois risques principaux..."
→ Technique, financier, légal (RGPD)

[Paragraphe 4 — Plan d'actions]
"Nous recommandons les actions suivantes, classées par urgence..."

[Conclusion]
"La formation des utilisateurs constitue un levier essentiel..."
```

---

## Points de Cours Essentiels à Avoir en Tête

### Tableau CVSS — Indispensable

| **Score** | **Niveau** | **Délai d'action** |
|---|---|---|
| 9.0 – 10.0 | 🔴 CRITIQUE | Immédiatement |
| 7.0 – 8.9 | 🟠 ÉLEVÉ | Dans la semaine |
| 4.0 – 6.9 | 🟡 MOYEN | Planifier |
| 0.1 – 3.9 | 🟢 FAIBLE | Surveiller |

### Les 6 Bases Légales du RGPD

| **Base légale** | **Exemple** |
|---|---|
| **Consentement** | Newsletter, cookies non essentiels |
| **Contrat** | Données nécessaires à l'exécution d'un contrat |
| **Obligation légale** | Conservation des bulletins de paie |
| **Intérêts vitaux** | Données médicales en urgence vitale |
| **Mission d'intérêt public** | Données traitées par une autorité publique |
| **Intérêts légitimes** | Vidéosurveillance pour la sécurité des locaux |

### Les 5 Ports Dangereux à Connaître Absolument

| **Port** | **Service** | **Risque principal** |
|---|---|---|
| **21** | FTP | Transfert en clair + backdoors connues |
| **23** | Telnet | Authentification en clair — remplacé par SSH |
| **445** | SMB | EternalBlue, WannaCry, propagation ransomware |
| **3306** | MySQL | Accès direct à la base de données |
| **3389** | RDP | Force brute, BlueKeep, session hijacking |

### Règle 3-2-1 des Sauvegardes

```
  3  copies des données
  2  supports différents (ex : disque externe + cloud)
  1  copie hors site (déconnectée du réseau principal)
```

### Obligations RGPD en cas de Violation

```
  72 heures → Notification à la CNIL (art. 33 RGPD)
  Sans délai → Information des personnes si risque élevé (art. 34 RGPD)
  Sanction max → 20 M€ ou 4% du CA mondial (le plus élevé)
```

---

## Pièges à Éviter

| **Piège fréquent** | **Conseil** |
|---|---|
| Répondre à côté de la question | Relisez la question avant de rédiger, pas après |
| Réponses trop courtes sur les questions à 6+ points | Développez : définition + exemple + application au contexte |
| Oublier le contexte CLINOVA SANTÉ | Chaque réponse doit mentionner l'entreprise du sujet |
| Confondre Responsable de traitement et Sous-traitant | RT = décide quoi faire des données / ST = les traite pour le compte du RT |
| Dire "il faut un antivirus" sans préciser le contexte | Précisez : type de serveur, fréquence de mise à jour, intégration au SI |
| Rédiger la note C1 en langage trop technique | Le destinataire est un Directeur Général non-technicien |

---

## Rappel des Compétences Évaluées

| **Code** | **Ce que le correcteur cherche à voir** |
|---|---|
| **B3.1** | Identification précise des menaces (ransomware, phishing, force brute, exploit CVE…) |
| **B3.2** | Mesures concrètes : mots de passe, MFA, mises à jour, sauvegardes, pare-feu, VPN, chiffrement |
| **B3.3** | Maîtrise du RGPD : bases légales, droits, DPO, notification violation, sanctions |
| **B3.4** | Lecture d'un rapport Nmap, score CVSS, priorisation des actions, rédaction d'un plan correctif |

---

*Fiche de Préparation Élève E6 — S20 BLOC 3 — BTS SIO SISR — Année 1 — Version 1.0*
