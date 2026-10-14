---
author: YLP
title: 🖥️ FICHE DE TP
---

# 🖥️ TP — CONSTRUIRE UNE MINI-PKI AVEC OPENSSL

*Durée : 65 minutes — Individuel*

---

## Préparation (3 min)

```bash
# Vérifier OpenSSL
openssl version
# Attendu : OpenSSL 3.x.x

# Créer l'arborescence de travail
mkdir -p ~/pki_tp/{rootca,server,client}
mkdir -p ~/pki_tp/rootca/{certs,private,newcerts,crl}
cd ~/pki_tp
chmod 700 rootca/private/
touch rootca/index.txt
echo 1000 > rootca/serial
echo "Arborescence PKI créée :"
find ~/pki_tp -type d | sort
```

---

## ÉTAPE 1 — Créer la Clé Privée et le Certificat de la Root CA (10 min)

### 1a — Générer la clé privée de la Root CA

```bash
# Générer une clé RSA-4096 pour la Root CA (plus longue = plus sûre pour la racine)
openssl genrsa -aes256 -out rootca/private/rootca.key 4096
# -aes256 : Protège la clé privée avec un mot de passe AES-256
# Entrer un mot de passe mémorable : "RootCA_TP_2024!"

# Vérifier la clé générée
ls -lh rootca/private/rootca.key
openssl rsa -in rootca/private/rootca.key -text -noout | head -10

# La clé est chiffrée avec AES-256 (protégée par mot de passe)
file rootca/private/rootca.key
cat rootca/private/rootca.key | head -3
# Devrait afficher : -----BEGIN ENCRYPTED PRIVATE KEY-----
```

### 1b — Créer le certificat auto-signé Root CA

```bash
# Créer le certificat auto-signé de la Root CA
# Durée : 3650 jours (10 ans) — Normal pour une Root CA
openssl req -new -x509 \
  -key rootca/private/rootca.key \
  -out rootca/certs/rootca.crt \
  -days 3650 \
  -sha256 \
  -subj "/C=FR/ST=Ile-de-France/L=Paris/O=Mon Entreprise Formation/OU=IT Security/CN=Mon Root CA TP/emailAddress=ca@formation.local"

# Explication des options :
# req -new -x509 : Créer un certificat auto-signé (pas une CSR)
# -key            : Clé privée à utiliser
# -out            : Fichier de sortie
# -days 3650      : Validité 10 ans
# -sha256         : Algorithme de hachage pour la signature
# -subj           : Identité de la CA (évite le mode interactif)

# Vérifier le certificat créé
openssl x509 -in rootca/certs/rootca.crt -text -noout
```

---

## ÉTAPE 2 — Inspecter le Certificat Root CA (5 min)

```bash
# Afficher les informations du certificat (version longue)
openssl x509 -in rootca/certs/rootca.crt -text -noout

# Repérer dans la sortie :
# ┌─────────────────────────────────────────────────────────┐
# │ Version: 3 (0x2)                                        │
# │ Serial Number: ... (généré automatiquement)             │
# │ Signature Algorithm: sha256WithRSAEncryption            │
# │ Issuer: C=FR, O=Mon Entreprise, CN=Mon Root CA TP       │
# │   → Issuer = Subject = CERTIFICAT AUTO-SIGNÉ            │
# │ Validity:                                               │
# │   Not Before: ... (aujourd'hui)                         │
# │   Not After:  ... (dans 10 ans)                         │
# │ Subject: C=FR, O=Mon Entreprise, CN=Mon Root CA TP      │
# │ Public Key: rsaEncryption (4096 bit)                    │
# │ X509v3 Basic Constraints:                               │
# │   CA:TRUE  ← Ce certificat EST une CA !                 │
# └─────────────────────────────────────────────────────────┘

# Affichage condensé (juste les infos essentielles)
echo "=== SUBJECT (Titulaire) ==="
openssl x509 -in rootca/certs/rootca.crt -subject -noout

echo "=== ISSUER (Signataire) ==="
openssl x509 -in rootca/certs/rootca.crt -issuer -noout

echo "=== VALIDITÉ ==="
openssl x509 -in rootca/certs/rootca.crt -dates -noout

echo "=== EMPREINTE SHA-256 ==="
openssl x509 -in rootca/certs/rootca.crt -fingerprint -sha256 -noout

echo "=== EST-ELLE UNE CA ? ==="
openssl x509 -in rootca/certs/rootca.crt -text -noout | grep -A1 "Basic Constraints"
```

---

## ÉTAPE 3 — Créer la Clé et la CSR du Serveur Web (10 min)

```bash
cd ~/pki_tp

# Générer la clé privée du serveur (RSA-2048 — standard pour serveur)
# Pas de mot de passe pour le serveur web (sinon nginx/Apache redemande le MDP au démarrage)
openssl genrsa -out server/server.key 2048

# Vérifier
echo "=== CLÉ PRIVÉE SERVEUR ==="
openssl rsa -in server/server.key -text -noout | head -5
cat server/server.key | head -3
# -----BEGIN PRIVATE KEY----- (pas de chiffrement)

# Créer la CSR avec un fichier de configuration (pour les SAN)
cat > server/server.cnf << 'EOF'
[req]
default_bits        = 2048
prompt              = no
default_md          = sha256
distinguished_name  = dn
req_extensions      = req_ext

[dn]
C  = FR
ST = Ile-de-France
L  = Paris
O  = Mon Entreprise Formation
OU = Serveur Web
CN = monserveur.formation.local

[req_ext]
subjectAltName = @alt_names

[alt_names]
DNS.1 = monserveur.formation.local
DNS.2 = www.formation.local
DNS.3 = formation.local
IP.1  = 127.0.0.1
IP.2  = 192.168.1.100
EOF

# Générer la CSR à partir du fichier de config
openssl req -new \
  -key server/server.key \
  -out server/server.csr \
  -config server/server.cnf

# Inspecter la CSR (ce qui sera envoyé à l'AC)
echo "=== CONTENU DE LA CSR ==="
openssl req -in server/server.csr -text -noout

# Vérifier que les SAN sont présents dans la CSR
openssl req -in server/server.csr -text -noout | grep -A5 "Subject Alternative"
```

---

## ÉTAPE 4 — Signer le Certificat Serveur avec la Root CA (10 min)

```bash
cd ~/pki_tp

# Fichier de configuration pour l'extension du certificat signé
cat > rootca/v3_ext.cnf << 'EOF'
[v3_server]
authorityKeyIdentifier = keyid,issuer
basicConstraints       = CA:FALSE
keyUsage               = critical, digitalSignature, keyEncipherment
extendedKeyUsage       = serverAuth
subjectAltName         = @alt_names

[alt_names]
DNS.1 = monserveur.formation.local
DNS.2 = www.formation.local
DNS.3 = formation.local
IP.1  = 127.0.0.1
IP.2  = 192.168.1.100
EOF

# Signer la CSR avec la Root CA → Certificat serveur
openssl x509 -req \
  -in server/server.csr \
  -CA rootca/certs/rootca.crt \
  -CAkey rootca/private/rootca.key \
  -CAcreateserial \
  -out server/server.crt \
  -days 365 \
  -sha256 \
  -extfile rootca/v3_ext.cnf \
  -extensions v3_server
# Entrer le mot de passe de la Root CA : "RootCA_TP_2024!"

# Explication :
# -req           : On signe une CSR
# -in server.csr : La CSR à signer
# -CA / -CAkey   : Le certificat et la clé privée de l'AC signataire
# -CAcreateserial: Génère un numéro de série unique
# -extfile       : Fichier d'extensions (SAN, keyUsage, etc.)
# -extensions    : Quelle section du fichier d'extension utiliser

echo "=== CERTIFICAT SERVEUR SIGNÉ ==="
openssl x509 -in server/server.crt -text -noout
```

---

## ÉTAPE 5 — Inspecter et Vérifier la Chaîne (10 min)

```bash
cd ~/pki_tp

echo "========================================"
echo "=== INSPECTION DU CERTIFICAT SERVEUR ==="
echo "========================================"

echo ""
echo "--- Subject (Titulaire du cert) ---"
openssl x509 -in server/server.crt -subject -noout

echo ""
echo "--- Issuer (Qui l'a signé) ---"
openssl x509 -in server/server.crt -issuer -noout

echo ""
echo "--- Validité ---"
openssl x509 -in server/server.crt -dates -noout

echo ""
echo "--- Subject Alternative Names ---"
openssl x509 -in server/server.crt -text -noout | grep -A10 "Subject Alternative Name"

echo ""
echo "--- Basic Constraints (est-ce une CA ?) ---"
openssl x509 -in server/server.crt -text -noout | grep -A2 "Basic Constraints"
# CA:FALSE → C'est bien un certificat final, pas une CA

echo ""
echo "--- Key Usage ---"
openssl x509 -in server/server.crt -text -noout | grep -A3 "Key Usage"

echo ""
echo "========================================="
echo "=== VÉRIFICATION DE LA CHAÎNE DE CONFIANCE ==="
echo "========================================="

# Vérifier que le certificat serveur est valide selon notre Root CA
openssl verify -CAfile rootca/certs/rootca.crt server/server.crt
# Attendu : server/server.crt: OK ✅

# Vérifier la relation entre la clé et le certificat
echo ""
echo "--- Hash de la clé privée ---"
openssl rsa -noout -modulus -in server/server.key | openssl md5

echo "--- Hash de la clé publique dans le certificat ---"
openssl x509 -noout -modulus -in server/server.crt | openssl md5
# Les 2 hash doivent être IDENTIQUES → Clé et certificat correspondent ✅
```

---

## ÉTAPE 6 — Créer un Certificat Auto-Signé Simple (Comparaison) (7 min)

```bash
cd ~/pki_tp

# Créer un certificat auto-signé en une seule commande (sans CA)
openssl req -new -x509 \
  -newkey rsa:2048 \
  -keyout server/self_signed.key \
  -out server/self_signed.crt \
  -days 365 \
  -sha256 \
  -nodes \
  -subj "/C=FR/O=Test/CN=localhost" \
  -addext "subjectAltName=DNS:localhost,IP:127.0.0.1"
# -nodes : Pas de mot de passe sur la clé privée (pour tests)
# -addext: Ajouter des extensions directement (OpenSSL 3.x)

echo ""
echo "=== COMPARAISON AUTO-SIGNÉ vs SIGNÉ PAR CA ==="
echo ""
echo "--- Certificat AUTO-SIGNÉ ---"
openssl x509 -in server/self_signed.crt -subject -noout
openssl x509 -in server/self_signed.crt -issuer -noout
echo "Subject = Issuer ? (auto-signé = OUI)"

echo ""
echo "--- Certificat SIGNÉ PAR CA ---"
openssl x509 -in server/server.crt -subject -noout
openssl x509 -in server/server.crt -issuer -noout
echo "Subject ≠ Issuer ? (signé par CA = OUI)"

echo ""
echo "=== TENTATIVE DE VÉRIFICATION ==="
echo "Vérifier auto-signé avec notre Root CA :"
openssl verify -CAfile rootca/certs/rootca.crt server/self_signed.crt
# → ERREUR : self signed certificate (attendu ✅)

echo ""
echo "Vérifier certificat serveur avec notre Root CA :"
openssl verify -CAfile rootca/certs/rootca.crt server/server.crt
# → OK ✅
```

---

## ÉTAPE 7 — Formats et Conversions (5 min)

```bash
cd ~/pki_tp

# Format PEM (ce qu'on a créé) — Texte base64
echo "=== FORMAT PEM (ASCII/Base64) ==="
cat server/server.crt | head -5
cat server/server.crt | tail -3
echo "Taille : $(wc -c < server/server.crt) octets"

# Convertir PEM → DER (format binaire)
openssl x509 -in server/server.crt -outform DER -out server/server.der
echo ""
echo "=== FORMAT DER (Binaire) ==="
xxd server/server.der | head -3
echo "Taille : $(wc -c < server/server.der) octets"

# Convertir en PKCS#12 / PFX (format Windows, contient clé + cert + chaîne)
cat server/server.crt rootca/certs/rootca.crt > server/fullchain.crt
openssl pkcs12 -export \
  -inkey server/server.key \
  -in server/server.crt \
  -certfile rootca/certs/rootca.crt \
  -out server/server.p12 \
  -name "Certificat Serveur Formation" \
  -passout pass:Export2024!
echo ""
echo "=== FORMAT PKCS#12 / PFX (Windows) ==="
ls -lh server/server.p12
openssl pkcs12 -info -in server/server.p12 -passin pass:Export2024! -nokeys 2>/dev/null | head -15

echo ""
echo "=== RÉCAPITULATIF DES FICHIERS ==="
ls -lh ~/pki_tp/server/ ~/pki_tp/rootca/certs/ ~/pki_tp/rootca/private/
```

---

## ÉTAPE 8 (BONUS) — Serveur HTTPS avec nginx (10 min)

*Uniquement si nginx est installé*

```bash
# Vérifier nginx
nginx -v 2>/dev/null || echo "nginx non installé — sudo apt install nginx"

# Copier les fichiers dans les répertoires nginx
sudo cp server/server.crt /etc/nginx/ssl/
sudo cp server/server.key /etc/nginx/ssl/
sudo cp rootca/certs/rootca.crt /etc/nginx/ssl/

# Configuration nginx HTTPS minimal
sudo tee /etc/nginx/sites-available/tp-pki << 'NGINX_CONF'
server {
    listen 443 ssl;
    server_name monserveur.formation.local localhost;

    ssl_certificate     /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;

    # Chaîne de confiance (certificats intermédiaires si nécessaire)
    # ssl_trusted_certificate /etc/nginx/ssl/rootca.crt;

    # TLS 1.3 uniquement
    ssl_protocols TLSv1.3;
    ssl_prefer_server_ciphers off;

    # HSTS (forcer HTTPS)
    add_header Strict-Transport-Security "max-age=63072000" always;

    location / {
        return 200 '<html><body>
            <h1>✅ HTTPS fonctionne !</h1>
            <p>Certificat signé par Mon Root CA TP</p>
            <p>TLS 1.3 activé</p>
        </body></html>';
        add_header Content-Type text/html;
    }
}

server {
    listen 80;
    server_name monserveur.formation.local localhost;
    return 301 https://$server_name$request_uri;
}
NGINX_CONF

sudo ln -sf /etc/nginx/sites-available/tp-pki /etc/nginx/sites-enabled/
sudo nginx -t && sudo nginx -s reload

# Tester avec curl en faisant confiance à notre Root CA
curl --cacert rootca/certs/rootca.crt https://localhost/
# → Devrait afficher le HTML sans erreur ✅

# Tester sans faire confiance à notre Root CA
curl https://localhost/ 2>&1 | head -3
# → curl: (60) SSL certificate problem: self-signed certificate in chain ❌
# C'est normal ! Notre Root CA n'est pas dans le trust store système.
```

---

## Questions de Réflexion (À rendre)

```
QUESTIONS DE RÉFLEXION — PKI TP
═══════════════════════════════════════════════════════════════

Q1. Expliquez la différence entre ces 3 fichiers que vous avez créés :
    server.key / server.csr / server.crt
    Lequel ne doit JAMAIS être partagé ? Pourquoi ?
──────────────────────────────────────────────────────────────
    server.key  : ___________________________________________
    server.csr  : ___________________________________________
    server.crt  : ___________________________________________
    Ne jamais partager : ___ car _________________________

Q2. Vous avez créé un certificat SIGNÉ PAR VOTRE Root CA.
    Pourquoi le navigateur Chrome affiche-t-il quand même
    une alerte de sécurité si vous visitez le site ?
    Comment résoudre ce problème en entreprise ?
──────────────────────────────────────────────────────────────
    Raison de l'alerte : ___________________________________
    Solution en entreprise : _______________________________

Q3. Quelle est la différence entre la Root CA que vous avez créée
    et une Root CA comme DigiCert ou Let's Encrypt ?
──────────────────────────────────────────────────────────────
    Différence technique : _________________________________
    Différence pratique  : _________________________________

Q4. Le directeur IT vous demande de créer un certificat pour
    couvrir ces 5 sous-domaines : www.acme.fr, api.acme.fr,
    mail.acme.fr, vpn.acme.fr, intranet.acme.fr
    Deux options : Wildcard *.acme.fr ou certificat multi-domaines SAN.
    Quelle option choisissez-vous et pourquoi ?
──────────────────────────────────────────────────────────────
    Mon choix : ____________________________________________
    Justification : ________________________________________

Q5. Rédigez la commande OpenSSL pour inspecter le certificat
    de n'importe quel site web directement depuis le terminal :
──────────────────────────────────────────────────────────────
    (Indice : openssl s_client + openssl x509)
    Commande : _____________________________________________

═══════════════════════════════════════════════════════════════
CORRIGÉ
═══════════════════════════════════════════════════════════════
Q1 : server.key = Clé PRIVÉE (jamais partagée)
     server.csr = Demande de certificat envoyée à l'AC
     server.crt = Certificat signé par l'AC (partageable)
     Ne jamais partager : server.key — Si volée, n'importe qui peut
     se faire passer pour le serveur (usurpation d'identité)

Q2 : Notre Root CA n'est pas dans le trust store du navigateur
     (Chrome, Firefox ont leurs propres listes d'AC de confiance).
     Solution en entreprise : Déployer le certificat Root CA
     dans le trust store via GPO (Group Policy Object) Active Directory,
     ou via le gestionnaire de certificats de l'OS.

Q3 : Technique : Même technologie (X.509, RSA, SHA-256)
     Pratique : DigiCert/Let's Encrypt sont dans les trust stores
     de tous les navigateurs/OS. Notre CA ne l'est pas.
     → Notre CA = Connue seulement des systèmes où on l'a importée.

Q4 : Les deux fonctionnent mais contextes différents :
     Wildcard *.acme.fr : 1 certificat pour TOUS les sous-domaines
     actuels et futurs → Plus simple à gérer, mais compromis = tous
     les sous-domaines affectés.
     SAN : Contrôle précis des domaines couverts → Plus sécurisé.
     Pour 5 sous-domaines connus : SAN recommandé.
     Si sous-domaines fréquents et dynamiques : Wildcard plus pratique.

Q5 : echo "" | openssl s_client -connect exemple.fr:443 -servername exemple.fr 2>/dev/null | openssl x509 -text -noout
═══════════════════════════════════════════════════════════════
```

---
