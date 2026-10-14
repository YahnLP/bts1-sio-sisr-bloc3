---
author: YLP
title: 📄 ANNEXE 3
---

# 📄 ANNEXE 3 — CAS D'ERREURS CATASTROPHIQUES

```
═══════════════════════════════════════════════════════════════
         CAS RÉELS D'ERREURS DE SAUVEGARDE
═══════════════════════════════════════════════════════════════

CAS 1 : GITLAB.COM (2017)
──────────────────────────────────────────────────────────────
ERREUR : Admin supprime accidentellement 300 Go de données
         de production

TENTATIVE RESTAURATION :
☐ Sauvegarde 1 : Corrompue (bug logiciel)
☐ Sauvegarde 2 : Ancienne (6 heures de retard)
☐ Sauvegarde 3 : Formatage raté
☐ Sauvegarde 4 : Script cassé depuis 3 mois
☐ Sauvegarde 5 : Finalement OK (snapshot LVM)

LEÇON : TESTER LES SAUVEGARDES régulièrement
        Une sauvegarde non testée = 0


CAS 2 : PIXAR (TOY STORY 2, 1998)
──────────────────────────────────────────────────────────────
ERREUR : Commande `rm -rf *` lancée sur serveur de production
         → 90% du film Toy Story 2 SUPPRIMÉ (18 mois de travail)

SAUVEGARDE SERVEUR : Également supprimée (même commande)

SAUVETAGE MIRACLE :
Une employée en congé maternité avait une copie complète chez
elle (backup personnel sur workstation).

Toy Story 2 restauré, film sorti en 1999.

LEÇON : RÈGLE 3-2-1 → 1 copie HORS SITE aurait évité la panique


CAS 3 : RANSOMWARE + SAUVEGARDE CONNECTÉE (2020)
──────────────────────────────────────────────────────────────
PME française (50 employés)
Ransomware infecte le serveur

TENTATIVE RESTAURATION :
☐ Sauvegarde locale (NAS) : ÉGALEMENT CHIFFRÉE (connectée au réseau)
☐ Sauvegarde cloud : Non activée (oubli lors du setup)

RÉSULTAT : Paiement rançon 50 000 € (30% données récupérées)

LEÇON : DÉBRANCHER les sauvegardes après usage
        TESTER le cloud régulièrement

═══════════════════════════════════════════════════════════════
```

