---
author: YLP
title: 📖 Aide-Mémoire
---

# Aide-Mémoire
## Commandes et Event ID Essentiels

---

# WINDOWS - OBSERVATEUR ÉVÉNEMENTS

## Accès
```
Windows + R → eventvwr.msc
```

## 4 Journaux Principaux
- **Application** : Apps, services applicatifs
- **Sécurité** : Auth, audit, intrusions
- **Installation** : Updates, installations
- **Système** : OS, services, pilotes, matériel

## Event ID Critiques

**Système** :
- 7000 : Service n'a pas démarré
- 7001 : Service dépend autre non démarré
- 7023 : Service terminé avec erreur
- 7036 : Service démarré/arrêté (normal)
- 6008 : Arrêt inattendu (crash)
- 41 : Kernel-Power (BSOD)
- 1001 : BugCheck (détails BSOD)

**Sécurité** :
- 4624 : Connexion réussie
- 4625 : Échec connexion (⚠️ attaque si répété)
- 4648 : RunAs (élévation)
- 4672 : Privilèges admin assignés
- 4720 : Compte créé
- 4732 : Membre ajouté groupe sécurité

## PowerShell
```powershell
# Exporter logs
Get-EventLog -LogName System -EntryType Error -Newest 100 | 
  Export-Csv logs.csv

# Vérifier Event ID
Get-EventLog -LogName System | Where {$_.EventID -eq 7000}
```

---

# LINUX - /var/log

## Fichiers Principaux
```
/var/log/syslog      # Général (tous services)
/var/log/auth.log    # SSH, sudo, login
/var/log/kern.log    # Kernel, drivers
/var/log/apache2/    # Serveur web
/var/log/mysql/      # Base données
```

## Commandes Essentielles

**Consultation**
```bash
# Fin fichier (20 dernières lignes)
tail -n 20 /var/log/syslog

# Temps réel
tail -f /var/log/syslog

# Début fichier
head -n 30 /var/log/kern.log

# Navigation
less /var/log/auth.log
```

**Filtrage**
```bash
# Rechercher mot
grep "error" /var/log/syslog
grep -i "failed" /var/log/auth.log  # Ignore casse

# Compter occurrences
grep -c "Failed password" /var/log/auth.log

# Combiner
tail -n 100 /var/log/syslog | grep "error"
```

**Journalctl (systemd)**
```bash
# Tous logs
journalctl

# Service spécifique
journalctl -u ssh.service
journalctl -u apache2.service

# Par priorité
journalctl -p err        # Erreurs seulement
journalctl -p warning    # Warnings +

# Temps réel
journalctl -f

# Période
journalctl --since "1 hour ago"
journalctl --since "2026-02-18 08:00" --until "2026-02-18 10:00"

# Combiné
journalctl -u ssh.service -p err --since "today"
```

---

# MÉTHODOLOGIE DIAGNOSTIC

## 6 Étapes
1. **COLLECTER** : Quoi, Quand, Qui, Où
2. **FENÊTRE** : ±15 min autour incident
3. **CONSULTER** : Logs pertinents
4. **FILTRER** : Critique + Erreur
5. **CORRÉLER** : Cause racine
6. **DOCUMENTER** : Fiche KEDB

## Patterns Courants

**Brute Force SSH**
```bash
grep "Failed password" /var/log/auth.log | tail -50
# Si 50+ échecs même IP → Bloquer
```

**Service ne démarre pas**
```
Event 7001 → Vérifier dépendances
Event 7000 → Vérifier fichiers/permissions
```

**Disque plein**
```bash
df -h
du -sh /var/log/* | sort -hr | head -5
```

---

# ACTIONS URGENCE SÉCURITÉ

## Compromission Serveur Linux

**1. Isoler**
```bash
iptables -P INPUT DROP
iptables -P OUTPUT DROP
```

**2. Identifier**
```bash
# Processus suspects
ps aux | grep -v "\["
netstat -tulpn | grep ESTABLISHED

# Fichiers récents
find /tmp -type f -mtime -1
find /var/www -type f -mtime -1

# Cron jobs
crontab -l
crontab -u www-data -l
```

**3. Nettoyer**
```bash
# Kill processus suspect
kill -9 PID

# Supprimer backdoor
rm /chemin/backdoor.php

# Supprimer cron malveillant
crontab -r -u www-data
```

**4. Bloquer**
```bash
# Bloquer IP
iptables -A INPUT -s IP_MALVEILLANTE -j DROP

# Sauvegarder règles
iptables-save > /etc/iptables/rules.v4
```

---

# DOCUMENTATION KEDB

## Modèle Fiche
```
Ticket : INC-XXXX
Date : JJ/MM/AAAA
Durée : XX min

SYMPTÔME : [Description utilisateur]

DIAGNOSTIC :
- Logs consultés : [Quels journaux]
- Event ID / Erreurs : [Codes]

CAUSE RACINE : [Explication technique]

SOLUTION :
1. [Action 1]
2. [Action 2]

PRÉVENTION : [Mesures futures]

MOTS-CLÉS : [Pour recherche]
```

---

*Aide-Mémoire S16 BLOC 3 — BTS SIO SISR*
