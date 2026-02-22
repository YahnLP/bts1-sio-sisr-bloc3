---
author: YLP
title: 📄 ANNEXE 2
---

# 📄 ANNEXE 2 — CALCULATEUR RPO/RTO

```
═══════════════════════════════════════════════════════════════
               CALCULATEUR RPO / RTO
═══════════════════════════════════════════════════════════════

SCÉNARIO : ___________________________________________________

1. ANALYSE RPO
──────────────────────────────────────────────────────────────
Combien de temps de données pouvez-vous perdre ?

☐ 0 (aucune perte)        → Réplication temps réel
☐ 15 minutes              → Sauvegarde continue (15 min)
☐ 1 heure                 → Sauvegarde horaire
☐ 4 heures                → Sauvegarde toutes les 4h
☐ 24 heures               → Sauvegarde quotidienne

FRÉQUENCE DE SAUVEGARDE = RPO

2. ANALYSE RTO
──────────────────────────────────────────────────────────────
Combien de temps max pour restaurer ?

☐ 1 heure                 → Besoin infrastructure haute dispo
☐ 4 heures                → Restauration rapide requise
☐ 24 heures               → Restauration standard acceptable
☐ 1 semaine               → Peut attendre

VITESSE RESTAURATION = RTO

3. CALCUL BESOIN STOCKAGE
──────────────────────────────────────────────────────────────
Données totales : ________ Go
Croissance quotidienne : ________ Go
Rétention : ________ jours

Type sauvegarde : ☐ Complète  ☐ Différentielle  ☐ Incrémentielle

ESPACE REQUIS = _________________________________________

═══════════════════════════════════════════════════════════════
```

