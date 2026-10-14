---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "VPN · Tunnelisation · Site-à-Site · Nomade · Protocoles"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 14*

---

## PARTIE II — Le VPN : Concept et Tunnelisation

### II.A. Définition

**VPN** = Virtual Private Network — Réseau Privé Virtuel

```
   DÉFINITION OPÉRATIONNELLE
   ═══════════════════════════════════════════════════════════════

   Un VPN est une connexion sécurisée et chiffrée
   établie sur un réseau public (Internet)
   simulant une liaison réseau privée dédiée.

   TROIS PROPRIÉTÉS FONDAMENTALES
   ──────────────────────────────────────────────────────────────
   ① CONFIDENTIALITÉ : Le trafic est chiffré (AES-256)
      → Illisible pour un observateur sur le trajet

   ② AUTHENTIFICATION : Les deux extrémités sont vérifiées
      → Certificats X.509 ou clé pré-partagée (PSK)
      → Impossible de se connecter sans les bonnes credentials

   ③ INTÉGRITÉ : Les données ne peuvent pas être modifiées
      → HMAC-SHA256/384 vérifie chaque paquet
      → Un paquet altéré est détecté et rejeté

   CE QU'UN VPN N'EST PAS
   ──────────────────────────────────────────────────────────────
   ❌ Un VPN n'anonymise pas complètement (le fournisseur VPN voit)
   ❌ Un VPN commercial (NordVPN, ProtonVPN) ≠ VPN d'entreprise
      (usages totalement différents)
   ❌ Un VPN ne protège pas des malwares sur votre machine
   ❌ Un VPN ne remplace pas HTTPS (couches complémentaires)
```

---

### II.B. La Tunnelisation : Principe Technique

```
   CONCEPT DE TUNNELISATION (Encapsulation)
   ═══════════════════════════════════════════════════════════════

   SANS VPN : Paquet IP classique
   ──────────────────────────────────────────────────────────────

   ┌────────────────────────────────────────────────────┐
   │  En-tête IP  │  En-tête TCP  │  Données (HTTP...)  │
   │  Src: 192.168.1.10           │                     │
   │  Dst: 10.0.0.5 (intranet)    │  GET /fichier.xlsx  │
   └────────────────────────────────────────────────────┘
   → Visible sur Internet, routeurs intermédiaires lisent tout

   AVEC VPN : Paquet encapsulé et chiffré
   ──────────────────────────────────────────────────────────────

   ┌────────────────────────────────────────────────────────────┐
   │ En-tête IP EXTERNE │ En-tête VPN │ PAQUET CHIFFRÉ         │
   │ Src: 82.64.12.5    │ (IPsec/UDP) │ ████████████████████   │
   │ Dst: 51.75.88.3    │             │ (paquet original caché)│
   └────────────────────────────────────────────────────────────┘
         ↑                                   ↑
   Adresse IP PUBLIQUE               Tout le contenu
   (visible sur Internet)            est chiffré ici

   CE QUI SE PASSE CÔTÉ RÉSEAU
   ──────────────────────────────────────────────────────────────

   Machine cliente                        Serveur VPN
   192.168.1.10 (IP privée)              51.75.88.3 (IP publique)
         │                                      │
         │  Encapsulation + Chiffrement         │
         │  [IP externe: 82.64.12.5→51.75.88.3]│
         │  [Contenu chiffré AES-256]           │
         ├──────── INTERNET PUBLIC ─────────────►
         │        (routeurs voient seulement    │
         │         l'IP externe, pas le contenu)│
                                                │
                                         Décapsulation
                                         Déchiffrement
                                                │
                                         Réseau interne
                                         10.0.0.0/24
                                         (intranet, fichiers...)

   NOTION D'INTERFACE VIRTUELLE
   ──────────────────────────────────────────────────────────────
   Le client VPN crée une interface réseau virtuelle (tun0/tap0) :
   → Interface physique : eth0 (192.168.1.10) → vers box/routeur
   → Interface VPN : tun0 (10.8.0.2) → vers réseau interne VPN

   Tout le trafic vers le réseau interne passe par tun0
   → Encapsulé, chiffré, envoyé via eth0 vers le serveur VPN
```

---

## PARTIE III — Types de VPN

### III.A. VPN Site-à-Site

```
   VPN SITE-À-SITE (LAN-to-LAN)
   ═══════════════════════════════════════════════════════════════

   DÉFINITION
   ──────────────────────────────────────────────────────────────
   Tunnel VPN PERMANENT entre deux (ou plusieurs) réseaux locaux.
   Établi entre les équipements de bordure (routeurs, firewalls).
   TRANSPARENT pour les utilisateurs (ils ne savent pas qu'il y a un VPN).

   TOPOLOGIE
   ──────────────────────────────────────────────────────────────

   SITE PARIS (Siège)               SITE LYON (Agence)
   ─────────────────                ─────────────────────
   Réseau : 10.1.0.0/24             Réseau : 10.2.0.0/24
   Serveur fichiers : 10.1.0.10     Postes de travail
   Serveur intranet  : 10.1.0.20    Imprimantes
         │                                │
   ┌─────▼──────┐                  ┌─────▼──────┐
   │ Firewall   │                  │ Firewall   │
   │ pfSense    │    TUNNEL VPN    │ pfSense    │
   │ Paris      ├──────────────────┤ Lyon       │
   │ IP pub:    │  (IPsec/IKEv2)  │ IP pub:    │
   │ 82.64.12.5 │                  │ 91.23.45.6 │
   └────────────┘                  └────────────┘
         │                                │
   Internet ───────────────────────── Internet

   Résultat : Un poste de Lyon (10.2.0.5) peut accéder
              au serveur Paris (10.1.0.10) comme s'ils
              étaient sur le même réseau local.

   CAS D'USAGE
   ──────────────────────────────────────────────────────────────
   → Entreprise multi-sites (siège + agences + filiales)
   → Interconnexion de datacenters
   → Partenariats B2B (accès contrôlé aux ressources partagées)

   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   ✅ Transparent pour les utilisateurs (pas de client VPN)
   ✅ Connexion permanente (toujours disponible)
   ✅ Haut débit possible (débit dépend de l'Internet)
   ✅ Gestion centralisée (sur les équipements réseau)
   ❌ Moins flexible (fixé entre des sites prédéfinis)
   ❌ Nécessite des équipements compatibles des deux côtés
   ❌ Si le tunnel tombe → Communication inter-sites interrompue
```

---

### III.B. VPN Nomade (Remote Access)

```
   VPN NOMADE / ACCÈS DISTANT (Remote Access VPN)
   ═══════════════════════════════════════════════════════════════

   DÉFINITION
   ──────────────────────────────────────────────────────────────
   Connexion à la demande entre un CLIENT individuel (poste nomade)
   et le réseau de l'entreprise.
   Nécessite un CLIENT VPN installé sur le poste de l'utilisateur.

   TOPOLOGIE
   ──────────────────────────────────────────────────────────────

   Commercial en déplacement          Réseau entreprise
   ────────────────────────           ─────────────────────────
   Hôtel, gare, domicile              10.0.0.0/16
   IP publique dynamique              Serveur fichiers, ERP, email
         │                                     │
   ┌─────▼──────┐                     ┌────────▼──────┐
   │ Client VPN │                     │ Serveur VPN   │
   │ (OpenVPN,  │ ─── TUNNEL VPN ───► │ (Concentrateur│
   │  WireGuard,│  (à la demande)     │  VPN)         │
   │  FortiVPN) │                     │ IP pub:       │
   │ IP VPN:    │                     │ 51.75.88.3    │
   │ 10.8.0.5   │                     └───────────────┘
   └────────────┘

   Une fois connecté : Le poste du commercial obtient une IP
   dans le réseau VPN (10.8.0.5) et peut accéder à tous
   les services internes comme s'il était au bureau.

   CAS D'USAGE
   ──────────────────────────────────────────────────────────────
   → Télétravail (accès intranet, ERP, fichiers depuis domicile)
   → Commerciaux / Techniciens en déplacement
   → Prestataires externes (accès limité et contrôlé)
   → Administration de serveurs depuis l'extérieur (sysadmins)

   CARACTÉRISTIQUES
   ──────────────────────────────────────────────────────────────
   ✅ Très flexible (depuis n'importe quel réseau)
   ✅ Authentification forte par utilisateur (MFA possible)
   ✅ Politique par utilisateur (segmentation des accès)
   ✅ Connexion à la demande (pas de ressources consommées en permanence)
   ❌ Nécessite un client VPN sur chaque poste
   ❌ Dépend de l'Internet de l'utilisateur
   ❌ Scalabilité : Plus d'utilisateurs = Plus de ressources serveur

   COMPARAISON SITE-À-SITE vs NOMADE
   ──────────────────────────────────────────────────────────────
                      │ Site-à-Site      │ Nomade
   ───────────────────┼──────────────────┼───────────────────
   Établi entre       │ Réseaux entiers  │ Poste ↔ Réseau
   Initié par         │ Équipement réseau│ Utilisateur
   Durée              │ Permanent        │ À la demande
   Client requis      │ Non (transparent)│ Oui (logiciel)
   Authentification   │ Certificat/PSK   │ Utilisateur/Cert
   Cas d'usage        │ Multi-sites      │ Télétravail
```

---

## PARTIE IV — Protocoles VPN

### IV.A. IPsec (Internet Protocol Security)

```
   IPsec — LE STANDARD HISTORIQUE
   ═══════════════════════════════════════════════════════════════

   Protocole : Couche 3 (Réseau) — Intégré dans le protocole IP
   Standard  : RFC 4301 (IETF) — Utilisé depuis 1995

   DEUX MODES DE FONCTIONNEMENT
   ──────────────────────────────────────────────────────────────

   MODE TRANSPORT
   ──────────────────────────────────────────────────────────────
   Seul le payload IP est chiffré.
   L'en-tête IP reste en clair.
   → Usage : Chiffrement bout en bout entre 2 hôtes

   MODE TUNNEL (plus courant)
   ──────────────────────────────────────────────────────────────
   Le paquet IP entier est encapsulé dans un nouveau paquet.
   → Usage : VPN Site-à-Site (entre les firewalls/routeurs)

   DEUX PROTOCOLES COMPOSANTS
   ──────────────────────────────────────────────────────────────
   AH (Authentication Header)
   → Intégrité + Authentification SANS chiffrement (rare)

   ESP (Encapsulating Security Payload)
   → Intégrité + Authentification + CHIFFREMENT (standard)
   → C'est ESP qu'on utilise toujours en pratique

   IKE / IKEv2 (Échange de clés)
   ──────────────────────────────────────────────────────────────
   Internet Key Exchange : Protocole d'établissement du tunnel
   → Phase 1 : Authentification des deux parties (certificats ou PSK)
   → Phase 2 : Négociation des algorithmes + échange de clé DH
   → Établit les SA (Security Associations) : paramètres du tunnel

   SUITES CRYPTOGRAPHIQUES IPsec RECOMMANDÉES (2025)
   ──────────────────────────────────────────────────────────────
   IKEv2 + ECDH P-256 + AES-256-GCM + SHA-384
   → Suite 4 (RFC 8221) — Standard moderne
```

---

### IV.B. OpenVPN

```
   OpenVPN — LE STANDARD OPEN SOURCE
   ═══════════════════════════════════════════════════════════════

   Protocole : Couche applicative (UDP ou TCP port 443/1194)
   License   : Open Source (GPL)
   Support   : Windows, macOS, Linux, Android, iOS, routeurs

   FONCTIONNEMENT
   ──────────────────────────────────────────────────────────────
   → Utilise TLS pour l'authentification et l'échange de clé
   → Certificats X.509 (PKI) ou PSK pour l'authentification
   → AES-256-GCM pour le chiffrement des données
   → Interface tun (routage L3) ou tap (bridge L2)

   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Port 443/UDP = Traverse presque tous les firewalls et proxys
   ✅ Open source = Auditable, pas de backdoor possible (theoretically)
   ✅ Très flexible (authentification cert + login/MDP + 2FA)
   ✅ Communauté large, documentation abondante
   ✅ Fonctionne sur tout

   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ Plus lent que WireGuard (userspace, overhead TLS)
   ❌ Configuration complexe (PKI requise)
   ❌ Protocole "vieillissant" (conçu dans les années 2000)

   FICHIER DE CONFIG TYPIQUE (client)
   ──────────────────────────────────────────────────────────────
   # /etc/openvpn/client.conf
   client
   dev tun
   proto udp
   remote vpn.entreprise.fr 1194
   ca ca.crt          # Certificat Root CA (S13)
   cert client.crt    # Certificat client
   key client.key     # Clé privée client
   cipher AES-256-GCM
   auth SHA256
   tls-version-min 1.2
   verb 3
```

---

### IV.C. WireGuard

```
   WireGuard — LE NOUVEAU STANDARD
   ═══════════════════════════════════════════════════════════════

   Créé par : Jason Donenfeld (2018)
   Protocole : Couche réseau (UDP uniquement)
   Code source : ~4 000 lignes (vs ~70 000 pour OpenVPN)

   INNOVATION PRINCIPALE
   ──────────────────────────────────────────────────────────────
   → Cryptographie moderne, fixe et non négociable :
     ECDH X25519 (échange de clé)
     ChaCha20-Poly1305 (chiffrement + auth)
     BLAKE2s (hash)
     Curve25519 (signatures)

   → Aucune négociation de suite crypto → Moins d'erreurs de config
   → Code minimal → Surface d'attaque réduite → Facilement auditable

   AVANTAGES
   ──────────────────────────────────────────────────────────────
   ✅ Très rapide (2-3× plus rapide qu'OpenVPN, proche de l'overhead nul)
   ✅ Très simple à configurer (quelques lignes)
   ✅ Intégré dans le noyau Linux 5.6+ (pas de dépendance)
   ✅ Reconnexion instantanée (roaming : changer de Wi-Fi → tunnel maintenu)
   ✅ Moderne (ED25519, X25519, ChaCha20)

   INCONVÉNIENTS
   ──────────────────────────────────────────────────────────────
   ❌ UDP uniquement → Bloqué par certains réseaux restrictifs
   ❌ Moins de fonctionnalités (pas de TCP, routage moins flexible)
   ❌ Jeune (moins de recul sur la sécurité à long terme)

   CONFIGURATION WIREGUARD (serveur)
   ──────────────────────────────────────────────────────────────
   # /etc/wireguard/wg0.conf (serveur)
   [Interface]
   Address = 10.8.0.1/24
   ListenPort = 51820
   PrivateKey = <clé privée du serveur>

   [Peer]
   # Client : Alice
   PublicKey = <clé publique d'Alice>
   AllowedIPs = 10.8.0.2/32   # IP allouée à Alice dans le tunnel
   EOF

   # /etc/wireguard/wg0.conf (client Alice)
   [Interface]
   Address = 10.8.0.2/24
   PrivateKey = <clé privée d'Alice>
   DNS = 10.8.0.1

   [Peer]
   PublicKey = <clé publique du serveur>
   Endpoint = vpn.entreprise.fr:51820
   AllowedIPs = 10.0.0.0/8   # Tout le réseau interne via VPN
```

---

### IV.D. SSL VPN / VPN Web

```
   SSL VPN (TLS VPN)
   ═══════════════════════════════════════════════════════════════

   Utilise HTTPS/TLS (port 443) → Traverse TOUS les firewalls.
   Peut fonctionner via navigateur web (sans client installé).

   DEUX MODES
   ──────────────────────────────────────────────────────────────
   ① PORTAIL WEB : Accès à des applications via navigateur
     → Intranet, webmail, applications métier
     → Pas de client VPN requis
     → Accès granulaire (par application, pas tout le réseau)

   ② TUNNEL TLS : Client VPN s'installe en extension navigateur
     → Accès au réseau complet
     → Plus transparent pour l'utilisateur

   EXEMPLES
   ──────────────────────────────────────────────────────────────
   → Fortinet FortiGate SSL VPN
   → Cisco AnyConnect (maintenant Cisco Secure Client)
   → Pulse Secure
   → GlobalProtect (Palo Alto)
   → F5 BIG-IP APM
```

---

### IV.E. Tableau Comparatif des Protocoles

```
   COMPARAISON DES PROTOCOLES VPN
   ═══════════════════════════════════════════════════════════════

                 │ IPsec/IKEv2│ OpenVPN   │ WireGuard │ SSL VPN
   ──────────────┼────────────┼───────────┼───────────┼──────────
   Couche réseau │ L3 (IP)    │ L4/L7     │ L3 (IP)   │ L7 (TLS)
   Transport     │ UDP 500/   │ UDP/TCP   │ UDP 51820 │ TCP 443
                 │ 4500       │ 1194/443  │           │
   Vitesse       │ ✅ Rapide  │ ⚠️ Moyen  │ ✅✅ Très │ ⚠️ Moyen
   Traversée FW  │ ❌ Bloqué  │ ✅ 443    │ ⚠️ UDP    │ ✅✅ 443
   Configuration │ ⚠️ Complexe│ ⚠️ Modéré │ ✅ Simple │ ✅ Facile
   Sans client   │ ❌ Non     │ ❌ Non    │ ❌ Non    │ ✅ Oui
   Site-à-site   │ ✅✅ Top   │ ✅ Bon    │ ✅ Bon    │ ❌ Non
   Nomade        │ ✅ Bon     │ ✅✅ Top  │ ✅✅ Top  │ ✅✅ Top
   Open source   │ Standard   │ ✅ GPL    │ ✅ GPL    │ ❌ Souvent
   Maturité      │ 30 ans     │ 20 ans    │ 7 ans     │ Variable
   Recommandé    │ Infra pro  │ Universel │ Moderne   │ Portail web
   ──────────────┴────────────┴───────────┴───────────┴──────────
```

---

## PARTIE V — Architecture VPN d'Entreprise

### V.A. Composants d'une Infrastructure VPN

```
   COMPOSANTS D'UNE INFRASTRUCTURE VPN D'ENTREPRISE
   ═══════════════════════════════════════════════════════════════

   ① CONCENTRATEUR VPN (VPN Gateway / Serveur VPN)
   ──────────────────────────────────────────────────────────────
   → Point de terminaison des tunnels VPN
   → Authentifie les clients (certificats, LDAP, RADIUS)
   → Gère le routage entre les tunnels et le réseau interne
   → Exemples : pfSense, Cisco ASA, FortiGate, Checkpoint, VPS OpenVPN

   ② FIREWALL (souvent couplé au concentrateur)
   ──────────────────────────────────────────────────────────────
   → Filtre le trafic entrant depuis le VPN
   → Applique des règles par utilisateur/groupe
   → Segmentation : Un nomade n'accède pas aux mêmes ressources
     qu'un administrateur

   ③ SERVEUR RADIUS / LDAP (Authentification)
   ──────────────────────────────────────────────────────────────
   → Active Directory → LDAP → Authentification login/MDP
   → FreeRADIUS → Gère l'authentification + autorisation VPN
   → Intégration MFA (Google Authenticator, Duo Security)

   ④ PKI (vu en S13)
   ──────────────────────────────────────────────────────────────
   → Root CA + AC intermédiaire
   → Certificats clients (pour authentification mutuelle)
   → Certificat serveur VPN

   ⑤ CLIENTS VPN
   ──────────────────────────────────────────────────────────────
   → Déployés via GPO (Windows) ou MDM (mobiles)
   → Configurés automatiquement (profil VPN)
   → Exemples : OpenVPN client, WireGuard, GlobalProtect, FortiClient
```

---

### V.B. Architecture VPN Enterprise Complète

```
   ARCHITECTURE VPN ENTERPRISE — VUE D'ENSEMBLE
   ═══════════════════════════════════════════════════════════════

                         INTERNET
   ┌────────────────────────────────────────────────────────────┐
   │                                                            │
   │  ┌─────────┐    VPN nomade        ┌─────────┐             │
   │  │Télétravail│───── TLS ──────────►│         │             │
   │  │ 10.8.0.5 │                     │  ZONE   │             │
   │  └─────────┘                      │   DMZ   │             │
   │                                   │         │             │
   │  ┌─────────┐    VPN nomade        │ Concentr│             │
   │  │Commercial│───── IKEv2 ────────►│ VPN     │◄──────────┐ │
   │  │ 10.8.0.6 │                     │         │           │ │
   │  └─────────┘                      │ Firewall│           │ │
   │                                   └────┬────┘           │ │
   │  ┌─────────┐    VPN Site-à-Site        │                │ │
   │  │Agence   │───── IPsec ──────────────►│                │ │
   │  │Lyon     │                           │                │ │
   │  └─────────┘                           │                │ │
   │                              ┌─────────▼──────────────┐ │ │
   │                              │    RÉSEAU INTERNE       │ │ │
   │                              │  10.0.0.0/16            │ │ │
   │                              │                         │ │ │
   │                              │  AD/LDAP   ERP   Fichie │ │ │
   │                              │  10.0.0.10 .20   .30   │ │ │
   │                              │                         │ │ │
   │                              │  RADIUS          Backup │ │ │
   │                              │  10.0.0.50        .60  │ │ │
   │                              └─────────────────────────┘ │ │
   └────────────────────────────────────────────────────────────┘

   FLUX D'AUTHENTIFICATION NOMADE (OpenVPN + LDAP)
   ──────────────────────────────────────────────────────────────
   1. Client présente son certificat X.509 (ou login/MDP)
   2. Serveur VPN vérifie le certificat (PKI / chaîne de confiance)
   3. Serveur VPN interroge RADIUS → qui interroge Active Directory
   4. Vérification login/MDP + groupe AD (autorisation)
   5. Si MFA configuré : Vérification token TOTP
   6. Tunnel établi : ECDH → Clé de session AES-256
   7. Règles firewall appliquées selon le groupe AD de l'utilisateur
```

---

## VI. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **VPN** | Virtual Private Network — Tunnel chiffré sur réseau public |
| **Tunnelisation** | Encapsulation d'un paquet IP dans un autre paquet IP (chiffré) |
| **Site-à-Site** | Tunnel VPN permanent entre deux réseaux (LAN-to-LAN) |
| **Nomade / Remote Access** | Tunnel VPN à la demande entre un poste individuel et un réseau |
| **Concentrateur VPN** | Équipement terminant les tunnels VPN côté entreprise |
| **IPsec** | Suite de protocoles de sécurité IP (AH, ESP, IKE) — couche réseau |
| **IKEv2** | Internet Key Exchange v2 — protocole d'établissement de tunnel IPsec |
| **OpenVPN** | Solution VPN open source utilisant TLS — très flexible |
| **WireGuard** | Protocole VPN moderne, rapide, code minimal, intégré dans Linux 5.6+ |
| **PSK** | Pre-Shared Key — Clé partagée à l'avance (alternative aux certificats) |
| **tun / tap** | Interfaces réseau virtuelles créées par le client VPN |
| **PFS** | Perfect Forward Secrecy — Clés éphémères : compromission future ≠ déchiffrement passé |
| **SA** | Security Association (IPsec) — Ensemble des paramètres cryptographiques d'un tunnel |
| **RADIUS** | Remote Authentication Dial-In User Service — Authentification centralisée |
| **Split Tunneling** | Technique VPN : Seul le trafic vers le réseau interne passe par le VPN |
| **Full Tunnel** | Tout le trafic (y compris Internet) passe par le VPN |
| **Diffie-Hellman** | Protocole d'échange de clé sur canal non sécurisé (1976) |
| **ECDH** | Version Elliptic Curve de Diffie-Hellman (plus rapide, clés plus courtes) |

---