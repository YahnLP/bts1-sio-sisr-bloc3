---
author: YLP
title: 📄 ANNEXE
---

# 📄 ANNEXE — AIDE-MÉMOIRE VPN ET CRYPTOGRAPHIE ASYMÉTRIQUE

```
═══════════════════════════════════════════════════════════════
         AIDE-MÉMOIRE S14 — VPN ET CRYPTO ASYMÉTRIQUE
═══════════════════════════════════════════════════════════════

CRYPTOGRAPHIE ASYMÉTRIQUE
──────────────────────────────────────────────────────────────
Clé publique : Partageable → Chiffre / Vérifie signature
Clé privée   : Secrète    → Déchiffre / Signe

RSA : Sécurité = Difficulté de factoriser n = p × q
ECDH: Échange de clé sur courbes elliptiques (plus rapide)
DH  : Échange de clé sans canal sécurisé préalable (1976)
PFS : Perfect Forward Secrecy (clés éphémères)

CHIFFREMENT HYBRIDE (TLS, VPN, SSH, GPG)
──────────────────────────────────────────────────────────────
Asymétrique → Authentification + échange de clé de session
Symétrique  → Chiffrement des données (AES-256-GCM)

COMMANDES OPENSSL ASYMÉTRIQUE
──────────────────────────────────────────────────────────────
# Générer clé RSA-2048
openssl genrsa -out private.pem 2048

# Extraire clé publique
openssl rsa -in private.pem -pubout -out public.pem

# Chiffrer avec clé publique
openssl rsautl -encrypt -inkey public.pem -pubin -in msg.txt -out msg.enc

# Déchiffrer avec clé privée
openssl rsautl -decrypt -inkey private.pem -in msg.enc -out msg.txt

# Inspecter un certificat TLS en ligne
echo "" | openssl s_client -connect site.fr:443 -servername site.fr 2>/dev/null \
  | openssl x509 -text -noout

TYPES DE VPN
──────────────────────────────────────────────────────────────
Site-à-Site : Réseau ↔ Réseau | Permanent | Transparent | IPsec/WG
Nomade      : Poste ↔ Réseau  | À la demande | Client VPN | OpenVPN/WG

PROTOCOLES (COMPARAISON RAPIDE)
──────────────────────────────────────────────────────────────
IPsec/IKEv2  : Standard pro, rapide, UDP 500/4500, Site-à-Site +++
OpenVPN      : Open source, port 443 UDP/TCP, très flexible, universel
WireGuard    : Moderne, ultra-rapide, simple, Linux kernel 5.6+
SSL VPN      : Portail web, port 443, sans client, accès par app

ARCHITECTURE VPN D'ENTREPRISE
──────────────────────────────────────────────────────────────
Internet → Concentrateur VPN (DMZ) → Firewall → Réseau interne
                      ↕
              RADIUS/AD/PKI (authentification)

FLUX AUTH NOMADE : Certificat X.509 → LDAP/AD → MFA → ECDH → AES
═══════════════════════════════════════════════════════════════
```

---
