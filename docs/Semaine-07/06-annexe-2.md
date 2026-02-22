---
author: YLP
title: 📄 ANNEXE 2
---

# 📄 ANNEXE 2 — ARBRE DE DÉCISION NOTIFICATION CNIL

```
═══════════════════════════════════════════════════════════════
         ARBRE DE DÉCISION — VIOLATION DE DONNÉES
═══════════════════════════════════════════════════════════════

             Incident de sécurité détecté
                          │
                          ▼
         Des données PERSONNELLES sont-elles concernées ?
         ┌─── NON → Documenter en interne, pas de notification
         │
         └─── OUI ↓

                    Quel est le risque ?
        ┌───────────────────────────────────────────┐
        ▼                                           ▼
   RISQUE FAIBLE                            RISQUE ÉLEVÉ
   • Données non sensibles              • Données sensibles (santé...)
   • Peu de personnes                   • Nombreuses personnes
   • Données chiffrées                  • Données en clair
   • Impact limité/réversible           • Impact grave/irréversible
        │                                           │
        ▼                                           ▼
   Documenter                         NOTIFIER LA CNIL
   en interne                         ≤ 72 heures
   uniquement                                       │
                                                    ▼
                                    Risque TRÈS ÉLEVÉ pour les personnes ?
                                    • Usurpation identité probable
                                    • Préjudice financier imminent
                                    • Données médicales exposées
                                         │            │
                                        OUI           NON
                                         │            │
                                         ▼            ▼
                                   NOTIFIER      Pas de notif.
                                   LES          aux personnes
                                   PERSONNES
                                   (sans délai)

═══════════════════════════════════════════════════════════════
DANS TOUS LES CAS : Documenter dans le registre interne des violations
═══════════════════════════════════════════════════════════════
```

---
