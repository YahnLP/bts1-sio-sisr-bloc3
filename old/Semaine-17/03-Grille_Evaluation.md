---
author: YLP
title: 📖 Grille d'Évaluation
---

# Grille d'Évaluation
## Projet Sécurisation Infrastructure

*Barème Qualiopi — 40 points*

---

## 📊 BARÈME DÉTAILLÉ

### LIVRABLE 1 : Schéma Réseau (8 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **Zones réseau** | /3 | - LAN clairement identifiée (1 pt)<br>- DMZ clairement identifiée (0,5 pt)<br>- Internet représenté (0,5 pt)<br>- Pare-feu externe et interne présents (1 pt) |
| **Placement serveurs** | /2 | - SRV-WEB en DMZ (1 pt)<br>- Autres serveurs en LAN (0,5 pt)<br>- Justification des choix (0,5 pt) |
| **Adressage IP** | /1 | - Plan d'adressage cohérent (LAN, DMZ différentes) |
| **Règles pare-feu** | /1 | - Tableau règles présent avec min 5 règles pertinentes |
| **Qualité schéma** | /1 | - Lisible, propre, légende présente (0,5 pt)<br>- Flux réseau indiqués (flèches) (0,5 pt) |

---

### LIVRABLE 2 : GPO (8 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **GPO Mot de passe** | /2 | - Paramètres conformes bonnes pratiques (longueur 12+, complexité) (1 pt)<br>- Capture écran configuration (0,5 pt)<br>- Justification (0,5 pt) |
| **GPO Verrouillage** | /1,5 | - Paramètres cohérents (seuil 5, durée 30 min) (1 pt)<br>- Capture + justification (0,5 pt) |
| **GPO Pare-feu** | /1,5 | - Activation 3 profils (1 pt)<br>- Capture + justification (0,5 pt) |
| **2 GPO supplémentaires** | /2 | - Pertinence des GPO choisies (1 pt)<br>- Configuration détaillée (0,5 pt)<br>- Justifications (0,5 pt) |
| **Documentation** | /1 | - Clarté rédactionnelle (0,5 pt)<br>- Mise en forme professionnelle (0,5 pt) |

---

### LIVRABLE 3 : Droits NTFS (6 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **Structure dossiers** | /2 | - Minimum 6 dossiers partagés (1 pt)<br>- Nomenclature claire (0,5 pt)<br>- Hiérarchie logique (0,5 pt) |
| **Matrice permissions** | /2 | - Tableau complet (tous services) (1 pt)<br>- Permissions cohérentes (0,5 pt)<br>- Aucune incohérence (0,5 pt) |
| **Principe moindre privilège** | /1,5 | - Appliqué correctement (1 pt)<br>- Pas d'excès de permissions (0,5 pt) |
| **Justifications** | /0,5 | - Choix expliqués et pertinents |

---

### LIVRABLE 4 : Sauvegardes (6 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **Règle 3-2-1** | /2 | - 3 copies identifiées (0,5 pt)<br>- 2 supports différents (0,5 pt)<br>- 1 copie hors site (1 pt) |
| **Tableau sauvegarde** | /2 | - Quoi, Quand, Où, Comment, Rétention (tous renseignés) |
| **Types sauvegardes** | /1 | - Complète + Différentielle/Incrémentielle (stratégie cohérente) |
| **Test restauration** | /0,5 | - Procédure mensuelle décrite |
| **Chiffrement** | /0,5 | - Mention chiffrement AES-256 (protection RGPD + ransomware) |

---

### LIVRABLE 5 : HTTPS (4 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **Choix certificat** | /1 | - Let's Encrypt / Payant / Auto-signé avec justification pertinente |
| **Procédure installation** | /1,5 | - Commandes détaillées (1 pt)<br>- Configuration Apache .conf (0,5 pt) |
| **Redirection HTTP→HTTPS** | /0,5 | - Présente et fonctionnelle |
| **Test validation** | /0,5 | - Capture écran cadenas HTTPS |
| **Qualité doc** | /0,5 | - Clarté, reproductibilité |

---

### LIVRABLE 6 : Soutenance Orale (8 points)

| **Critère** | **Points** | **Détail** |
|-------------|------------|------------|
| **Structure présentation** | /2 | - Introduction claire (0,5 pt)<br>- Plan logique (0,5 pt)<br>- Conclusion (0,5 pt)<br>- Respect timing 5 min (0,5 pt) |
| **Contenu technique** | /3 | - Schéma réseau présenté et expliqué (1 pt)<br>- GPO et NTFS expliqués (1 pt)<br>- Sauvegardes + HTTPS expliqués (1 pt) |
| **Maîtrise sujet** | /2 | - Réponses aux questions jury pertinentes (1 pt)<br>- Vocabulaire technique maîtrisé (0,5 pt)<br>- Pas de lecture slides (0,5 pt) |
| **Support visuel** | /1 | - PowerPoint clair ou docs bien présentés |

---

## ✅ VALIDATION (Qualiopi)

**Pour valider le projet (≥ 20/40)** :
- ✅ Tous les livrables rendus (même partiels)
- ✅ Schéma réseau avec DMZ séparée
- ✅ Au moins 3 GPO configurées
- ✅ Matrice NTFS avec minimum 4 dossiers
- ✅ Plan sauvegarde avec règle 3-2-1
- ✅ Soutenance effectuée (même imparfaite)

**Pour excellence (≥ 32/40)** :
- ✅ 5 GPO pertinentes avec justifications solides
- ✅ Matrice NTFS complète 6+ dossiers
- ✅ Plan sauvegarde détaillé avec tests
- ✅ HTTPS Let's Encrypt configuré (pas auto-signé)
- ✅ Soutenance fluide, questions maîtrisées
- ✅ Documentation professionnelle (orthographe, mise en forme)

---

## 📝 FEUILLE NOTATION (Par Groupe)

**Groupe** : _______________ **Membres** : _______________

| Livrable | Note / Max | Commentaires |
|----------|------------|--------------|
| Schéma réseau | ___ / 8 | |
| GPO | ___ / 8 | |
| NTFS | ___ / 6 | |
| Sauvegardes | ___ / 6 | |
| HTTPS | ___ / 4 | |
| Soutenance | ___ / 8 | |
| **TOTAL** | **___ / 40** | |

**Appréciation globale** :
___________________________________________________________
___________________________________________________________

**Signature enseignant** : _______________

---

*Grille Évaluation S17 BLOC 3 — BTS SIO SISR*
