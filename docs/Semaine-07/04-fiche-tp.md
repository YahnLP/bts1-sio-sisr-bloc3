---
author: YLP
title: 🖥️ FICHE TP
---

# 🖥️ TP — NOTIFICATION CNIL + SCRIPT DE PURGE

*Durée : 30 minutes — Individuel*

---

## Exercice 1 — Rédiger une Notification CNIL (20 min)

**Contexte :**
Vous êtes technicien IT chez **BioSanté**, un laboratoire d'analyses médicales.

**Incident :**

> *Jeudi 14 mars, 9h : Votre antivirus détecte un comportement anormal. Analyse des logs : depuis mardi 12 mars 23h, un attaquant a accédé à votre serveur de fichiers via un compte compromis. Il a pu consulter et probablement télécharger le répertoire "Résultats Patients 2024" contenant : nom, prénom, date de naissance, médecin traitant, résultats d'analyses médicales de **4 200 patients**. Les fichiers étaient en clair (non chiffrés).*

**Mission :** Rédiger la notification CNIL via le formulaire textuel :

```
NOTIFICATION CNIL — BioSanté
═══════════════════════════════════════════════════════════════

COORDONNÉES DU RESPONSABLE
──────────────────────────────────────────────────────────────
Organisme : BioSanté SAS
DPO / Contact RGPD : _________________________________________
Email : ______________________________________________________

A — NATURE DE LA VIOLATION
──────────────────────────────────────────────────────────────
Type(s) de violation :
☐ Confidentialité  ☐ Disponibilité  ☐ Intégrité

Description des faits :
_______________________________________________________________
_______________________________________________________________
_______________________________________________________________

B — DONNÉES ET PERSONNES CONCERNÉES
──────────────────────────────────────────────────────────────
Catégories de données concernées :
_______________________________________________________________

Nombre approximatif de personnes : ___________________________

Données sensibles (catégorie particulière) ? ☐ Oui  ☐ Non
Si oui, lesquelles : ________________________________________

C — CONSÉQUENCES PROBABLES
──────────────────────────────────────────────────────────────
Risques pour les personnes concernées :
_______________________________________________________________
_______________________________________________________________

D — MESURES PRISES
──────────────────────────────────────────────────────────────
Mesures immédiates :
_______________________________________________________________
_______________________________________________________________

Mesures correctives prévues :
_______________________________________________________________
_______________________________________________________________

E — NOTIFICATION AUX PERSONNES
──────────────────────────────────────────────────────────────
Les personnes concernées doivent-elles être notifiées ?
☐ Oui  ☐ Non

Justification :
_______________________________________________________________

F — DATE ET HEURE
──────────────────────────────────────────────────────────────
Date/heure de prise de connaissance : ____ / ____ / 2024 à ____h____
Date/heure de notification CNIL : ____ / ____ / 2024 à ____h____
Délai respecté (< 72h) ? ☐ Oui  ☐ Non

═══════════════════════════════════════════════════════════════
```

---

## Exercice 2 — Script de Purge Automatique (10 min)

**Contexte :**
La politique de conservation de BioSanté prévoit :
- Résultats d'analyses : **20 ans** (obligation santé)
- Données de connexion (logs) : **1 an**
- Emails internes : **5 ans**

**Mission :** Compléter les tâches CRON suivantes :

```bash
# crontab -e — Tâches planifiées RGPD BioSanté

# 1. Purge des logs de connexion (1 an)
# Exécution : Tous les jours à 3h du matin
____  ____  ____  ____  ____  find /var/log/biosante/ -name "*.log" \
  -mtime ____  -delete >> /var/log/purge_rgpd.log

# 2. Archivage des résultats d'analyses (20 ans)
# Exécution : Premier jour de chaque mois à 2h
____  ____  ____  ____  ____  mysql -u purge_user biosante_db \
  -e "UPDATE resultats SET statut='archive' \
  WHERE date_analyse < DATE_SUB(NOW(), INTERVAL ____ YEAR) \
  AND statut='actif';"

# 3. Purge définitive des résultats > 20 ans
# Exécution : Premier jour de chaque mois à 2h30
30  2  1  *  *  mysql -u purge_user biosante_db \
  -e "DELETE FROM resultats \
  WHERE date_analyse < DATE_SUB(NOW(), INTERVAL ____ YEAR) \
  AND statut='archive';"

# Réponses attendues :
# Cron quotidien 3h : 0 3 * * *
# -mtime +365 (jours)
# Cron mensuel 1er à 2h : 0 2 1 * *
# INTERVAL 20 YEAR (conservation active → archivage)
# INTERVAL 20 YEAR (purge après 20 ans archivés)
```

---
