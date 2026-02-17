---
author: ELP
title: 24 📖 Trace écrite
---

# S24 – Lampe UV / UV-Visible : spectres et absorbance 📖

---

## 1️⃣ Rappel : ondes électromagnétiques vs mécaniques

| Critère | Onde mécanique (S23) | Onde EM (S24) |
|---------|:--------------------:|:-------------:|
| **Exemple** | Ultrasons | Lumière, UV, IR |
| **Milieu nécessaire ?** | ✅ Oui (air, eau, peau) | ❌ Non (se propage dans le vide) |
| **Célérité dans le vide** | Impossible | c = 3 × 10⁸ m/s |
| **Gel de contact ?** | Obligatoire | Non nécessaire |
| **Relation** | c = λ × f (identique) | c = λ × f (identique) |

---

## 2️⃣ Le spectre électromagnétique

### Vue d'ensemble

```
  Rayons γ   Rayons X     UV      VISIBLE      IR      Micro-ondes   Radio
  ◄──────────────────────────────────────────────────────────────────────►
  λ petit                                                      λ grand
  E élevée                                                     E faible
                         │         │           │
                      10 nm    400 nm       800 nm
```

### Zoom sur UV et visible

| Domaine | Bornes de λ | Caractéristiques | Usage cosmétique |
|---------|:-----------:|------------------|------------------|
| **UVC** | 100 – 280 nm | Très dangereux, arrêtés par l'ozone | Stérilisation (lampes germicides) |
| **UVB** | 280 – 320 nm | Coups de soleil (érythème) | Protection SPF |
| **UVA** | 320 – 400 nm | Vieillissement cutané, bronzage | Protection PA / UVA |
| **Visible** | 400 – 800 nm | Lumière perçue par l'œil | LED bleue (anti-acné), rouge (anti-âge) |
| **IR** | 800 nm – 1 mm | Chaleur | Lampes IR institut |

---

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   📌 À RETENIR – SPECTRE EM :                                 │
│                                                                 │
│   • UV : 10-400 nm (invisible, dangereux pour la peau)         │
│   • Visible : 400-800 nm (couleurs perçues par l'œil)         │
│   • IR : > 800 nm (chaleur)                                    │
│   • UVA (320-400) = vieillissement ; UVB (280-320) = brûlure  │
│   • Filtres solaires = molécules qui ABSORBENT les UV          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3️⃣ Le spectrophotomètre UV-visible

### Principe

Un spectrophotomètre mesure la quantité de lumière **absorbée** par un échantillon en solution.

```
┌──────────┐   ┌───────────────┐   ┌──────────┐   ┌──────────────┐   ┌───────────┐
│  LAMPE   │ → │ MONOCHROMATEUR │ → │   CUVE   │ → │  DÉTECTEUR   │ → │ AFFICHAGE │
│ (UV/vis) │   │ (sélection λ) │   │ (l = 1cm)│   │ (mesure I)   │   │   A, T    │
└──────────┘   └───────────────┘   └──────────┘   └──────────────┘   └───────────┘
```

### Grandeurs mesurées

| Grandeur | Symbole | Définition | Unité |
|----------|:-------:|------------|:-----:|
| **Transmittance** | T | Fraction de lumière transmise : T = I/I₀ | Sans unité |
| **Absorbance** | A | Mesure de la lumière absorbée : A = −$log_{10}$(T) = $log_{10}$(I₀/I) | Sans unité |

> ⚠️ Si **T** est exprimée en **%**, convertir : **T = T(%) / 100** avant d'utiliser **$log_{10}$**.

**Signification :**
- Si l'échantillon absorbe beaucoup → A grand (solution foncée, concentrée)
- Si l'échantillon n'absorbe pas → A ≈ 0 (solution transparente, diluée)

---

## 4️⃣ Spectres d'absorption

### Définition

Un **spectre d'absorption** est le graphe de l'absorbance A en fonction de la longueur d'onde λ : A = f(λ).

### Ce qu'on cherche sur un spectre

| Élément | Comment le trouver | Signification |
|---------|-------------------|---------------|
| **$λ_{max}$** | Sommet du pic (maximum d'absorption) | Longueur d'onde où la mesure est la plus sensible |
| **Domaine** | UV (< 400 nm) ou visible (> 400 nm) | Détermine l'usage (filtre UV ou colorant) |

### Lien spectre – couleur

Si une molécule absorbe dans le **visible**, elle apparaît de la **couleur complémentaire** :

| Couleur absorbée | λ absorbée | Couleur observée |
|:----------------:|:----------:|:----------------:|
| Violet | 400-450 nm | Jaune-vert |
| Bleu | 450-495 nm | Orange |
| Vert | 495-570 nm | Rouge-violet |
| Rouge | 620-800 nm | Bleu-vert |

**Exemple :** Le β-carotène absorbe le bleu-violet (≈ 450 nm) → il apparaît **orange**.

---

## 5️⃣ Loi de Beer-Lambert

### Énoncé

L'absorbance A d'une solution est **proportionnelle** à la concentration C de l'espèce absorbante.

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│               A = ε × l × C                                  │
│                                                              │
│   A : absorbance (sans unité)                                │
│   ε : coefficient d'absorption molaire (L·mol⁻¹·cm⁻¹)        │
│   l : longueur de la cuve (cm) – en général l = 1 cm         │
│   C : concentration molaire (mol·L⁻¹)                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Relations dérivées

| On cherche | Formule |
|:----------:|---------|
| **A** | A = ε × l × C |
| **C** | C = A / (ε × l) |
| **ε** | ε = A / (l × C) |

### Signification physique

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│   ⚠️  Si la CONCENTRATION DOUBLE → l'ABSORBANCE DOUBLE      │
│                                                              │
│   Analogie du thé :                                          │
│   1 sachet → couleur claire (A faible)                       │
│   2 sachets → couleur 2× plus foncée (A double)              │
│   3 sachets → couleur 3× plus foncée (A triple)              │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Conditions de validité

La loi de Beer-Lambert est valable si :
- La solution est **diluée** (A < 2)
- La lumière est **monochromatique** (une seule λ, de préférence $λ_{max}$)
- La solution est **homogène**

---

## 6️⃣ Dosage par courbe d'étalonnage

### Méthode en 5 étapes

1. Préparer des **solutions étalons** de concentration connue
2. Mesurer l'**absorbance** de chaque étalon à $λ_{max}$
3. Tracer la courbe **A = f(C)** → droite passant par l'origine
4. Mesurer l'absorbance de l'**échantillon inconnu** (A_éch)
5. **Lecture graphique** : trait horizontal → droite → trait vertical → $C_{éch}$

### Lecture graphique

<p style="text-align:center;">
  <img src="/24_absorbance/images/courbe_etalonnage.png" alt="Corbe d'étalonnage" style="width:85%;">
  <br>
  <em>Courbe d'étalonnage</em>
</p>



### Conclusion de conformité

| Étape | Action |
|-------|--------|
| 1 | Déterminer $C_{éch}$ par lecture graphique |
| 2 | Rappeler l'intervalle du cahier des charges [$C_{min}$ ; $C_{max}$] |
| 3 | Comparer : $C_{min}$ ≤ $C_{éch}$ ≤ $C_{max}$ ? |
| 4 | Conclure : **conforme** (dans l'intervalle) ou **non conforme** |

---

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   📌 À RETENIR – DOSAGE SPECTROPHOTOMÉTRIQUE :                 │
│                                                                 │
│   • Mesurer TOUJOURS à $λ_{max}$ (sensibilité maximale)         │
│   • Loi de Beer-Lambert : A = ε × l × C                         │
│   • Courbe d'étalonnage : droite A = f(C) par l'origine         │
│   • Lecture graphique : horizontal → droite → vertical          │
│   • Conformité : $C_{éch}$ ∈ [$C_{min}$ ; $C_{max}$] du CDC     |          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 7️⃣ Pourquoi mesurer à $λ_{max}$ ?

À $λ_{max}$, l'absorbance est **maximale** → meilleure **sensibilité** :

- Petite variation de C → variation mesurable de A → dosage **précis**
- À une autre λ, A serait plus faible → difficile de distinguer deux concentrations proches → dosage **imprécis**

---

## 📌 À retenir pour l'E2

### Définitions essentielles

| Terme | Définition |
|-------|------------|
| **Onde EM** | Perturbation qui se propage sans milieu matériel |
| **Absorbance A** | Grandeur sans unité mesurant la lumière absorbée |
| **$λ_{max}$** | Longueur d'onde du maximum d'absorption |
| **Loi de Beer-Lambert** | A = ε × l × C (proportionnalité A ↔ C) |
| **Courbe d'étalonnage** | Droite A = f(C) permettant de doser un inconnu |
| **Filtre UV** | Molécule qui absorbe les UV ($λ_{max}$ dans le domaine UV) |
| **Spectrophotomètre** | Appareil mesurant l'absorbance d'un échantillon |

### Règles pratiques

| Règle | Application |
|-------|-------------|
| A ↑ quand C ↑ | Proportionnalité Beer-Lambert |
| $λ_{max}$ = sommet du pic | Lecture de spectre |
| Mesure à $λ_{max}$ | Meilleure sensibilité pour le dosage |
| Droite par l'origine | Vérification de la loi de Beer-Lambert |
| $C_{éch}$ ∈ [$C_{min}$ ; $C_{max}$] → conforme | Conclusion de contrôle qualité |

### Vocabulaire à maîtriser

- **Spectre électromagnétique** – **UV, UVA, UVB, UVC** – **Visible, IR**
- **Absorbance, transmittance** – **$λ_{max}$**
- **Spectrophotomètre** – **Monochromateur, cuve, détecteur**
- **Loi de Beer-Lambert** – **ε, l, C**
- **Courbe d'étalonnage** – **Lecture graphique**
- **Conforme, non conforme** – **Cahier des charges**

---

## 🔗 Lien avec la suite de la progression

| Séance | Réinvestissement |
|--------|------------------|
| **S03** | Concentration massique → ici : dosage par spectrophotométrie |
| **S05** | Échelle de teinte → ici : courbe d'étalonnage (même logique, plus précis) |
| **S23** | Ondes mécaniques (US) → ici : ondes EM (c = λ × f identique) |
| **COSMÉTO S24** | Preuves d'efficacité → documents instrumentaux (spectres) |
| **COSMÉTO S25** | Analyse résultats expérimentaux → dosage spectrophotométrique |

---

## 🔧 Fiches méthode associées

➡️ [**Fiche méthode 02 – Calculer et interpréter (D.U.C.I.)**](../Methodologie/02_fiche_methode/)

➡️ [**Fiche méthode 01 – Justifier une réponse scientifique (O.A.C.J.)**](../Methodologie/01_fiche_methode/)
