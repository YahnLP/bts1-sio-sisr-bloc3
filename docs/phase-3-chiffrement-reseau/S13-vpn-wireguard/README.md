# S13 – VPN : protéger les échanges entre sites et utilisateurs nomades

| Élément | Détail |
|---|---|
| **Niveau** | BTS SIO option SISR, 1re année – bloc 3 |
| **Séance** | S13 (séance 13 sur 19) – Phase 3 |
| **Durée** | 4 heures |
| **Prérequis** | S10 et S11 (chiffrement, clés publiques et privées) ; notions de routage IP. |
| **Matériel** | Deux VM Debian de laboratoire sur un réseau interne (`wireguard`, `tcpdump`) ; droits `sudo` |
| **Compétences travaillées** | B3.4 · B3.5A (voir [le référentiel](../../ressources/referentiel.md)) |

> [!NOTE]
> **Question qui guide la séance :** *« Comment permettre à un utilisateur à distance d'accéder au réseau de l'entreprise sans exposer ses échanges ? »*

## Objectifs

À la fin de la séance, l'étudiant est capable de :

1. **Définir** un VPN et la tunnelisation, et **distinguer** VPN nomade et VPN site à site ;
2. **Comparer** IPsec, OpenVPN et WireGuard (usage, forces, limites) ;
3. **Monter** un tunnel WireGuard avec une paire de clés par machine ;
4. **Vérifier** que le trafic est chiffré et que seules les routes prévues passent par le tunnel ;
5. **Citer** les mesures de sécurité d'un VPN d'entreprise (authentification, moindre privilège, journalisation).

## Contenu de la séance

| Document | Rôle |
|---|---|
| [Cours – VPN : principes, protocoles et architecture](01-cours.md) | Cours |
| [TP – Monter un tunnel WireGuard entre un client nomade et un serveur](02-tp.md) | TP |
| [Aide-mémoire – VPN et WireGuard](03-aide-memoire.md) | Aide-mémoire |

## Déroulé conseillé (4 h)

| Durée | Activité | Format |
|---|---|---|
| 0 h 00 – 0 h 15 | **Rappel d'amorçage** (S11) : que faut-il pour authentifier une extrémité ? | Oral |
| 0 h 15 – 1 h 15 | **Cours** : tunnel, types de VPN, protocoles, architecture | Cours et questions |
| 1 h 15 – 2 h 30 | **TP partie A et B** : installation, clés, configuration, démarrage du tunnel | Binôme |
| 2 h 30 – 3 h 20 | **TP parties C et D** : observation du trafic, routes, restrictions | Binôme |
| 3 h 20 – 3 h 40 | **TP partie E** : analyse de scénarios d'entreprise | Binôme |
| 3 h 40 – 4 h 00 | **Bilan de compétences** | Individuel |

## Retour en entreprise

Si ta situation le permet : **observer** comment ton entreprise traite le sujet de la séance, **documenter** en une demi-page l'écart avec le TP, ou **réaliser** une partie après accord de ton tuteur. Voir [Transfert en entreprise](../../ressources/transfert-entreprise.md).

## Évaluation

- Fichiers de configuration (sans clé privée), sorties de commandes et réponses, nommés `RENDU-B3-S13-NOM.pdf`.
- Bilan de compétences rempli à la fin de la séance (individuel).

<details markdown="1">
<summary>Notes pour l'enseignant</summary>

- **Compétences :** codes relus sur le référentiel (page [Référentiel](../../ressources/referentiel.md)) ; le choix des compétences pour cette séance est une proposition à valider.
- La configuration WireGuard (clés, `wg-quick`, `AllowedIPs`, `PersistentKeepalive`) est standard mais **non exécutée** pendant la rédaction (paquet absent du bac à sable) : à tester sur les VM avant la séance.
- Aucune clé privée ne doit figurer dans les rendus : le TP le rappelle.
- Les clés et adresses du TP sont des valeurs de laboratoire.

</details>
