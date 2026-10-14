---
author: YLP
title: 📄 ANNEXE 1
---

# 📄 ANNEXE 1 — AIDE-MÉMOIRE OPENSSL + GPG

```
═══════════════════════════════════════════════════════════════
          AIDE-MÉMOIRE CRYPTOGRAPHIE EN LIGNE DE COMMANDE
═══════════════════════════════════════════════════════════════

OPENSSL — COMMANDES ESSENTIELLES
──────────────────────────────────────────────────────────────
# Chiffrer un fichier (AES-256-CBC)
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 \
  -in FICHIER_CLAIR -out FICHIER_CHIFFRE \
  -pass pass:MOT_DE_PASSE

# Déchiffrer un fichier
openssl enc -aes-256-cbc -d -pbkdf2 -iter 100000 \
  -in FICHIER_CHIFFRE -out FICHIER_RESTAURE \
  -pass pass:MOT_DE_PASSE

# Hash SHA-256 d'un fichier
openssl dgst -sha256 FICHIER

# Générer un mot de passe aléatoire robuste (32 chars)
openssl rand -base64 32

# Voir les algorithmes disponibles
openssl list -cipher-algorithms

GPG — COMMANDES ESSENTIELLES
──────────────────────────────────────────────────────────────
# Chiffrer symétriquement
gpg --symmetric --cipher-algo AES256 \
  --batch --passphrase "MDP" \
  --output FICHIER.gpg FICHIER_SOURCE

# Déchiffrer
gpg --decrypt --batch --passphrase "MDP" \
  --output FICHIER_RESTAURE FICHIER.gpg

# Chiffrer une archive tar
tar -czf - DOSSIER/ | \
  gpg --symmetric --cipher-algo AES256 \
  --batch --passphrase "MDP" --output ARCHIVE.tar.gz.gpg

# Déchiffrer et extraire l'archive
gpg --decrypt --batch --passphrase "MDP" ARCHIVE.tar.gz.gpg | \
  tar -xzf - -C DESTINATION/

HASH ET INTÉGRITÉ
──────────────────────────────────────────────────────────────
# Calculer SHA-256
sha256sum FICHIER

# Générer un fichier de vérification
sha256sum FICHIER > FICHIER.sha256

# Vérifier l'intégrité
sha256sum -c FICHIER.sha256

SUPPRESSION SÉCURISÉE
──────────────────────────────────────────────────────────────
# Suppression sécurisée (3 passes par défaut)
shred -vuz FICHIER

# Plus de passes (7 = norme DoD américaine)
shred -vuzn 7 FICHIER

═══════════════════════════════════════════════════════════════
```

---

