---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Chiffrement Asymétrique · Diffie-Hellman · Chiffrement Hybride"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 14*

---

## PARTIE I — Chiffrement Asymétrique : Compléments Essentiels

### I.A. Récapitulatif et Positionnement

```
   RÉCAPITULATIF CRYPTOGRAPHIE (S11 + S13 + S14)
   ═══════════════════════════════════════════════════════════════

   SYMÉTRIQUE (S11)          ASYMÉTRIQUE (S13 + S14)
   ──────────────────────    ──────────────────────────────────
   1 clé secrète partagée    2 clés mathématiquement liées
   AES-128/192/256           RSA, ECDSA, ECDH, ED25519
   Très rapide (10 Gb/s)     Lent (100× plus lent)
   Chiffre les données       Échange de clés + signatures
   Problème : comment        Solution : pas besoin de canal
   partager la clé ?         sécurisé préalable

   HYBRIDE (pratique réelle : HTTPS, VPN, SSH, GPG)
   ──────────────────────────────────────────────────────────────
   Asymétrique  → Échanger la clé secrète de session (1 fois)
   Symétrique   → Chiffrer toutes les données (en continu)
   = Sécurité du asymétrique + Vitesse du symétrique
```

---

### I.B. RSA : Fonctionnement Conceptuel

```
   RSA (Rivest–Shamir–Adleman, 1977)
   ═══════════════════════════════════════════════════════════════

   FONDEMENT MATHÉMATIQUE
   ──────────────────────────────────────────────────────────────
   Problème de la factorisation de grands entiers :

   Facile : 17 × 23 = 391         (quelques nanosecondes)
   Difficile : 391 = ? × ?        (chercher les facteurs premiers)

   En pratique :
   p = 7 919 (nombre premier)
   q = 7 907 (nombre premier)
   n = p × q = 62 566 733

   Connaître n = 62 566 733 ET retrouver p et q ?
   → Trivial pour un humain ici, mais avec n de 4096 bits...
   → n = nombre de 1 233 chiffres décimaux
   → Factorisation par tous les ordinateurs de la planète :
     Des milliards d'années.

   GÉNÉRATION DES CLÉS RSA (simplifié)
   ──────────────────────────────────────────────────────────────
   ① Choisir 2 grands nombres premiers p et q (secret)
   ② Calculer n = p × q (partie publique)
   ③ Calculer φ(n) = (p-1)(q-1) (secret)
   ④ Choisir e (exposant public, souvent 65537)
   ⑤ Calculer d tel que e × d ≡ 1 (mod φ(n)) — secret

   → Clé publique  : (n, e)  → Partageable
   → Clé privée    : (n, d)  → Secrète

   CHIFFREMENT / DÉCHIFFREMENT RSA
   ──────────────────────────────────────────────────────────────
   Chiffrer (avec clé publique) :
   c = m^e mod n   (m = message, c = chiffré)

   Déchiffrer (avec clé privée) :
   m = c^d mod n   (retrouve le message original)

   Propriété : Sans connaître d, impossible de retrouver m depuis c.
   Et retrouver d depuis (n, e) nécessite de factoriser n.

   LIMITES DE RSA
   ──────────────────────────────────────────────────────────────
   → Lent (opérations modulaires sur grands entiers)
   → Ne chiffre pas de messages longs directement
      (taille max ≈ taille de la clé - 11 octets)
   → En pratique : RSA chiffre uniquement la CLÉ DE SESSION AES
     puis AES chiffre les données
   → Vulnérable aux ordinateurs quantiques (Shor 1994)
     → Migration vers algorithmes post-quantiques (CRYSTALS-Kyber)
```

---

### I.C. L'Échange de Clé Diffie-Hellman

> **L'invention cryptographique la plus importante du XXe siècle** (Whitfield Diffie et Martin Hellman, 1976).

```
   DIFFIE-HELLMAN : PARTAGER UN SECRET SANS SE RENCONTRER
   ═══════════════════════════════════════════════════════════════

   PROBLÈME : Alice et Bob veulent établir un secret commun
              sur un canal public (Internet) sans se rencontrer
              et sans qu'un observateur (Eve) puisse le trouver.

   ANALOGIE DES COULEURS (conceptuelle)
   ──────────────────────────────────────────────────────────────

   ① Alice et Bob conviennent publiquement d'une couleur de BASE
     (tout le monde peut voir : JAUNE)

   ② Alice choisit secrètement sa couleur : ROUGE
      Elle mélange : JAUNE + ROUGE = ORANGE
      Elle envoie ORANGE à Bob (Eve voit ORANGE)

   ③ Bob choisit secrètement sa couleur : BLEU
      Il mélange : JAUNE + BLEU = VERT
      Il envoie VERT à Alice (Eve voit VERT)

   ④ Alice mélange VERT + son secret ROUGE = MARRON
      Bob mélange ORANGE + son secret BLEU = MARRON (identique !)

      → Alice et Bob ont le même secret : MARRON
      → Eve n'a vu que JAUNE, ORANGE, VERT
      → Eve ne peut pas trouver MARRON sans savoir ROUGE ou BLEU

   EN MATHÉMATIQUES (logarithme discret)
   ──────────────────────────────────────────────────────────────
   Paramètres publics : g = 2, p = 23 (petit pour l'exemple)

   Alice choisit a = 6 (secret)
   Alice calcule : A = g^a mod p = 2^6 mod 23 = 64 mod 23 = 18
   Alice envoie A = 18 à Bob (public)

   Bob choisit b = 15 (secret)
   Bob calcule : B = g^b mod p = 2^15 mod 23 = 32768 mod 23 = 2
   Bob envoie B = 2 à Alice (public)

   Alice calcule : s = B^a mod p = 2^6 mod 23 = 64 mod 23 = 18
                                                     → s = 18

   Bob calcule   : s = A^b mod p = 18^15 mod 23
                                                     → s = 18 ✅

   → Alice et Bob ont obtenu le même secret s = 18 !
   → Eve a vu g=2, p=23, A=18, B=2 mais ne peut pas trouver s=18
     sans résoudre le problème du logarithme discret (facile ici
     car p=23 petit, impossible avec p de 2048 ou 4096 bits)

   ECDH — VERSION SUR COURBES ELLIPTIQUES
   ──────────────────────────────────────────────────────────────
   Même principe, même sécurité, clés 10× plus courtes.
   ECDH-256 ≈ DH-3072 en sécurité.
   → C'est ce qu'utilise TLS 1.3 (ECDHE avec courbe X25519)

   EPHEMERAL (le E dans ECDHE)
   ──────────────────────────────────────────────────────────────
   Chaque connexion TLS génère une NOUVELLE paire de clés DH.
   → Perfect Forward Secrecy (PFS) :
     Si la clé privée du serveur est compromise AUJOURD'HUI,
     les conversations PASSÉES restent protégées.
     (Les clés éphémères sont détruites après chaque session)
   → Obligatoire dans TLS 1.3
```

---

### I.D. Le Chiffrement Hybride en Pratique

```
   CHIFFREMENT HYBRIDE : COMMENT TLS LE FAIT
   ═══════════════════════════════════════════════════════════════

   CONNEXION https://monsite.fr — Détail du TLS 1.3 Handshake
   ──────────────────────────────────────────────────────────────

   CLIENT                                         SERVEUR
   ──────                                         ───────
   1. ClientHello
      → Versions TLS supportées
      → Suites crypto supportées (AES-256-GCM, ChaCha20...)
      → Clé publique ECDHE du client (X25519)
      ─────────────────────────────────────────────────────►

   2.                                         ServerHello
      ◄──────────────────────────────────────────────────────
      ← Suite choisie : TLS_AES_256_GCM_SHA384
      ← Clé publique ECDHE du serveur (X25519)
      ← Certificat du serveur (X.509 — vu S13)
      ← Finished (signé avec la clé privée serveur)

   3. Le client vérifie le certificat (chaîne PKI — S13)

   4. Les deux calculent la même clé de session :
      ECDHE : client_priv × server_pub = secret partagé
      → HKDF (Key Derivation Function) → AES-256-GCM key ✅

   5. Données chiffrées avec AES-256-GCM (symétrique)
      ◄────────────────── Canal AES chiffré ──────────────────►

   ═══════════════════════════════════════════════════════════
   RÉCAPITULATIF DES RÔLES
   ──────────────────────────────────────────────────────────────
   Certificat X.509 (S13) → AUTHENTIFICATION (qui est le serveur ?)
   ECDHE (Diffie-Hellman)  → ÉCHANGE DE CLÉ (secret partagé)
   AES-256-GCM (S11)       → CHIFFREMENT DES DONNÉES (vitesse)
   SHA-384 (HMAC)          → INTÉGRITÉ (données non modifiées)
   ═══════════════════════════════════════════════════════════
```

---

### I.E. Usages Concrets du Chiffrement Asymétrique

```
   OÙ TROUVE-T-ON DE LA CRYPTOGRAPHIE ASYMÉTRIQUE ?
   ═══════════════════════════════════════════════════════════════

   HTTPS / TLS
   ──────────────────────────────────────────────────────────────
   Certificat (RSA/ECDSA) → Authentification serveur
   ECDHE → Échange de clé de session
   AES-GCM → Chiffrement des données HTTP
   Utilisation : Tout site web sécurisé

   SSH (Secure Shell)
   ──────────────────────────────────────────────────────────────
   Clés SSH (RSA-4096 ou ED25519) → Authentification sans MDP
   ECDH → Échange de clé de session
   AES-ChaCha20 → Chiffrement du terminal
   Utilisation : Administration de serveurs à distance

   GPG / PGP
   ──────────────────────────────────────────────────────────────
   Clé publique destinataire → Chiffrement
   Clé privée destinataire → Déchiffrement
   Clé privée émetteur → Signature
   Utilisation : Emails chiffrés, signature de code

   Emails S/MIME
   ──────────────────────────────────────────────────────────────
   Certificat email (client cert) → Signature + chiffrement
   Standard corporatif (Outlook, Thunderbird)

   VPN
   ──────────────────────────────────────────────────────────────
   Certificats (IKEv2/IPsec, OpenVPN) → Authentification tunnel
   DH/ECDH → Échange de clé de session
   AES → Chiffrement du tunnel
   ← C'est la partie VPN que nous allons voir maintenant

   Bitcoin / Crypto-monnaies
   ──────────────────────────────────────────────────────────────
   ECDSA secp256k1 → Signature des transactions
   Clé privée = "accès au portefeuille"
   Adresse Bitcoin = Hash de la clé publique
```

---

