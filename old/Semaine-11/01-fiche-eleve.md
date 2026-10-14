---
author: YLP
title: 📚 FICHE DE COURS
---


# 📚 FICHE DE COURS ÉLÈVE
## "Cryptographie Symétrique · Objectifs · Principe · AES"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 11*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.5** | Mettre en œuvre des mécanismes de chiffrement |

---

## PARTIE I — Cryptographie : Définitions et Objectifs

### I.A. Définitions

```
   VOCABULAIRE FONDAMENTAL
   ═══════════════════════════════════════════════════════════════

   CRYPTOGRAPHIE
   ──────────────────────────────────────────────────────────────
   Science de la protection de l'information par transformation
   mathématique.

   Du grec : kruptos (caché) + graphein (écrire)
   → "L'art d'écrire de manière cachée"

   CHIFFREMENT (Encryption)
   ──────────────────────────────────────────────────────────────
   Transformation d'un message lisible (clair) en message illisible
   (chiffré) à l'aide d'un algorithme et d'une clé.

   Texte clair (plaintext)  + Clé → Texte chiffré (ciphertext)

   DÉCHIFFREMENT (Decryption)
   ──────────────────────────────────────────────────────────────
   Opération inverse : Retrouver le texte clair à partir du
   texte chiffré en utilisant la clé appropriée.

   ⚠️ NE PAS CONFONDRE :
   ──────────────────────────────────────────────────────────────
   CHIFFREMENT   : Transformation avec clé (réversible avec clé)
   HACHAGE       : Empreinte numérique SANS clé (irréversible)
   ENCODAGE      : Représentation alternative (Base64, UTF-8)
                   → PAS de sécurité ! (réversible sans clé)

   Exemples :
   Base64 de "Bonjour" = "Qm9uam91cg==" → Décodable par n'importe qui
   SHA-256 de "Bonjour" = "58bdf..." → Impossible à inverser
   AES-256 de "Bonjour" = "x4Kp..." → Réversible avec la bonne clé
```

---

### I.B. Les 4 Objectifs de la Cryptographie

```
   LES 4 SERVICES DE SÉCURITÉ CRYPTOGRAPHIQUES
   ═══════════════════════════════════════════════════════════════

   ① CONFIDENTIALITÉ
   ──────────────────────────────────────────────────────────────
   Garantir que seules les personnes autorisées peuvent lire
   les données.

   Outil : Chiffrement (AES, RSA...)
   Exemple : Vos messages WhatsApp sont chiffrés de bout en bout
             → Meta/Facebook NE PEUT PAS les lire

   ② INTÉGRITÉ
   ──────────────────────────────────────────────────────────────
   Garantir que les données n'ont pas été modifiées (ni par
   erreur, ni malicieusement).

   Outil : Fonctions de hachage (SHA-256, SHA-3)
   Exemple : Télécharger Ubuntu et vérifier le hash SHA-256
             → Si le hash correspond → Fichier non altéré

   ③ AUTHENTICITÉ (Non-répudiation)
   ──────────────────────────────────────────────────────────────
   Garantir l'identité de l'émetteur et qu'il ne peut pas
   nier avoir envoyé le message.

   Outil : Signature numérique (RSA + Hash)
   Exemple : Un email signé numériquement prouve que c'est
             bien Jean Dupont qui l'a envoyé

   ④ DISPONIBILITÉ
   ──────────────────────────────────────────────────────────────
   Garantir l'accès aux données quand on en a besoin.
   → Lié aux clés : Si la clé est perdue → Données inaccessibles
   → C'est pourquoi la gestion des clés est critique
```

---

## PARTIE II — Le Chiffrement Symétrique

### II.A. Principe Fondamental

```
   CHIFFREMENT SYMÉTRIQUE
   ═══════════════════════════════════════════════════════════════

   DÉFINITION
   ──────────────────────────────────────────────────────────────
   La MÊME clé secrète sert à chiffrer ET à déchiffrer.

   SCHÉMA
   ──────────────────────────────────────────────────────────────

   Alice                               Bob
     │                                   │
     │   Texte clair : "Réunion 14h"     │
     │                                   │
     │   Clé secrète : "X7k#P2mQ"       │
     │         ↓                         │
     │   [AES-256]                       │
     │         ↓                         │
     │   Chiffré : "Kx9pL3vR..."        │
     │                                   │
     │ ══════ Canal non sécurisé ══════► │
     │         (Internet, email...)      │
     │                                   │
     │                             Clé secrète : "X7k#P2mQ"
     │                                   │
     │                             [AES-256 inverse]
     │                                   │
     │                             "Réunion 14h" ✅

   CONDITION : Alice et Bob DOIVENT avoir la même clé
   PROBLÈME : Comment se transmettre la clé de façon sécurisée ?
              → C'est le "problème de l'échange de clé"
              → Résolu par la cryptographie asymétrique (S12)
```

---

### II.B. Chiffrement par Bloc vs Chiffrement par Flux

```
   DEUX FAMILLES DE CHIFFREMENT SYMÉTRIQUE
   ═══════════════════════════════════════════════════════════════

   CHIFFREMENT PAR BLOC (Block Cipher)
   ──────────────────────────────────────────────────────────────
   Principe : Les données sont découpées en blocs de taille fixe,
              chaque bloc est chiffré indépendamment (ou en chaîne).

   Taille de bloc typique : 128 bits (16 octets)

   Exemple : "Bonjour tout le monde !"
   → Bloc 1 : "Bonjour t"   (16 octets)
   → Bloc 2 : "out le mon"  (16 octets)
   → Bloc 3 : "de !"        (4 octets + padding)

   Algorithmes : AES, DES, 3DES, Blowfish
   Usage : Chiffrement fichiers, disques, BDD

   CHIFFREMENT PAR FLUX (Stream Cipher)
   ──────────────────────────────────────────────────────────────
   Principe : Génère un flux pseudo-aléatoire de bits (keystream)
              et les XOR avec les données bit par bit (ou octet par octet).

   Analogie : Un masque unique de la même longueur que le message.

   Algorithmes : RC4 (obsolète), ChaCha20, Salsa20
   Usage : Communications temps réel (TLS, streaming vidéo)

   COMPARAISON
   ──────────────────────────────────────────────────────────────
                    │ Bloc              │ Flux
   ─────────────────┼───────────────────┼────────────────────
   Traitement       │ Par blocs         │ Bit par bit
   Vitesse          │ Un peu plus lent  │ Très rapide
   Erreur           │ Contenue au bloc  │ Peut se propager
   Parallélisable   │ Oui (certains)    │ Non (en général)
   Usage typique    │ Fichiers, BDD     │ Streaming, VoIP
```

---

## PARTIE III — AES : Advanced Encryption Standard

### III.A. Histoire et Adoption

```
   GENÈSE DE L'AES
   ═══════════════════════════════════════════════════════════════

   1977 : DES adopté par le NIST (National Institute of Standards
          and Technology — USA)
          Clé : 56 bits

   1999 : DES cassé en 22h par EFF DES Cracker
          → DES obsolète, 3DES en attendant

   1997 : NIST lance un concours mondial pour DES successor
          → 15 algorithmes candidats de 12 pays différents

   2001 : AES adopté — Algorithme gagnant : RIJNDAEL
          Conçu par Joan Daemen et Vincent Rijmen (Belgique)

   Critères de sélection :
   → Sécurité maximale
   → Efficacité (matériel et logiciel)
   → Simplicité d'implémentation
   → Flexibilité (tailles de clé)

   AUJOURD'HUI (2025)
   ──────────────────────────────────────────────────────────────
   AES est l'algorithme de chiffrement symétrique standard mondial.
   → Milliards d'opérations AES par seconde sur votre smartphone
   → Instructions matérielles dédiées : AES-NI (Intel/AMD depuis 2010)
   → Utilisé partout : HTTPS, VPN, WiFi, stockage, messagerie...
```

---

### III.B. Caractéristiques d'AES

```
   PARAMÈTRES FONDAMENTAUX D'AES
   ═══════════════════════════════════════════════════════════════

   TAILLE DU BLOC : 128 bits (fixe)
   ──────────────────────────────────────────────────────────────
   AES traite TOUJOURS des blocs de 128 bits (16 octets)
   → Quelle que soit la taille de la clé

   TAILLES DE CLÉ : 128, 192 ou 256 bits
   ──────────────────────────────────────────────────────────────
   AES-128 : Clé de 128 bits → 10 tours de transformation
   AES-192 : Clé de 192 bits → 12 tours de transformation
   AES-256 : Clé de 256 bits → 14 tours de transformation

   → Plus la clé est longue, plus il y a de tours → Plus sécurisé
   → AES-128 est déjà considéré sûr pour 2025
   → AES-256 est recommandé pour données ultra-sensibles
     et résistant aux futurs ordinateurs quantiques

   NOMBRE DE COMBINAISONS DE CLÉ
   ──────────────────────────────────────────────────────────────
   AES-128 : 2^128  ≈ 340 000 milliards de milliards de milliards de milliards
   AES-256 : 2^256  ≈ 115 quattuorvigintillions
             (un 1 suivi de 77 zéros)

   Pour casser AES-256 par force brute :
   → Supposons 1 milliard de milliards de milliards de tentatives/s
   → Durée : ≈ 10^44 ans
   → Âge de l'univers : 1,38 × 10^10 ans
   → AES-256 : 10^34 fois l'âge de l'univers → Inattaquable
```

---

### III.C. Fonctionnement d'AES (Conceptuel)

```
   AES — FONCTIONNEMENT CONCEPTUEL
   ═══════════════════════════════════════════════════════════════

   STRUCTURE GÉNÉRALE
   ──────────────────────────────────────────────────────────────
   AES traite un bloc de 128 bits (4×4 octets = matrice d'état)
   et lui applique N tours de 4 transformations successives.

   LA MATRICE D'ÉTAT (State)
   ──────────────────────────────────────────────────────────────
   Le bloc de 128 bits est organisé en matrice 4×4 octets :

   ┌────┬────┬────┬────┐
   │ b0 │ b4 │ b8 │b12 │
   ├────┼────┼────┼────┤
   │ b1 │ b5 │ b9 │b13 │
   ├────┼────┼────┼────┤
   │ b2 │ b6 │b10 │b14 │
   ├────┼────┼────┼────┤
   │ b3 │ b7 │b11 │b15 │
   └────┴────┴────┴────┘

   Les 4 TRANSFORMATIONS par tour :
   ──────────────────────────────────────────────────────────────

   ① SubBytes (Substitution)
   ──────────────────────────────────────────────────────────────
   Chaque octet est remplacé par un autre selon une table de
   substitution (S-Box).

   Analogie : Comme un code secret où chaque lettre est
              remplacée par une autre selon un tableau prédéfini.

   But : Confusion — Rendre la relation clé↔chiffré non linéaire.

   ② ShiftRows (Décalage de lignes)
   ──────────────────────────────────────────────────────────────
   Chaque ligne de la matrice est décalée circulairement :
   • Ligne 0 : Pas de décalage
   • Ligne 1 : Décalage de 1 octet vers la gauche
   • Ligne 2 : Décalage de 2 octets vers la gauche
   • Ligne 3 : Décalage de 3 octets vers la gauche

   But : Diffusion — Mélanger les octets entre les colonnes.

   ③ MixColumns (Mélange de colonnes)
   ──────────────────────────────────────────────────────────────
   Chaque colonne est multipliée par une matrice fixe (algèbre
   de corps de Galois GF(2^8)).

   Analogie : Mélanger les ingrédients d'une recette —
              Chaque élément influence tous les autres.

   But : Diffusion maximale — 1 bit modifié → 128 bits différents.

   ④ AddRoundKey (Ajout de la sous-clé)
   ──────────────────────────────────────────────────────────────
   Le résultat est XORé avec une sous-clé dérivée de la clé
   principale (Key Schedule).

   XOR : 0 XOR 0 = 0 | 0 XOR 1 = 1 | 1 XOR 0 = 1 | 1 XOR 1 = 0

   But : Mélanger les données avec la clé secrète.

   STRUCTURE COMPLÈTE (AES-128 = 10 tours)
   ──────────────────────────────────────────────────────────────

   Données claires
       │
   AddRoundKey (Tour 0)
       │
       ▼
   ┌─────────────────────────────┐  × 9 tours
   │  SubBytes                   │
   │  ShiftRows                  │
   │  MixColumns                 │
   │  AddRoundKey                │
   └─────────────────────────────┘
       │
   ┌─────────────────────────────┐  Tour final (sans MixColumns)
   │  SubBytes                   │
   │  ShiftRows                  │
   │  AddRoundKey                │
   └─────────────────────────────┘
       │
   Données chiffrées ✅
```

---

### III.D. Les Modes Opératoires

**Le problème :** AES chiffre 1 bloc de 128 bits. Mais un fichier fait souvent plusieurs mégaoctets → Des milliers de blocs. Comment enchaîner le chiffrement de ces blocs ?

```
   MODES OPÉRATOIRES D'AES
   ═══════════════════════════════════════════════════════════════

   MODE ECB (Electronic Code Book) — ❌ À NE PAS UTILISER
   ──────────────────────────────────────────────────────────────
   Principe : Chaque bloc chiffré INDÉPENDAMMENT avec la même clé.

   Problème :
   → 2 blocs identiques en clair → 2 blocs IDENTIQUES chiffrés
   → Un attaquant détecte les patterns même sans la clé

   Exemple célèbre : Pingouin Linux chiffré en ECB
   → L'image chiffrée laisse voir la silhouette du pingouin !

   Utilisation : JAMAIS en production.

   MODE CBC (Cipher Block Chaining) — ✅ Standard
   ──────────────────────────────────────────────────────────────
   Principe : Chaque bloc est XORé avec le bloc chiffré précédent
              avant d'être chiffré.

   Bloc 1 clair ──XOR──► [AES] ──► Bloc 1 chiffré
                  ↑                        │
                  IV                       │
                                           ▼
   Bloc 2 clair ──XOR──► [AES] ──► Bloc 2 chiffré
                  ↑
            Bloc 1 chiffré

   IV = Initialization Vector (vecteur d'initialisation, aléatoire)
   → 2 blocs identiques en clair → 2 blocs DIFFÉRENTS chiffrés ✅
   → Si un bloc est corrompu → Les 2 blocs suivants affectés

   Utilisation : Chiffrement fichiers, disques → OpenSSL par défaut

   MODE CTR (Counter) — ✅ Efficace
   ──────────────────────────────────────────────────────────────
   Principe : Chiffre un compteur incrémenté (nonce + counter)
              et XOR avec les données → Transforme AES en flux.

   Avantages :
   → Chiffrement parallélisable (rapide sur multi-cœurs)
   → Erreur contenue (pas de propagation)
   → Pas de padding nécessaire

   Utilisation : TLS, VPN, communications temps réel

   MODE GCM (Galois/Counter Mode) — ✅✅ Recommandé
   ──────────────────────────────────────────────────────────────
   Principe : CTR + Authentification intégrée (MAC)

   Double avantage :
   → Chiffrement (confidentialité)
   → Authentification (intégrité + authenticité)
   → Si les données sont modifiées → Déchiffrement ÉCHOUE

   Utilisation : HTTPS/TLS 1.3 (obligatoire), SSH moderne

   TABLEAU RÉCAPITULATIF
   ──────────────────────────────────────────────────────────────
   Mode │ Sécurité │ Parallèle │ Authenticité │ Usage
   ─────┼──────────┼───────────┼──────────────┼─────────────────
   ECB  │ ❌ Nulle │ ✅ Oui    │ ❌ Non       │ JAMAIS
   CBC  │ ✅ Bonne │ ❌ Non    │ ❌ Non       │ Fichiers (legacy)
   CTR  │ ✅ Bonne │ ✅ Oui    │ ❌ Non       │ Streaming
   GCM  │ ✅✅ Top │ ✅ Oui    │ ✅ Oui       │ TLS 1.3, SSH
```

---

## PARTIE IV — Le Problème de l'Échange de Clé

### IV.A. La Limite Fondamentale du Symétrique

```
   LE PARADOXE DE L'ÉCHANGE DE CLÉ
   ═══════════════════════════════════════════════════════════════

   SCÉNARIO : Alice veut envoyer un fichier chiffré à Bob.
              Ils ne se sont jamais rencontrés.

   ① Alice chiffre le fichier avec la clé "X7k#P2mQ"
   ② Alice envoie le fichier chiffré à Bob par email ✅
      → L'attaquant Eve intercepte → Ne peut pas lire (chiffré ✅)

   ③ Alice doit maintenant envoyer la clé "X7k#P2mQ" à Bob
      → Par email → Eve intercepte la clé ❌
      → Par téléphone → Eve écoute ❌
      → Par courrier → Eve intercepte ❌

   PROBLÈME FONDAMENTAL
   ──────────────────────────────────────────────────────────────
   "Comment partager la clé secrète de façon sécurisée
    sur un canal non sécurisé ?"

   → Ce problème a été RÉSOLU en 1976 par Whitfield Diffie et
     Martin Hellman (échange de clés Diffie-Hellman)
   → Et par la cryptographie ASYMÉTRIQUE (RSA, 1977)
   → Ce sera le sujet de S12

   EN PRATIQUE AUJOURD'HUI (TLS/HTTPS)
   ──────────────────────────────────────────────────────────────
   TLS résout le problème ainsi :
   ① Cryptographie ASYMÉTRIQUE (RSA/ECDH) pour échanger
      une clé de session de façon sécurisée
   ② Cryptographie SYMÉTRIQUE (AES-GCM) pour chiffrer
      toutes les données (plus rapide)

   → Asymétrique pour l'échange de clé (lent mais sécurisé)
   → Symétrique pour les données (rapide)
   → C'est le meilleur des deux mondes

   POURQUOI SYMÉTRIQUE POUR LES DONNÉES ?
   ──────────────────────────────────────────────────────────────
   AES-256 : 10 Gb/s sur matériel moderne (avec AES-NI)
   RSA-2048 : ~10 Mb/s (100× plus lent)
   → Pour chiffrer 1 To de données :
     AES-256 : ~13 minutes
     RSA :     ~22 heures
```

---

## PARTIE V — Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Cryptographie** | Science de la protection de l'information par transformation mathématique |
| **Chiffrement** | Transformation réversible d'un message avec une clé (≠ hachage irréversible) |
| **Texte clair** | Données originales lisibles (plaintext) |
| **Texte chiffré** | Données après chiffrement, illisibles sans la clé (ciphertext) |
| **Clé symétrique** | Clé unique partagée servant à chiffrer ET déchiffrer |
| **AES** | Advanced Encryption Standard — algorithme de chiffrement symétrique par bloc standard mondial |
| **Bloc** | Unité de traitement d'AES = 128 bits (16 octets) |
| **IV / Nonce** | Valeur aléatoire unique utilisée pour initialiser le chiffrement (Initialization Vector) |
| **Mode ECB** | Mode dangereux — blocs identiques → chiffrés identiques |
| **Mode CBC** | Mode standard — chaînage des blocs, IV requis |
| **Mode GCM** | Mode recommandé — chiffrement + authentification intégrée |
| **Padding** | Données ajoutées pour compléter le dernier bloc à 128 bits |
| **AES-NI** | Instructions matérielles Intel/AMD accélérant AES (x10 à x20) |
| **XOR** | Opération logique bit à bit (0⊕0=0, 0⊕1=1, 1⊕0=1, 1⊕1=0) |
| **Diffie-Hellman** | Protocole d'échange de clé sécurisé sur canal non sécurisé |
| **Problème de l'échange de clé** | Comment partager la clé symétrique de façon sécurisée ? (résolu par crypto asymétrique) |

---
