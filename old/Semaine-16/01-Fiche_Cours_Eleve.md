---
author: YLP
title: 📖 Fiche de Cours Élève
---

# Fiche de Cours Élève
## Logs Système Windows et Linux

*BTS SIO SISR — Année 1 — Semaine 16*

---

## 🎯 Compétences RNCP

| Code | Compétence |
|------|------------|
| B3.1 | Identifier les principales menaces de sécurité |
| B3.3 | Gérer les incidents de sécurité |
| B1.4 | Résoudre les incidents et les demandes d'assistance |

---

# PARTIE I — LOGS WINDOWS

## 1. Qu'est-ce qu'un Log ?

**Log/Journal** = Fichier texte enregistrant chronologiquement tous les événements système.

**Rôle** : Diagnostic incidents (80% résolubles via logs), détection intrusions, conformité RGPD, analyse performance, base de connaissances ITIL.

## 2. Observateur d'Événements Windows

**Accès** : `Windows+R` → `eventvwr.msc`

**4 Journaux principaux** :
- **Application** : Événements applications (crashes, services app)
- **Sécurité** : Authentification, accès fichiers, tentatives intrusion
- **Installation** : Windows Updates, installations
- **Système** : OS, services Windows, pilotes, matériel

**5 Niveaux de sévérité** :
- 🔴 **Critique** : Panne majeure, action immédiate
- ❌ **Erreur** : Problème significatif, action rapide
- ⚠️ **Avertissement** : Problème potentiel, surveillance
- ℹ️ **Information** : Événement normal
- 🔍 **Audit** : Réussite/Échec sécurité

## 3. Event ID Windows Essentiels

**Système** :
- **7000** : Service n'a pas démarré
- **7001** : Service dépend d'un autre non démarré
- **6008** : Arrêt inattendu (crash)
- **41** : Kernel-Power (BSOD, crash matériel)

**Sécurité** :
- **4624** : Connexion réussie
- **4625** : Échec connexion (si répété = attaque brute force)
- **4672** : Privilèges admin assignés

## 4. Filtrer les Logs

Clic droit journal → Filtrer :
- Par niveau (Critique + Erreur uniquement)
- Par plage horaire (±15 min autour incident)
- Par Event ID spécifique
- Recherche texte

---

# PARTIE II — LOGS LINUX

## 1. Architecture /var/log

**Fichiers principaux** :
- **/var/log/syslog** : Log système général (tous services)
- **/var/log/auth.log** : Authentification (SSH, sudo, login)
- **/var/log/kern.log** : Noyau Linux, drivers, matériel
- **/var/log/apache2/** : Logs serveur web
- **/var/log/mysql/** : Logs base de données

## 2. Niveaux Syslog (0-7)

0=emerg, 1=alert, 2=crit, 3=err, 4=warning, 5=notice, 6=info, 7=debug

## 3. Commandes Essentielles

```bash
# Afficher fin fichier
tail -n 50 /var/log/syslog

# Suivre en temps réel
tail -f /var/log/syslog

# Filtrer par mot-clé
grep "error" /var/log/syslog
grep "Failed" /var/log/auth.log

# Compter occurrences
grep -c "Failed" /var/log/auth.log

# Logs systemd
journalctl -u ssh.service -p err --since "1 hour ago"
```

## 4. Format Ligne Log Linux

```
Feb 18 10:23:45 srv01 sshd[1234]: Failed password for alice from 192.168.1.50
│           │    │     │       │                │
Timestamp   Host Service[PID]  Message          IP source
```

---

# PARTIE III — MÉTHODOLOGIE DIAGNOSTIC

## 1. Les 6 Étapes

① **COLLECTER** : Quoi, Quand, Qui, Où
② **FENÊTRE TEMPORELLE** : ±15 min autour incident
③ **CONSULTER LOGS** : Windows (Observateur) / Linux (/var/log)
④ **FILTRER** : Critique + Erreur uniquement
⑤ **CORRÉLER** : Trouver cause racine (pas symptôme)
⑥ **DOCUMENTER** : Fiche KEDB pour base connaissances

## 2. Corrélation d'Événements

**Exemple** :
```
10:12 → Disque plein (98%)
  ↓
10:13 → SQL ne peut plus écrire
  ↓
10:15 → IIS dépend de SQL → IIS plante
  ↓
SYMPTÔME : Site web inaccessible
CAUSE RACINE : Disque plein
```

## 3. Patterns Courants

**Attaque brute force SSH** :
```
45 tentatives "Failed password" même IP en 2 min
→ Bloquer IP au firewall
```

**Service ne démarre pas** :
```
Event 7001 : Dépend service X non démarré
→ Démarrer service X d'abord
```

## 4. Documentation ITIL (Fiche KEDB)

Modèle :
- Ticket, Date, Technicien
- **SYMPTÔME** : Description utilisateur
- **DIAGNOSTIC** : Logs consultés, Event ID
- **CAUSE RACINE** : Explication technique
- **SOLUTION** : Actions effectuées
- **PRÉVENTION** : Mesures futures
- **MOTS-CLÉS** : Pour recherche

---

# VOCABULAIRE CLÉ

| Terme | Définition |
|-------|------------|
| **Log/Journal** | Fichier enregistrement chronologique événements |
| **Observateur événements** | Outil Windows `eventvwr.msc` |
| **Event ID** | Code unique identifiant type événement Windows |
| **/var/log** | Répertoire Linux contenant tous les logs |
| **syslog** | Système standard journalisation Linux |
| **auth.log** | Log authentifications Linux |
| **tail -f** | Suivre fichier log en temps réel |
| **grep** | Filtrer lignes contenant mot-clé |
| **journalctl** | Consulter logs systemd |
| **Corrélation** | Identification relations cause-effet |
| **Cause racine** | Cause originelle (≠ symptôme) |
| **KEDB** | Known Error Database (base connaissances ITIL) |
| **Pattern** | Motif récurrent indiquant type incident |

---

*Fiche de Cours S16 BLOC 3 — BTS SIO SISR*
