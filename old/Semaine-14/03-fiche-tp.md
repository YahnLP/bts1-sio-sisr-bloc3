---
author: YLP
title: 🖥️ FICHE DE TP
---

# 🖥️ TP — ANALYSE VPN ET CRYPTOGRAPHIE ASYMÉTRIQUE

*Durée : 45 minutes — Individuel*

---

## Exercice 1 — Inspecter un Certificat TLS en Direct (10 min)

```bash
# Observer le chiffrement asymétrique en action dans une vraie connexion TLS

# 1. Inspecter le certificat de la CNIL (notre sujet de cours !)
echo "" | openssl s_client \
  -connect www.cnil.fr:443 \
  -servername www.cnil.fr 2>/dev/null | openssl x509 -text -noout

# Questions à répondre :
# a. Qui a émis ce certificat ? (Issuer)
# b. Pour combien de temps est-il valide ?
# c. Quel algorithme de clé publique est utilisé ?
# d. Quels SAN (Subject Alternative Names) sont couverts ?

# 2. Voir la négociation TLS complète
echo "" | openssl s_client \
  -connect www.cnil.fr:443 \
  -servername www.cnil.fr 2>&1 | head -30

# Questions supplémentaires :
# e. Quelle version de TLS est utilisée ?
# f. Quelle suite cryptographique a été négociée ?
#    (Chercher : Cipher is ...)
# g. Quel algorithme d'échange de clé est utilisé ?

# 3. Inspecter plusieurs sites et comparer
for site in google.fr impots.gouv.fr github.com; do
  echo "=== $site ==="
  echo "" | openssl s_client -connect $site:443 -servername $site 2>/dev/null \
    | openssl x509 -noout -issuer -dates -subject
  echo ""
done
```

---

## Exercice 2 — Générer et Utiliser des Clés Asymétriques (15 min)

```bash
mkdir -p ~/tp_asymmetrique && cd ~/tp_asymmetrique

# === PARTIE A : RSA ===
echo "=== PARTIE A : Génération de clés RSA ==="

# Générer une paire de clés RSA-2048
openssl genrsa -out alice_private.pem 2048

# Extraire la clé publique depuis la clé privée
openssl rsa -in alice_private.pem -pubout -out alice_public.pem

# Inspecter les deux clés
echo "--- Clé PRIVÉE (extrait) ---"
cat alice_private.pem | head -3
echo "..."
openssl rsa -in alice_private.pem -text -noout | head -5

echo ""
echo "--- Clé PUBLIQUE ---"
cat alice_public.pem
openssl rsa -in alice_public.pem -pubin -text -noout | head -5

# Taille des fichiers
ls -lh alice_private.pem alice_public.pem

# === PARTIE B : Chiffrement/Déchiffrement RSA ===
echo ""
echo "=== PARTIE B : Chiffrement RSA d'un message court ==="

# Créer un message court (RSA ne chiffre que de petits messages directement)
echo "Clé AES secrète : X7k#P2mQ9vL4nR8s" > message_secret.txt

# Chiffrer avec la CLÉ PUBLIQUE d'Alice
openssl rsautl -encrypt \
  -inkey alice_public.pem \
  -pubin \
  -in message_secret.txt \
  -out message_chiffre.bin

echo "Message original :"
cat message_secret.txt

echo ""
echo "Message chiffré (binaire — illisible) :"
xxd message_chiffre.bin | head -3
echo "Taille : $(wc -c < message_chiffre.bin) octets"

# Déchiffrer avec la CLÉ PRIVÉE d'Alice
openssl rsautl -decrypt \
  -inkey alice_private.pem \
  -in message_chiffre.bin \
  -out message_dechiffre.txt

echo ""
echo "Message déchiffré :"
cat message_dechiffre.txt
diff message_secret.txt message_dechiffre.txt && echo "Identique ✅"

# === PARTIE C : Simulation Chiffrement Hybride ===
echo ""
echo "=== PARTIE C : Simulation Chiffrement Hybride (comme TLS) ==="

# Bob veut envoyer un fichier volumineux à Alice
# Étape 1 : Bob génère une clé AES aléatoire (clé de session)
openssl rand -base64 32 > session_key.txt
echo "Clé AES de session générée :"
cat session_key.txt

# Étape 2 : Bob chiffre la clé AES avec la clé PUBLIQUE d'Alice (RSA)
openssl rsautl -encrypt \
  -inkey alice_public.pem -pubin \
  -in session_key.txt \
  -out session_key_chiffree.bin
echo "Clé AES chiffrée avec RSA (envoyée à Alice)"

# Étape 3 : Bob chiffre ses données volumineuses avec AES
echo "Données volumineuses de Bob : rapport financier, base clients..." > gros_fichier.txt
for i in {1..20}; do echo "Ligne $i : données confidentielles..." >> gros_fichier.txt; done

openssl enc -aes-256-cbc -salt -pbkdf2 \
  -in gros_fichier.txt \
  -out gros_fichier.enc \
  -pass file:session_key.txt

echo "Fichier chiffré avec AES-256 (envoyé à Alice)"
ls -lh gros_fichier.txt gros_fichier.enc

# Étape 4 : Alice déchiffre la clé AES avec sa CLÉ PRIVÉE
openssl rsautl -decrypt \
  -inkey alice_private.pem \
  -in session_key_chiffree.bin \
  -out session_key_restauree.txt

# Étape 5 : Alice déchiffre les données avec la clé AES
openssl enc -aes-256-cbc -d -salt -pbkdf2 \
  -in gros_fichier.enc \
  -out gros_fichier_restaure.txt \
  -pass file:session_key_restauree.txt

echo ""
echo "Fichier restauré par Alice :"
head -3 gros_fichier_restaure.txt
diff gros_fichier.txt gros_fichier_restaure.txt && echo "Chiffrement hybride : Identique ✅"

echo ""
echo "=== RÉSUMÉ CHIFFREMENT HYBRIDE ==="
echo "RSA chiffre : session_key.txt (32 octets) → session_key_chiffree.bin"
echo "AES chiffre : gros_fichier.txt → gros_fichier.enc (données volumineuses)"
echo "→ Sécurité de RSA + Vitesse de AES"
```

---

## Exercice 3 — Analyse VPN (Questions Théoriques) (20 min)

```
ÉTUDE DE CAS — ENTREPRISE MULTISITE CONNECT'PRO
═══════════════════════════════════════════════════════════════

ConnectPro SARL est une PME de 80 salariés avec :
• Siège social à Paris (45 salariés)
  → Réseau : 192.168.10.0/24
  → Serveurs : ERP (192.168.10.100), fichiers (192.168.10.200)

• Agence Marseille (20 salariés permanents)
  → Réseau : 192.168.20.0/24

• 15 commerciaux itinérants (domicile + hôtels + clients)

• 3 développeurs en full télétravail permanent

CONTRAINTES :
• Budget : Limité, utilisation de solutions open source si possible
• Sécurité : Accès ERP = MFA obligatoire
• Réseau Marseille doit accéder à l'ERP Paris en permanence
• Les commerciaux accèdent uniquement au CRM et aux fichiers
• Les développeurs accèdent à tout (y compris serveurs de dev)
═══════════════════════════════════════════════════════════════

QUESTIONS (répondre sur feuille ou fichier texte)
──────────────────────────────────────────────────────────────

Q1. ARCHITECTURE VPN
Combien et quels types de VPN faut-il déployer pour ConnectPro ?
Expliquez le rôle de chacun.
_______________________________________________________________

Q2. CHOIX DE PROTOCOLE
Pour le VPN Site-à-Site Paris ↔ Marseille, quel protocole
recommandez-vous (IPsec, OpenVPN, WireGuard) ?
Justifiez en 3 arguments.
_______________________________________________________________

Q3. AUTHENTIFICATION
Comment authentifier les commerciaux et les développeurs
de façon distincte ? Proposez un mécanisme.
(Pensez aux notions S13 : certificats, et S10 : droits d'accès)
_______________________________________________________________

Q4. SPLIT TUNNELING vs FULL TUNNEL
Pour les commerciaux, recommandez-vous le split tunneling
(seul le trafic vers l'intranet passe par le VPN)
ou le full tunnel (tout le trafic passe par le VPN) ?
Avantages et inconvénients de chaque option ?
_______________________________________________________________

Q5. CRYPTOGRAPHIE DANS LE VPN
Lors de la connexion d'un commercial depuis un hôtel,
décrivez en 4-5 étapes ce qui se passe cryptographiquement
(authentification, échange de clé, chiffrement des données).
Reliez à ce que vous avez appris en S11, S13 et S14.
_______________________________________________________________

Q6. SCHÉMA
Dessinez (ou décrivez textuellement) l'architecture VPN
complète de ConnectPro avec les 3 types d'accès.
_______________________________________________________________
