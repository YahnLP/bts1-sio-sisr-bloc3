# Aide-mémoire – Architecture et durcissement

*BTS SIO SISR 1re année – Bloc 3 – S14*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Principes

**Défense en profondeur · moindre privilège · cloisonnement · refus par défaut · surface d'attaque réduite.**

## Zones

| Zone | Rôle |
|---|---|
| **DMZ** | Services exposés à Internet, isolés de l'interne |
| **LAN** | Postes utilisateurs |
| **Serveurs** | Données et services internes |
| **Administration** | Seuls postes autorisés à administrer |

La **matrice de flux** liste les flux autorisés ; le reste est refusé.

## Durcir Linux

| Mesure | Commande ou réglage |
|---|---|
| Ports en écoute | `ss -tlnp` |
| Services actifs | `systemctl list-unit-files --state=enabled` |
| Arrêter un service | `sudo systemctl disable --now service` |
| SSH par clés | `PermitRootLogin no`, `PasswordAuthentication no`, `AllowUsers …` |
| Tester SSH | `sudo sshd -t` puis `sudo systemctl reload ssh` |
| Clé SSH | `ssh-keygen -t ed25519` puis `ssh-copy-id` |
| Pare-feu | `ufw default deny incoming` → `ufw allow …` → `ufw enable` |
| Mises à jour auto | `apt install unattended-upgrades` |
| Audit | `sudo lynis audit system` |

> [!WARNING]
> Ouvrir l'accès SSH **avant** d'activer le pare-feu, tester la configuration **avant** de recharger, garder une **console** ouverte.

## Référentiels

**ANSSI** : guide d'hygiène informatique et guides de configuration ; **CIS Benchmarks** ; outils d'audit (Lynis, OpenSCAP).
