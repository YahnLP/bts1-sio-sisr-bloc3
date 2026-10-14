---
author: YLP
title: 🎯 MÉTHODOLOGIE ÉPREUVE E6
---

# 🎯 MÉTHODOLOGIE ÉPREUVE E6

## I. Format de l'Épreuve

**Durée** : 4 heures
**Support** : Étude de cas papier (10-15 pages)
**Documents** : AUCUN autorisé
**Questions** : 4-6 questions ouvertes progressives

---

## II. Gestion du Temps (4h)

| Phase | Durée | Activité |
|-------|-------|----------|
| **Lecture** | 30 min | Lire TOUT le sujet, surligner infos clés |
| **Planification** | 10 min | Répartir temps par question |
| **Rédaction** | 150 min | Répondre aux questions (30-40 min chacune) |
| **Relecture** | 30 min | Corriger orthographe, vérifier numérotation |

**Règle d'or** : Ne PAS bloquer sur une question. Si bloqué >20 min → Passer à la suivante.

---

## III. Lecture Active (30 min)

### Étape 1 : Contexte Entreprise (10 min)

**Surligner** :
- Secteur, effectif, sites
- Infrastructure (serveurs, réseau, postes)
- Budget disponible

**Pourquoi** : Toutes vos réponses doivent être adaptées à CE contexte précis.

### Étape 2 : Situation Problématique (10 min)

**Identifier** :
- Quel est le problème ? (audit négatif, incident, projet)
- Quelles sont les failles/manquements ?
- Quelles sont les contraintes ? (budget, délai, compétences)

### Étape 3 : Questions (10 min)

**Anticiper** :
- Question 1 → Souvent analyse (lister, identifier)
- Question 2 → Souvent conformité (RGPD, lois)
- Question 3 → Souvent propositions techniques (2-3 solutions)
- Question 4 → Souvent justification/choix (argumenter)

---

## IV. Structure Réponse Type

### Questions ANALYSE (ex: Q1)

**Structure** :
```
Introduction (2 lignes) : "L'infrastructure de [entreprise] présente 
plusieurs vulnérabilités critiques identifiées lors de l'audit."

1. [Vulnérabilité 1]
   - Description : ...
   - Risque : ...
   - Impact : ...

2. [Vulnérabilité 2]
   ...

Conclusion (2 lignes) : "Ces 5 vulnérabilités nécessitent des actions 
correctives urgentes pour sécuriser l'infrastructure."
```

**Longueur** : 1 page minimum

---

### Questions PROPOSITIONS (ex: Q3)

**Structure** :
```
Introduction : "Pour sécuriser [aspect], je propose les mesures suivantes :"

Mesure 1 : [Titre clair]
- Description technique : ...
- Mise en œuvre : ... (comment, où, avec quoi)
- Bénéfice sécurité : ...
- Coût estimé : ... (si pertinent)

Mesure 2 : ...

Conclusion : "Ces mesures couvrent les risques identifiés tout en 
respectant les contraintes budgétaires."
```

**Longueur** : 1-2 pages

---

### Questions JUSTIFICATION (ex: Q4)

**Structure** :
```
Introduction : "Plusieurs options sont envisageables. Voici une analyse 
comparative :"

Tableau comparatif :
| Critère | Option A | Option B |
|---------|----------|----------|
| Coût | ... | ... |
| Complexité | ... | ... |
| ...

Recommandation : "Je recommande l'option [X] pour les raisons suivantes :"
1. Argument 1 (risque)
2. Argument 2 (coût)
3. Argument 3 (faisabilité)
```

---

## V. Conseils Rédactionnels

### ✅ À FAIRE

**Reformuler avec contexte** :
❌ "Il faut des sauvegardes"
✅ "TechServices doit mettre en place des sauvegardes automatisées de ses 4 serveurs (AD, Fichiers, Web, CRM)"

**Justifier TOUJOURS** :
❌ "Je propose un firewall"
✅ "Je propose un firewall FortiGate car il permet de segmenter le réseau en DMZ et protège contre les attaques depuis Internet, répondant ainsi au risque identifié en Q1"

**Utiliser vocabulaire technique précis** :
✅ GPO, NTFS, DMZ, RGPD Art. 30, 3-2-1, ISO 27001

**Numéroter clairement** :
```
QUESTION 1

1. Vulnérabilité 1 : ...
2. Vulnérabilité 2 : ...
```

---

### ❌ À ÉVITER

**Réponses trop courtes** :
❌ "Les mots de passe sont faibles" (1 ligne)
✅ Développer : description + risque + solution (5-10 lignes)

**Hors sujet** :
❌ Parler de cloud si le sujet mentionne infrastructure on-premise uniquement

**Copier-coller cours** :
❌ "La sauvegarde est importante car..."
✅ Adapter au contexte : "TechServices ayant subi un ransomware en février 2026 détruisant 6 semaines de compta, une stratégie de sauvegarde 3-2-1 est critique."

**Pas de justification** :
❌ "Je choisis pfSense"
✅ "Je choisis pfSense car : 1) gratuit (économie 5k€), 2) DSI compétent Linux, 3) fonctionnalités suffisantes"

---

## VI. Checklist Avant Rendu

**10 min avant la fin** :

☐ Toutes les questions sont numérotées
☐ Nom sur chaque feuille
☐ Orthographe relue (surtout termes techniques)
☐ Schémas clairs et légendés si demandés
☐ Aucune abréviation non expliquée
☐ Toutes les questions traitées (même partiellement)

---

## VII. Erreurs Fréquentes

| Erreur | Conséquence | Solution |
|--------|-------------|----------|
| Passer 1h sur Q1 | Pas le temps pour Q3-Q4 | Timer 30-40 min/question |
| Rédiger sans plan | Réponse désordonnée | 5 min plan avant rédiger |
| Oublier de justifier | -50% de la note | TOUJOURS dire POURQUOI |
| Vocabulaire imprécis | Perte crédibilité | Réviser termes techniques |
| Pas de contexte | Réponse générique | Toujours citer l'entreprise du cas |

---

## VIII. Barème Typique E6

- **40%** : Analyse (identifier, lister, expliquer)
- **35%** : Propositions techniques (solutions concrètes)
- **20%** : Justifications (argumenter, comparer)
- **5%** : Qualité rédactionnelle (orthographe, clarté)

---

*Méthodologie S18 BLOC 3 — BTS SIO SISR*
