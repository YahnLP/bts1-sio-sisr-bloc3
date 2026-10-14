# Aide-mémoire – Réponse à incident et preuves

*BTS SIO SISR 1re année – Bloc 3 – S17*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Phases

**Préparer · détecter/qualifier · contenir · éradiquer · restaurer · retour d'expérience.**

On **éradique avant de restaurer**.

## Rançongiciel : premiers réflexes

1. **Isoler** les machines du réseau (câble, Wi-Fi) ; décider en connaissance de cause d'éteindre ou non.
2. **Protéger** les sauvegardes (débrancher).
3. **Prévenir** la direction, le DPO.
4. **Noter** (main courante horodatée).
5. **Collecter** avant de nettoyer.
6. **Ne pas payer** sans analyse.
7. **Déposer plainte** ; déclarer à l'assureur.

## Qui prévenir

Direction · DPO · **CNIL sous 72 h** (données personnelles, risque) · personnes (risque élevé) · assureur · police ou gendarmerie · Cybermalveillance.gouv.fr · clients.

## Collecte de preuves

| Règle | |
|---|---|
| Copies, pas originaux | Support externe |
| **Ordre de volatilité** | Mémoire/état → temporaires → disque → distants |
| **Empreintes** | `sha256sum fichiers > SHA256SUMS` |
| **Documenter** | Qui, quand, comment |
| **Chaîne de possession** | Qui détient la preuve |

| But | Commande |
|---|---|
| Connexions | `ss -tupan` |
| Processus | `ps -eo pid,ppid,user,lstart,cmd` |
| Sessions | `who -a`, `last -n 30` |
| Journal | `journalctl --no-pager -n 500` |
| Vérifier | `sha256sum -c SHA256SUMS` |

> [!WARNING]
> Ne « nettoie » pas avant d'avoir collecté. Ne te connecte pas avec un compte administrateur sur une machine infectée.
