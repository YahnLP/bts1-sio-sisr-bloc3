# Cours – Journalisation, détection d'intrusion (IDS/IPS) et réaction

*BTS SIO SISR 1re année – Bloc 3 – S15 – à lire avant le [TP](02-tp.md)*

> [!NOTE] Ce que tu dois savoir déjà
> - **Prérequis :** S03 (force brute), S14 (architecture, pare-feu) ; lecture de commandes shell (`grep`, `awk`).
> - **Matériel :** Deux VM Debian de laboratoire (`fail2ban`, `suricata`, `nmap`, `rsyslog`) ; VM Windows de laboratoire pour l'observateur d'événements

## À la fin de ce cours tu sauras

- [ ] **Identifier** les journaux utiles (système, authentification, pare-feu, applications) et les événements Windows à surveiller ;
- [ ] **Extraire** d'un journal les indices d'une force brute avec `grep`, `awk` et `sort` ;
- [ ] **Configurer** Fail2ban pour bannir automatiquement une adresse qui multiplie les échecs ;
- [ ] **Distinguer** IDS et IPS, détection par signatures et par comportement ;
- [ ] **Écrire** une règle Suricata simple et **vérifier** qu'elle déclenche une alerte.

## I. Pourquoi journaliser ?

Les **journaux** (*logs*) enregistrent ce qui se passe sur un système : connexions, erreurs, changements, flux réseau. Sans eux, on ne sait ni **détecter** une attaque, ni **comprendre** ce qui s'est passé, ni **prouver** les faits (S09, S17).

| Usage | Exemple |
|---|---|
| **Détection** | Cinquante échecs de connexion en une minute |
| **Investigation** | Quel compte a lu ce fichier, à quelle heure, depuis quelle adresse ? |
| **Preuve** | Journal horodaté et intègre (S09) |
| **Exploitation** | Diagnostiquer une panne |
| **Conformité** | Traçabilité exigée par un référentiel ou un contrat (et limitée dans le temps, S08) |

### Les sources principales

| Source | Où | Exemples d'événements |
|---|---|---|
| **Authentification Linux** | `/var/log/auth.log`, `journalctl -u ssh` | `Failed password`, `Accepted publickey`, `sudo` |
| **Système Linux** | `journalctl`, `/var/log/syslog` | Démarrages, services, erreurs du noyau |
| **Serveur web** | `/var/log/nginx/access.log`, `error.log` | Requêtes, codes 4xx/5xx, tentatives d'injection |
| **Pare-feu** | Journal du pare-feu | Connexions refusées, scans de ports |
| **Windows** | Observateur d'événements (journal **Sécurité**) | Connexions, créations de comptes, effacement du journal |
| **Applications et bases** | Journaux applicatifs | Erreurs, requêtes lentes, exports massifs |

### Événements Windows à connaître

| ID | Signification |
|---|---|
| **4624** | Ouverture de session **réussie** |
| **4625** | Échec d'ouverture de session |
| **4720** | Compte utilisateur **créé** |
| **4732** | Membre **ajouté** à un groupe local de sécurité (par exemple Administrateurs) |
| **1102** | Journal de sécurité **effacé** (signe d'une dissimulation de traces) |

(à confirmer sur la documentation Microsoft selon la version.)

### Bonnes pratiques de journalisation

- **Horloges synchronisées** (NTP) : sinon, impossible de corréler les événements de plusieurs machines ;
- **Centraliser** sur un serveur (rsyslog, ou une solution de supervision de sécurité) : un attaquant qui s'empare d'une machine peut effacer ses journaux locaux ;
- **Protéger** les journaux (droits, intégrité, copie hors machine) ;
- **Limiter** la durée de conservation et les données personnelles qu'ils contiennent (adresses IP : S08) ;
- **Rotation** pour éviter de remplir le disque (`logrotate`) ;
- **Surveiller** : un journal que personne ne lit est inutile. On définit des **alertes** sur les événements critiques.

## II. Analyser un journal

Une force brute a une signature : **beaucoup d'échecs, une même source, un court laps de temps**.

| Question | Outil |
|---|---|
| Combien d'échecs ? | `grep -c "Failed password" fichier` |
| Depuis quelles adresses ? | `grep … \| awk … \| sort \| uniq -c \| sort -rn` |
| Quels comptes visés ? | Extraire le champ du nom d'utilisateur |
| **Y a-t-il eu un succès après les échecs ?** | `grep -B3 "Accepted"` : un succès après une série d'échecs peut signaler un compte compromis |
| Ce n'est pas une erreur de frappe ? | Comptes inexistants (`invalid user`) → scan automatique |

## III. Détecter : IDS et IPS

| | **IDS** (*Intrusion Detection System*) | **IPS** (*Intrusion Prevention System*) |
|---|---|---|
| Action | **Observe et alerte** | **Observe et bloque** |
| Position | En copie du trafic (miroir) | **En ligne** sur le chemin du trafic |
| Risque | Alerte non traitée | **Faux positif** : trafic légitime bloqué |
| Avantage | N'affecte pas le service | Réagit sans délai |

On distingue aussi :

| Niveau | Surveille | Exemple |
|---|---|---|
| **Réseau** (NIDS/NIPS) | Le trafic réseau | **Suricata**, **Snort** |
| **Hôte** (HIDS/HIPS) | Une machine : fichiers, processus, journaux | **Wazuh**, **OSSEC**, **Fail2ban** (réaction simple sur journaux) |

### Deux méthodes de détection

| Méthode | Principe | Limite |
|---|---|---|
| **Signatures** | Compare à des motifs d'attaques connus | Ne détecte pas ce qui est nouveau |
| **Comportement / anomalie** | Repère ce qui s'écarte de la normale | Faux positifs, apprentissage nécessaire |

### Une règle Suricata

Une règle décrit : l'**action**, le **protocole**, les **adresses et ports**, et des **options**.

```text
alert tcp any any -> $HOME_NET 22 (msg:"LAB - rafale de connexions SSH"; flags:S; threshold:type both, track by_src, count 5, seconds 10; sid:1000001; rev:1;)
```

| Élément | Sens |
|---|---|
| `alert` | Action : générer une alerte (on peut aussi `drop` en mode IPS) |
| `tcp any any -> $HOME_NET 22` | De n'importe quelle source vers notre réseau, port 22 |
| `msg` | Message de l'alerte |
| `flags:S` | Paquets de demande de connexion (SYN) |
| `threshold … count 5, seconds 10` | Alerte si 5 SYN en 10 secondes depuis la même source |
| `sid` | Identifiant de la règle (les valeurs ≥ 1 000 000 sont réservées aux règles locales) |

## IV. Réagir

| Niveau de réaction | Exemple | Précaution |
|---|---|---|
| **Alerter** | Courriel, tableau de bord | Éviter le bruit : trop d'alertes = aucune alerte lue |
| **Bloquer automatiquement** | Fail2ban bannit une adresse après N échecs | Ne pas bloquer ses propres adresses ; durée limitée ; usurpation d'adresse possible |
| **Isoler** | Mettre un poste en quarantaine | Décision humaine, procédure d'incident (S17) |

Une architecture complète regroupe les journaux dans un **SIEM** (*Security Information and Event Management*) qui les **centralise**, les **corrèle** et déclenche des alertes. Les petites structures commencent par une centralisation simple et quelques alertes bien choisies.

## À retenir

- Les journaux permettent de **détecter, comprendre et prouver** ; ils doivent être **horodatés, centralisés, protégés et limités dans le temps**.
- Une force brute se repère par **beaucoup d'échecs, une source, peu de temps** ; un **succès après des échecs** est un signal fort.
- **IDS** alerte, **IPS** bloque ; **signatures** ou **comportement** ; réseau ou hôte.
- Réagir automatiquement est utile mais demande des **garde-fous** (liste blanche, durée limitée).
- Un **SIEM** centralise et corrèle ; sans lecture des alertes, la détection ne sert à rien.
