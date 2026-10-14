# Corrigé S13

## Partie A

1. On échange les clés **publiques**. La clé **privée** reste sur sa machine.
2. 32 octets encodés en **base 64** (44 caractères, terminés par `=`).

## Partie B

3. `latest handshake` : instant de la dernière poignée de main cryptographique réussie (preuve que les deux pairs se sont authentifiés) ; `transfer` : volumes reçus et envoyés. S'il n'y a pas de handshake, le tunnel n'est pas établi.
4. `172.16.0.0/24 dev wg0` (route vers le réseau d'entreprise via le tunnel), en plus de `10.8.0.0/24`.
5. Le paquet est envoyé dans le tunnel (adresse autorisée), le serveur le reçoit, mais aucune machine ne répond : l'adresse `172.16.0.99` n'existe pas dans le laboratoire. Il n'y a pas de blocage par le VPN ; c'est l'**absence de destinataire**.
6. Le serveur ne reconnaît pas l'émetteur : les paquets sont **ignorés en silence**, sans handshake. C'est volontaire : le serveur ne répond pas aux inconnus.

## Partie C

7. Des paquets **UDP** entre `192.168.56.20` et `192.168.56.10` sur le port 51820, avec un contenu chiffré.
8. Le contenu : ni ICMP, ni adresses internes (`10.8.0.x`, `172.16.0.x`), ni protocoles applicatifs.
9. Les adresses publiques, le port, la **taille** et le **rythme** des paquets : cela suffit à savoir qu'il existe un VPN et quand il est actif. C'est acceptable pour la confidentialité des échanges, mais pas pour une exigence de **discrétion** (la présence d'un VPN n'est pas cachée).

## Partie D

10. Non : `172.16.0.0/24` n'est plus dans `AllowedIPs`, donc le client n'envoie pas ce trafic dans le tunnel (pas de route) ; `10.8.0.1` fonctionne toujours.
11. La route par défaut passe par `wg0` (WireGuard installe des routes qui couvrent tout le trafic). Tout le trafic Internet du client transite par l'entreprise.
12. Quand l'entreprise veut **contrôler et journaliser** tout le trafic du poste nomade (filtrage web, antivirus réseau), ou pour un poste sur un réseau non sûr.
13. Non : plus de nouveau handshake accepté ; `wg show` n'affiche plus le pair, et le `ping` ne répond plus (après expiration du dernier échange).
14. Révoquer son pair immédiatement, chiffrer les disques des portables (S05), protéger l'accès VPN par un second facteur, journaliser les connexions, déclarer la perte (procédure d'incident, S17).
15. Le port **UDP 51820** (ou celui choisi dans `ListenPort`).
16. Cela autoriserait n'importe quelle source à se faire passer pour ce pair : on limite à l'adresse de tunnel **de ce client** (`10.8.0.2/32`).

## Partie E

| # | Type | Protocole | Mesures |
|---|---|---|---|
| 1 | Nomade | OpenVPN, WireGuard avec une solution de gestion, ou IPsec/IKEv2 selon le pare-feu | MFA, accès limités à l'ERP, postes conformes, journaux |
| 2 | Site à site | IPsec entre les deux pare-feu (ou WireGuard) | Clés/certificats protégés, filtrage entre sites, supervision du tunnel |
| 3 | Nomade restreint | VPN SSL à portail, ou accès VPN avec règle de pare-feu vers un seul serveur | Compte nominatif, accès limité dans le temps et à une destination, journalisation, désactivation après l'intervention |
