---
author: YLP
title: 📄 ANNEXE 1
---

# 📄 ANNEXE 1 — AIDE-MÉMOIRE PKI OPENSSL

```
═══════════════════════════════════════════════════════════════
              AIDE-MÉMOIRE PKI / CERTIFICATS OPENSSL
═══════════════════════════════════════════════════════════════

GÉNÉRATION DE CLÉS
──────────────────────────────────────────────────────────────
# Clé RSA-4096 protégée par mot de passe (CA)
openssl genrsa -aes256 -out ca.key 4096

# Clé RSA-2048 sans mot de passe (serveur)
openssl genrsa -out server.key 2048

# Clé EC ECDSA P-256 (moderne, recommandée)
openssl ecparam -name prime256v1 -genkey -noout -out ec.key

# Clé ED25519 (plus moderne)
openssl genpkey -algorithm ed25519 -out ed25519.key

CERTIFICAT AUTO-SIGNÉ (Root CA ou test)
──────────────────────────────────────────────────────────────
openssl req -new -x509 -key ca.key -out ca.crt -days 3650 \
  -sha256 -subj "/C=FR/O=Mon Org/CN=Mon Root CA"

# Certificat auto-signé en une commande (test rapide)
openssl req -new -x509 -newkey rsa:2048 -keyout test.key \
  -out test.crt -days 365 -nodes \
  -subj "/CN=localhost" \
  -addext "subjectAltName=DNS:localhost,IP:127.0.0.1"

CSR (Certificate Signing Request)
──────────────────────────────────────────────────────────────
openssl req -new -key server.key -out server.csr \
  -subj "/C=FR/O=Mon Org/CN=www.exemple.fr"

SIGNER UNE CSR
──────────────────────────────────────────────────────────────
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key \
  -CAcreateserial -out server.crt -days 365 -sha256 \
  -extfile ext.cnf -extensions v3_server

INSPECTION
──────────────────────────────────────────────────────────────
openssl x509 -in cert.crt -text -noout      # Tout afficher
openssl x509 -in cert.crt -subject -noout   # Titulaire
openssl x509 -in cert.crt -issuer -noout    # Signataire
openssl x509 -in cert.crt -dates -noout     # Validité
openssl req  -in cert.csr -text -noout      # Inspecter une CSR

# Certificat d'un site web en ligne
echo "" | openssl s_client -connect SITE:443 \
  -servername SITE 2>/dev/null | openssl x509 -text -noout

VÉRIFICATION
──────────────────────────────────────────────────────────────
openssl verify -CAfile ca.crt server.crt    # Vérifier chaîne
openssl rsa -noout -modulus -in server.key | openssl md5
openssl x509 -noout -modulus -in server.crt | openssl md5
# → Les 2 hash identiques = clé et cert correspondent

CONVERSIONS DE FORMATS
──────────────────────────────────────────────────────────────
# PEM → DER
openssl x509 -in cert.pem -outform DER -out cert.der

# DER → PEM
openssl x509 -in cert.der -inform DER -out cert.pem

# PEM → PKCS#12/PFX (Windows)
openssl pkcs12 -export -inkey key.pem -in cert.pem \
  -certfile ca.crt -out cert.p12 -passout pass:MonMDP

# PKCS#12 → PEM
openssl pkcs12 -in cert.p12 -out cert.pem -passin pass:MonMDP

═══════════════════════════════════════════════════════════════
EXTENSIONS X.509 IMPORTANTES
──────────────────────────────────────────────────────────────
basicConstraints    = CA:TRUE    → C'est une CA
basicConstraints    = CA:FALSE   → C'est un certificat final
keyUsage            = digitalSignature, keyEncipherment
extendedKeyUsage    = serverAuth   → Authentification serveur TLS
extendedKeyUsage    = clientAuth   → Authentification client TLS
subjectAltName      = DNS:exemple.fr, IP:192.168.1.1
═══════════════════════════════════════════════════════════════
```

---
