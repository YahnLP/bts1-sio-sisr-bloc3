---
author: YLP
title: 🖥️ FICHE DE TP
---

# 🖥️ TP — CHIFFREMENT AVEC OPENSSL ET GPG

*Durée : 50 minutes — Individuel*

---

## Prérequis — Vérification des Outils (5 min)

```bash
# Vérifier OpenSSL
openssl version
# Attendu : OpenSSL 3.x.x (ou 1.1.x)

# Vérifier GPG
gpg --version
# Attendu : gpg (GnuPG) 2.x.x

# Si non installés :
# Linux (Debian/Ubuntu) :
sudo apt install openssl gnupg2

# Windows (Git Bash ou WSL) :
# OpenSSL : inclus dans Git for Windows
# GPG : Télécharger Gpg4win https://gpg4win.org
```

---

## ÉTAPE 1 — Créer le Fichier de Test (5 min)

```bash
# Créer un répertoire de travail
mkdir ~/tp_crypto && cd ~/tp_crypto

# Créer un fichier texte de test (données sensibles fictives)
cat > secret.txt << 'EOF'
=== DONNÉES CONFIDENTIELLES — ENTREPRISE INNOTECH ===
Date : 2024-03-15
Auteur : Jean Dupont

PROJET ALPHA — CONFIDENTIEL
Budget alloué : 2 500 000 €
Partenaires : Société X, Société Y
Lancement prévu : Q4 2024

DONNÉES CLIENTS PRIORITAIRES
- Client A : 850 000 €/an — Contact : alice@clientA.fr
- Client B : 1 200 000 €/an — Contact : bob@clientB.fr

MOT DE PASSE SERVEUR DE PROD : (à ne jamais stocker ici en vrai !)
srv-prod-01 : admin / R4nd0mP@ss!2024

NOTE : Ce document est destiné à la direction uniquement.
EOF

# Vérifier le contenu
cat secret.txt

# Vérifier la taille
ls -lh secret.txt
```

---

## ÉTAPE 2 — Hachage SHA-256 (Intégrité) (5 min)

```bash
# Calculer l'empreinte SHA-256 du fichier original
sha256sum secret.txt
# Résultat : [hash en hexadécimal 64 chars]  secret.txt

# Stocker l'empreinte pour vérification ultérieure
sha256sum secret.txt > secret.txt.sha256
cat secret.txt.sha256

# ─── COMPRENDRE ───────────────────────────────────────────────
# SHA-256 génère TOUJOURS une empreinte de 256 bits (64 caractères hex)
# Quelle que soit la taille du fichier en entrée.
# Si 1 seul bit du fichier change → Empreinte COMPLÈTEMENT différente.
# IRRÉVERSIBLE : Impossible de retrouver le fichier depuis l'empreinte.

# Simulation de modification et détection d'altération :
cp secret.txt secret_modifie.txt
echo "Modification malveillante" >> secret_modifie.txt

sha256sum secret.txt
sha256sum secret_modifie.txt
# → Les 2 hashes sont complètement différents !

# Vérification d'intégrité automatique :
sha256sum -c secret.txt.sha256
# Si OK : secret.txt: OK
# Si altéré : secret.txt: FAILED
```

---

## ÉTAPE 3 — Chiffrement avec OpenSSL (AES-256-CBC) (15 min)

### 3a — Chiffrer le fichier

```bash
# CHIFFREMENT AES-256-CBC avec dérivation de clé PBKDF2
openssl enc -aes-256-cbc \
  -salt \
  -pbkdf2 \
  -iter 100000 \
  -in secret.txt \
  -out secret.enc \
  -pass pass:MonMotDePasseSecret2024!

# Explication des options :
# -aes-256-cbc    : Algorithme AES-256 en mode CBC
# -salt           : Ajoute un sel aléatoire (évite attaques par dictionnaire)
# -pbkdf2         : Dérivation de clé PBKDF2 (Password-Based Key Derivation)
# -iter 100000    : 100 000 itérations (ralentit le brute force)
# -in secret.txt  : Fichier source (clair)
# -out secret.enc : Fichier destination (chiffré)
# -pass pass:xxx  : Mot de passe (EN PROD : utiliser -pass file: ou prompt)

# Comparer les tailles
ls -lh secret.txt secret.enc
echo ""
echo "Contenu chiffré (données brutes en base64 pour visualisation) :"
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 \
  -in secret.txt -pass pass:MonMotDePasseSecret2024! | base64 | head -5

# Tenter de lire le fichier chiffré
cat secret.enc
# → Données binaires illisibles ✅
```

### 3b — Vérifier qu'on ne peut pas lire sans la clé

```bash
# Tenter de déchiffrer avec le MAUVAIS mot de passe
openssl enc -aes-256-cbc -d \
  -pbkdf2 \
  -iter 100000 \
  -in secret.enc \
  -out secret_mauvais.txt \
  -pass pass:MauvaisMotDePasse
# → Erreur : "bad decrypt" ou fichier illisible/corrompu ✅

cat secret_mauvais.txt 2>/dev/null || echo "Fichier illisible — Mauvais mot de passe ✅"
```

### 3c — Déchiffrer avec le bon mot de passe

```bash
# DÉCHIFFREMENT
openssl enc -aes-256-cbc -d \
  -pbkdf2 \
  -iter 100000 \
  -in secret.enc \
  -out secret_restaure.txt \
  -pass pass:MonMotDePasseSecret2024!

# Vérifier que le fichier restauré est identique à l'original
cat secret_restaure.txt

# Comparaison automatique (diff)
diff secret.txt secret_restaure.txt
echo "diff retourne : $? (0 = identiques ✅, autre = différences ❌)"

# Vérification par hash
sha256sum secret.txt secret_restaure.txt
# Les 2 hashes doivent être IDENTIQUES
```

### 3d — Analyser ce qui s'est passé "sous le capot"

```bash
# Afficher les informations sur le fichier chiffré
openssl enc -aes-256-cbc -d \
  -pbkdf2 \
  -iter 100000 \
  -in secret.enc \
  -pass pass:MonMotDePasseSecret2024! \
  -P 2>&1 | grep -E "salt|key|iv" || true

# Avec le flag -v (verbose) pour voir les détails
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 \
  -in secret.txt -out secret2.enc \
  -pass pass:MonMotDePasseSecret2024! -v 2>&1

# Remarquer que :
# → salt : aléatoire à chaque chiffrement (même mot de passe → fichiers différents)
# → key : 256 bits dérivés du mot de passe via PBKDF2
# → iv : Initialization Vector, aléatoire

# Preuve : Chiffrer 2 fois le même fichier avec le même MDP
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 \
  -in secret.txt -out secret_copy1.enc \
  -pass pass:MonMotDePasseSecret2024!
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 \
  -in secret.txt -out secret_copy2.enc \
  -pass pass:MonMotDePasseSecret2024!

sha256sum secret_copy1.enc secret_copy2.enc
# → Les 2 hashes sont DIFFÉRENTS (grâce au salt aléatoire) ✅
```

---

## ÉTAPE 4 — Chiffrement avec GPG (Symétrique) (15 min)

### 4a — Chiffrer avec GPG

```bash
# CHIFFREMENT SYMÉTRIQUE GPG (AES-256 par défaut)
gpg --symmetric \
    --cipher-algo AES256 \
    --batch \
    --passphrase "AutreMotDePasseGPG!2024" \
    --output secret.gpg \
    secret.txt

# Options :
# --symmetric      : Chiffrement symétrique (pas de clé publique)
# --cipher-algo    : Algorithme de chiffrement
# --batch          : Mode non-interactif (pas de prompt)
# --passphrase     : Mot de passe
# --output         : Fichier de sortie

# Voir les informations du fichier chiffré
gpg --list-packets secret.gpg 2>/dev/null || gpg --dry-run --decrypt secret.gpg 2>&1 | head -10

# Comparer les tailles
ls -lh secret.txt secret.gpg secret.enc
```

### 4b — Déchiffrer avec GPG

```bash
# DÉCHIFFREMENT
gpg --decrypt \
    --batch \
    --passphrase "AutreMotDePasseGPG!2024" \
    --output secret_gpg_restaure.txt \
    secret.gpg

# Vérifier le résultat
cat secret_gpg_restaure.txt
diff secret.txt secret_gpg_restaure.txt
echo "Résultat diff : $? (0 = identique ✅)"
```

### 4c — Chiffrer un dossier entier avec GPG (tar + gpg)

```bash
# En pratique : on chiffre souvent une archive tar
mkdir -p ~/tp_crypto/dossier_confidentiel
echo "Fichier 1 confidentiel" > ~/tp_crypto/dossier_confidentiel/fichier1.txt
echo "Fichier 2 confidentiel" > ~/tp_crypto/dossier_confidentiel/fichier2.txt

# Créer l'archive tar puis chiffrer en une commande
tar -czf - ~/tp_crypto/dossier_confidentiel/ | \
  gpg --symmetric \
      --cipher-algo AES256 \
      --batch \
      --passphrase "MotDePasseArchive!2024" \
      --output archive_confidentielle.tar.gz.gpg

# Déchiffrer et extraire
gpg --decrypt \
    --batch \
    --passphrase "MotDePasseArchive!2024" \
    archive_confidentielle.tar.gz.gpg | \
  tar -xzf - -C /tmp/

ls /tmp/root/tp_crypto/dossier_confidentiel/ 2>/dev/null || \
ls /tmp/*/tp_crypto/dossier_confidentiel/ 2>/dev/null
```

---

## ÉTAPE 5 — Comparaison et Réflexion (10 min)

```bash
# TABLEAU DE COMPARAISON FINAL
echo "====== COMPARAISON OPENSSL vs GPG ======"
echo ""
echo "Fichier original :"
ls -lh secret.txt

echo ""
echo "Chiffrements :"
ls -lh secret.enc secret.gpg

echo ""
echo "Vérification intégrité des restaurations :"
sha256sum secret.txt secret_restaure.txt secret_gpg_restaure.txt
```

**Répondre aux questions suivantes (sur papier ou dans un fichier notes.txt) :**

```
QUESTIONS DE RÉFLEXION — À RENDRE
═══════════════════════════════════════════════════════════════

Q1. Observez les tailles des fichiers :
    secret.txt   : ______ octets
    secret.enc   : ______ octets
    secret.gpg   : ______ octets

    a) Pourquoi le fichier chiffré est-il légèrement PLUS GRAND ?
    _______________________________________________________________
    (Indice : padding, salt, IV, en-tête)

    b) Peut-on deviner le contenu d'un fichier
       à partir de sa taille chiffrée ?
    _______________________________________________________________

Q2. Vous avez chiffré 2 fois le même fichier avec le même
    mot de passe OpenSSL. Les 2 fichiers chiffrés sont différents.
    Pourquoi ?
    _______________________________________________________________
    (Indice : salt aléatoire, PBKDF2)

Q3. Quel est le maillon FAIBLE dans tout ce système ?
    _______________________________________________________________
    (Indice : Ce n'est pas l'algorithme AES...)

Q4. En entreprise, pour chiffrer une sauvegarde de 500 Go
    stockée sur un NAS externe, quelle commande utiliseriez-vous ?
    Rédigez-la (openssl ou gpg) :
    _______________________________________________________________

Q5. Votre collègue vous envoie un fichier chiffré avec OpenSSL.
    Comment peut-il vous communiquer le mot de passe de façon
    sécurisée ? (Listez 3 méthodes)
    1. ___________________________________________________________
    2. ___________________________________________________________
    3. ___________________________________________________________

---

## ÉTAPE 6 — Nettoyage Sécurisé (5 min)

```bash
# Supprimer de façon sécurisée les fichiers sensibles
# (simple rm ne supprime pas réellement les données sur le disque)

# Linux — Suppression sécurisée avec shred
shred -vuz secret.txt secret_restaure.txt secret_gpg_restaure.txt secret_mauvais.txt 2>/dev/null
# -v : verbose
# -u : supprimer le fichier après écrasement
# -z : écrire des zéros en dernier passage

# Alternative sans shred :
# srm (secure-delete) : apt install secure-delete
# wipe : apt install wipe

# Garder les fichiers chiffrés (c'est le but !)
ls -lh ~/tp_crypto/
echo ""
echo "Fichiers restants (chiffrés uniquement) :"
ls *.enc *.gpg *.sha256 2>/dev/null

# ─── POURQUOI shred ET PAS rm ? ───────────────────────────────
# rm supprime juste la référence (l'entrée dans la table FAT/inode)
# Les données sont TOUJOURS sur le disque jusqu'à être écrasées
# Un outil forensique (Autopsy, Sleuth Kit) peut les récupérer
# shred écrase les données avec des motifs aléatoires (3 passes par défaut)
```

---
