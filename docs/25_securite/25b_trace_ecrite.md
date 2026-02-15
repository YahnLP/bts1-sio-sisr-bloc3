---
author: ELP
title: 25 📖 Trace écrite
---

# S25 – Choisir et sécuriser un appareil

---

## 1️⃣ Les grandeurs électriques

### Les 4 grandeurs fondamentales

| Grandeur | Symbole | Unité | Analogie |
|----------|:-------:|:-----:|----------|
| **Tension** | U | volt (V) | Pression de l'eau |
| **Intensité** | I | ampère (A) | Débit de l'eau |
| **Puissance** | P | watt (W) | Force du jet |
| **Énergie** | E | joule (J) ou kilowattheure (kWh) | Quantité totale d'eau utilisée |

### Relations fondamentales

```
┌─────────────────────────────────────────────────┐
│                                                 │
│   P = U × I                                     │
│                                                 │
│   P (W) = U (V) × I (A)                         │
│   I = P / U          U = P / I                  │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│   E = P × t                                     │
│                                                 │
│   E (kWh) = P (kW) × t (h)                      │
│   ou  E (J) = P (W) × t (s)                     │
│                                                 │
└─────────────────────────────────────────────────┘
```

### Valeurs de référence en France

| Donnée | Valeur |
|--------|:------:|
| Tension du réseau | **230 V** |
| Fréquence du réseau | **50 Hz** |
| Intensité max par prise standard | **16 A** |
| Puissance max par prise 16 A | 230 × 16 = **3 680 W** |

---

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   📌 À RETENIR – GRANDEURS ÉLECTRIQUES :                        │
│                                                                 │
│   • P = U × I  →  permet de vérifier si la prise supporte       │
│     l'appareil (I = P / U < calibre du disjoncteur ?)           │
│   • E = P × t  →  permet de calculer la consommation            │
│     (en kWh = ce qu'on paye sur la facture)                     │
│   • En France : 230 V, 50 Hz, prise 16 A max                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2️⃣ La plaque signalétique

Chaque appareil porte une **plaque signalétique** avec les informations obligatoires :

| Information | Ce qu'elle indique | Exemple |
|-------------|-------------------|---------|
| **Tension (V)** | Tension d'alimentation requise | 220-240 V ~ |
| **Fréquence (Hz)** | Fréquence du réseau | 50/60 Hz |
| **Puissance (W)** | Consommation de l'appareil | 800 W |
| **Classe** | Type de protection électrique | I, II ou III |
| **Marquage CE** | Conformité aux normes européennes | CE |
| **IP xx** | Protection contre solides (1er chiffre) et eau (2e) | IP21 |
| **DEEE** (🗑️ barré) | Ne pas jeter en ordures ménagères | Collecte séparée |

**Savoir lire une plaque signalétique permet de :**
- Vérifier la compatibilité avec l'installation (230 V en France)
- Calculer l'intensité tirée (I = P / U)
- Identifier la classe de protection
- Vérifier la conformité (CE)

---

## 3️⃣ Danger et risque

### Définitions

| Concept | Définition | Caractéristique |
|---------|------------|-----------------|
| **Danger** | Propriété intrinsèque de provoquer un dommage | Permanent, ne disparaît pas |
| **Risque** | Probabilité qu'un dommage survienne | Variable, dépend des conditions |

Le courant électrique 230 V est **toujours** un danger. Le risque d'accident varie selon les conditions : état de l'appareil, environnement, protections en place.

### Les 4 risques électriques

| Risque | Description | Gravité |
|--------|-------------|:-------:|
| **Électrisation** | Passage du courant dans le corps | Variable |
| **Électrocution** | Électrisation mortelle | ☠️ |
| **Brûlure** | Échauffement ou arc électrique | Grave |
| **Incendie** | Embrasement par surcharge ou court-circuit | Grave |

---

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   📌 À RETENIR – DANGER vs RISQUE :                             │
│                                                                 │
│   • Le DANGER est intrinsèque → on ne le supprime pas           │
│   • Le RISQUE dépend des conditions → on le RÉDUIT              │
│   • En institut : eau + électricité = risque ÉLEVÉ              │
│   • Réduire le risque = protections + bonnes pratiques          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4️⃣ Dispositifs de sécurité électrique

### Protection des personnes

| Dispositif | Rôle | Protection contre |
|------------|------|-------------------|
| **Prise de terre** (fil vert/jaune) | Évacue le courant de fuite vers le sol | Électrisation / électrocution |
| **Disjoncteur différentiel** (30 mA) | Coupe le courant si fuite détectée (en 30 ms) | Électrisation / électrocution |
| **Fusible** | Fond si I trop forte → coupe le circuit | Surcharge / court-circuit / incendie |

### Classes de protection des appareils

| Classe | Protection | Prise de terre ? | Symbole | Exemple |
|:------:|-----------|:-----------------:|:-------:|---------|
| **I** | Mise à la terre | ✅ Oui (3 broches) | — | Vapozone, étuve, spectrophotomètre |
| **II** | Double isolation | ❌ Non | ☐☐ | Sèche-cheveux, lisseur, fer à boucler |
| **III** | Très basse tension (< 50 V) | ❌ Non | — | Chargeur, lampe LED 12 V |

**Remarque importante :** Classe I et Classe II offrent un niveau de sécurité **équivalent** par des moyens différents. Classe I nécessite une prise avec terre ; Classe II s'en passe grâce à la double couche d'isolation.

### Marquages obligatoires

| Marquage | Signification |
|:--------:|---------------|
| **CE** | Conformité aux exigences essentielles européennes (obligatoire) |
| **NF** | Conformité aux normes françaises (volontaire, gage de qualité supplémentaire) |
| **🗑️ barré** | DEEE : collecte séparée obligatoire |
| **IP xx** | Indice de protection (ex : IP21 = protégé contre les gouttes d'eau) |

---

## 5️⃣ Choix raisonné d'un appareil

### Les 4 critères de choix

| Critère | Questions à se poser |
|---------|---------------------|
| **Technique** | Puissance adaptée ? Tension compatible (230 V) ? Fonctionnalités suffisantes ? |
| **Sécuritaire** | Marquage CE ? Classe de protection adaptée ? Norme NF (bonus) ? |
| **Économique** | Consommation (kWh) ? Durabilité ? Garantie ? Rapport qualité/prix ? |
| **Éco-responsable** | Indice de réparabilité ? Durée de vie ? Gestion de fin de vie (DEEE) ? |

### Méthode de choix

1. **Définir le besoin** (usage, fréquence, environnement)
2. **Comparer** les modèles sur les 4 critères
3. **Croiser** les critères (pas uniquement le prix !)
4. **Justifier** le choix avec au moins 3 arguments

---

## 6️⃣ Gestion des déchets et éco-responsabilité

### Filières de tri en institut et en labo

| Type de déchet | Filière | Ce qu'il faut faire |
|----------------|---------|---------------------|
| **DEEE** (appareils en fin de vie) | Collecte séparée | Point de collecte ou reprise distributeur (1 pour 1) |
| **Lampes UV / fluorescentes** | Collecte spéciale | Déchèterie (contiennent du mercure) |
| **Déchets chimiques** (solutions labo) | Bidons étiquetés | **Jamais dans l'évier !** Collecte spécialisée |
| **Emballages** (plastique, verre, carton) | Tri sélectif | Bacs de tri selon le matériau |
| **Consommables souillés** (cotons, lingettes) | Ordures ménagères | Poubelle classique |

### Éco-gestes au quotidien

- **Éteindre** les appareils en veille (consommation inutile)
- **Choisir** des appareils avec un bon indice de **réparabilité** (≥ 6/10)
- **Entretenir** régulièrement (allonge la durée de vie)
- **Recycler** via les filières appropriées (DEEE, tri sélectif)

---

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   📌 À RETENIR – DÉCHETS :                                     │
│                                                                 │
│   • DEEE (🗑️ barré) → collecte séparée OBLIGATOIRE             │
│   • Lampes UV → collecte spéciale (mercure)                     │
│   • Déchets chimiques → bidons étiquetés, JAMAIS l'évier        │
│   • Éco-responsabilité = durabilité + réparabilité + tri        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📌 À retenir pour l'E2

### Définitions essentielles

| Terme | Définition |
|-------|------------|
| **Tension U** | Grandeur (en V) qui « pousse » le courant |
| **Intensité I** | Grandeur (en A) mesurant le « débit » de courant |
| **Puissance P** | Énergie consommée par seconde (en W) : P = U × I |
| **Énergie E** | Quantité totale d'énergie consommée (en kWh) : E = P × t |
| **Danger** | Propriété intrinsèque de provoquer un dommage |
| **Risque** | Probabilité qu'un dommage survienne |
| **Classe I** | Appareil avec mise à la terre (prise 3 broches) |
| **Classe II** | Appareil avec double isolation (symbole ☐☐) |
| **DEEE** | Déchets d'Équipements Électriques et Électroniques |

### Formules à maîtriser

| Formule | Usage |
|---------|-------|
| P = U × I | Calculer la puissance, vérifier le calibre du disjoncteur |
| I = P / U | Calculer l'intensité tirée par un appareil |
| E = P × t | Calculer la consommation d'énergie |

### Vocabulaire à maîtriser

- **Tension, intensité, puissance, énergie** – **Volt, ampère, watt, kWh**
- **Danger, risque** – **Électrisation, électrocution**
- **Prise de terre, disjoncteur différentiel, fusible**
- **Classe I, Classe II, Classe III** – **Marquage CE, NF**
- **DEEE** – **Éco-responsabilité, indice de réparabilité**
- **Plaque signalétique** – **Calibre**

---

## 🔗 Lien avec la suite de la progression

| Séance | Réinvestissement |
|--------|------------------|
| **S23** | Appareils US → ici : sécurité électrique de ces appareils |
| **S24** | Spectrophotomètre UV-vis → ici : sécurité labo, déchets chimiques |
| **S26** | TP spectrophotométrie → appliquer les règles de sécurité en labo |
| **COSMÉTO S05** | Sécurité au poste de travail → sécurité électrique |
| **COSMÉTO S22 / S29** | Dossier professionnel → choix raisonné, éco-responsabilité |

---

## 🔧 Fiches méthode associées

➡️ [**Fiche méthode 02 – Calculer et interpréter (D.U.C.I.)**](../Methodologie/02_fiche_methode/)

➡️ [**Fiche méthode 01 – Justifier une réponse scientifique (O.A.C.J.)**](../Methodologie/01_fiche_methode/)
