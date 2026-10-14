# Aide-mémoire – VPN et WireGuard

*BTS SIO SISR 1re année – Bloc 3 – S13*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## VPN

| Terme | Sens |
|---|---|
| **Tunnel** | Paquets encapsulés et chiffrés dans d'autres paquets |
| **Nomade** | Un utilisateur se connecte au réseau de l'entreprise |
| **Site à site** | Deux réseaux reliés en permanence |
| **Tunnel complet / partiel** | Tout le trafic / seulement les réseaux d'entreprise |

## Protocoles

| Protocole | À retenir |
|---|---|
| **IPsec** (IKEv2) | Standard des pare-feu, site à site |
| **OpenVPN** | TLS, certificats, port 443 possible |
| **WireGuard** | Simple, rapide, une paire de clés par machine, UDP |
| **VPN SSL** | Portail web pour quelques applications |

## WireGuard : configuration minimale

```ini
[Interface]
Address = 10.8.0.2/24
PrivateKey = <clé privée de CETTE machine>

[Peer]
PublicKey = <clé publique de l'AUTRE machine>
Endpoint = ip-serveur:51820
AllowedIPs = 10.8.0.1/32, 172.16.0.0/24
PersistentKeepalive = 25
```

`AllowedIPs` : **routage** à l'envoi + **filtrage** à la réception.

## Commandes

| But | Commande |
|---|---|
| Clés | `wg genkey \| tee privee.key \| wg pubkey > publique.key` |
| Monter / couper | `sudo wg-quick up wg0` / `sudo wg-quick down wg0` |
| État du tunnel | `sudo wg show` |
| Retirer un pair | `sudo wg set wg0 peer <clé> remove` |
| Voir le trafic chiffré | `sudo tcpdump -ni enp0s3 udp port 51820` |
| Voir le trafic clair du tunnel | `sudo tcpdump -ni wg0` |

> [!WARNING]
> La clé **privée** ne se partage ni ne se publie jamais. Une clé par appareil. Un VPN est une **porte d'entrée** : moindre privilège, révocation, journaux, mises à jour.
