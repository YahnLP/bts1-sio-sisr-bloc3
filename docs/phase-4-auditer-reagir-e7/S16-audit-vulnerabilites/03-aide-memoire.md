# Aide-mémoire – Audit de vulnérabilités

*BTS SIO SISR 1re année – Bloc 3 – S16*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Cadre légal

**Autorisation écrite** : qui autorise · qui réalise · **périmètre inclus et exclu** · dates · méthodes · contacts · confidentialité. Sans autorisation : risque d'infraction (Code pénal 323-1 et suivants).

## Nmap

| But | Commande |
|---|---|
| Découverte | `nmap -sn réseau/24` |
| Tous les ports (SYN) | `sudo nmap -sS -p- hôte` |
| Services et versions | `nmap -sV -p 21,22,80 hôte` |
| Système | `sudo nmap -O hôte` |
| Script | `nmap --script ftp-anon -p 21 hôte` |
| Sauvegarder | `-oN fichier.txt` ou `-oX fichier.xml` |

**États** : `open` · `closed` · `filtered`.

## CVE et CVSS

| Score CVSS | Gravité |
|---|---|
| 0,1 – 3,9 | Faible |
| 4,0 – 6,9 | Moyenne |
| 7,0 – 8,9 | Élevée |
| 9,0 – 10,0 | Critique |

**Prioriser** = score + exposition + exploitabilité + valeur du bien + facilité de correction.

## Fiche d'audit

Cadre · synthèse · constats (avec preuve) · risque · recommandations (action, priorité, responsable, échéance) · suivi.

> [!WARNING]
> Scan = **laboratoire isolé** ou système **autorisé par écrit**. Jamais sur Internet ni sur le réseau de l'établissement.
