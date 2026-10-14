# Aide-mémoire – Journaux et détection

*BTS SIO SISR 1re année – Bloc 3 – S15*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Journaux utiles

| Source | Où |
|---|---|
| Authentification Linux | `journalctl -u ssh`, `/var/log/auth.log` |
| Système | `journalctl`, `/var/log/syslog` |
| Serveur web | `/var/log/nginx/access.log` |
| Windows | Observateur d'événements → Sécurité |

**4624** connexion réussie · **4625** échec · **4720** compte créé · **4732** ajout à un groupe · **1102** journal effacé.

## Bonnes pratiques

Horloges **synchronisées** · journaux **centralisés** et **protégés** · **rotation** · durée **limitée** · **alertes** lues.

## Repérer une force brute

| But | Commande |
|---|---|
| Nombre d'échecs | `grep -c "Failed password" auth.log` |
| Adresses sources | `grep "Failed password" auth.log \| awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' \| sort \| uniq -c \| sort -rn` |
| Succès après échecs | `grep -B3 "Accepted" auth.log` |

## Fail2ban

```ini
[DEFAULT]
ignoreip = 127.0.0.1/8 ::1 <adresse admin>
[sshd]
enabled = true
backend = systemd
maxretry = 3
findtime = 10m
bantime = 10m
```

`fail2ban-client status sshd` · `fail2ban-client set sshd unbanip IP`.

## IDS / IPS

| | Action | Exemples |
|---|---|---|
| **IDS** | Alerte | Suricata, Snort |
| **IPS** | Bloque | Suricata en ligne |
| **HIDS** | Surveille une machine | Wazuh, OSSEC |

Règle : `alert tcp any any -> $HOME_NET any (msg:"…"; flags:S; threshold:type both, track by_src, count 20, seconds 5; sid:1000002; rev:1;)`

Tester : `sudo suricata -T -c /etc/suricata/suricata.yaml -v` · alertes : `/var/log/suricata/fast.log`.

> [!WARNING]
> Un blocage automatique peut bloquer un utilisateur légitime : **liste blanche**, **durée limitée**, tests en laboratoire.
