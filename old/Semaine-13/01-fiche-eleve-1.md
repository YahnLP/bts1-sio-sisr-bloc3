---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Cryptographie Asymétrique · Certificats X.509 · PKI"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 13*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.5** | Mettre en œuvre des mécanismes de chiffrement |
| **B3.6** | Administrer une infrastructure à clés publiques |

---

## PARTIE I — Cryptographie Asymétrique (rappel et approfondissement)

### I.A. Le Principe Clé Publique / Clé Privée

```
   CRYPTOGRAPHIE ASYMÉTRIQUE
   ═══════════════════════════════════════════════════════════════

   DEUX CLÉS MATHÉMATIQUEMENT LIÉES mais fonctionnellement opposées :

   CLÉ PUBLIQUE                     CLÉ PRIVÉE
   ──────────────────────           ──────────────────────────────
   Peut être partagée librement     Doit rester ABSOLUMENT secrète
   Tout le monde peut la voir       Jamais transmise, jamais copiée
   Utilisée pour CHIFFRER           Utilisée pour DÉCHIFFRER
   Utilisée pour VÉRIFIER           Utilisée pour SIGNER

   PROPRIÉTÉ FONDAMENTALE
   ──────────────────────────────────────────────────────────────
   Ce qui est chiffré avec la clé publique
   → Ne peut être déchiffré QUE avec la clé privée correspondante

   Ce qui est signé avec la clé privée
   → Peut être vérifié par n'importe qui avec la clé publique

   ANALOGIE : La boîte aux lettres
   ──────────────────────────────────────────────────────────────
   Clé publique = La fente de la boîte aux lettres
   → Tout le monde peut y déposer un message (chiffrer)

   Clé privée = La clé qui ouvre la boîte
   → Seul le propriétaire peut lire les messages (déchiffrer)
```

---

### I.B. Algorithmes Asymétriques Courants

```
   ALGORITHMES ASYMÉTRIQUES
   ═══════════════════════════════════════════════════════════════

   RSA (Rivest–Shamir–Adleman) — 1977
   ──────────────────────────────────────────────────────────────
   Principe : Difficulté de factoriser de grands nombres
   Tailles de clé : 2048, 3072, 4096 bits (minimum 2048 en 2025)
   Usage : TLS/HTTPS, signatures, emails S/MIME
   Vitesse : Lent (100× plus lent qu'AES)

   ECDSA / ECDH (Elliptic Curve) — 1985, généralisé 2010s
   ──────────────────────────────────────────────────────────────
   Principe : Difficulté du logarithme discret sur courbes elliptiques
   Tailles de clé : 256, 384, 521 bits
   Avantage : Sécurité équivalente à RSA avec clé 10× plus courte
               ECDSA-256 ≈ RSA-3072 en sécurité
   Usage : TLS 1.3 (préféré), Bitcoin, Let's Encrypt
   Vitesse : Beaucoup plus rapide que RSA

   ED25519 (Edwards-curve) — 2011
   ──────────────────────────────────────────────────────────────
   Sécurité et vitesse maximales
   Usage : SSH (clés modernes), GPG, TLS 1.3
   Clé : 256 bits — Le futur des clés asymétriques

   COMPARAISON SÉCURITÉ / TAILLE DE CLÉ
   ──────────────────────────────────────────────────────────────
   RSA-3072     ≡    ECDSA-256    ≡    AES-128   (sécurité équivalente)
   RSA-15360    ≡    ECDSA-521    ≡    AES-256
```

---

### I.C. Signature Numérique

```
   SIGNATURE NUMÉRIQUE — FONCTIONNEMENT
   ═══════════════════════════════════════════════════════════════

   OBJECTIFS : Authenticité + Intégrité + Non-répudiation

   PROCESSUS DE SIGNATURE
   ──────────────────────────────────────────────────────────────

   ÉMETTEUR (Alice — possède la clé privée)
   ─────────────────────────────────────────
   Document original
        │
        ▼
   [Hachage SHA-256]    →   Empreinte du document (256 bits)
        │
        ▼
   [Chiffrement avec    →   Signature numérique
    clé privée Alice]
        │
        ▼
   Document + Signature  ──────────────►  DESTINATAIRE

   VÉRIFICATION (Bob — possède uniquement la clé publique)
   ─────────────────────────────────────────────────────────
   Document + Signature reçus
        │
        ├──────────────────────────────────────────────────────┐
        │                                                      │
   [Hachage SHA-256]                              [Déchiffrement avec
   du document reçu                                clé publique Alice]
        │                                                      │
        ▼                                                      ▼
   Empreinte calculée                          Empreinte de la signature
        │                                                      │
        └─────────────────── COMPARAISON ──────────────────────┘
                                   │
                            Identiques ? ✅ → Document authentique, non modifié
                          Différents ?   ❌ → Document falsifié ou clé incorrecte
```

---

## PARTIE II — Les Certificats Numériques

### II.A. Pourquoi les Certificats ?

```
   LE PROBLÈME QUE LE CERTIFICAT RÉSOUT
   ═══════════════════════════════════════════════════════════════

   SANS CERTIFICAT : L'attaque "Man-in-the-Middle"
   ──────────────────────────────────────────────────────────────

   Alice veut communiquer avec le serveur de sa banque.
   Eve (attaquant) s'intercale :

   Alice ──► "Je veux la clé publique de la banque"
             │
             ▼ (Eve intercepte)
   Eve   ──► Banque : "Donne-moi ta clé publique"
   Eve reçoit la vraie clé publique de la banque
   Eve envoie SA propre clé publique à Alice en se faisant passer pour la banque

   Alice croit communiquer avec la banque
   → Elle chiffre avec la clé d'Eve
   → Eve déchiffre, lit, rechiffre avec la vraie clé de la banque
   → La banque répond normalement
   → Alice ne sait pas qu'Eve a tout vu

   AVEC CERTIFICAT : La solution
   ──────────────────────────────────────────────────────────────

   La banque ne transmet pas seulement sa clé publique.
   Elle transmet un CERTIFICAT contenant :
   → Sa clé publique
   → Son identité (nom de domaine, organisation)
   → La SIGNATURE d'une Autorité de Certification
     qui a vérifié que cette clé appartient bien à cette banque

   Eve ne peut pas falsifier le certificat sans avoir
   la clé privée de l'AC → Impossible en pratique.
```

---

### II.B. Structure d'un Certificat X.509

**X.509 est le standard international des certificats numériques** (RFC 5280).

```
   STRUCTURE D'UN CERTIFICAT X.509 v3
   ═══════════════════════════════════════════════════════════════

   ┌─────────────────────────────────────────────────────────┐
   │               CERTIFICAT X.509 v3                       │
   ├─────────────────────────────────────────────────────────┤
   │ Version : 3                                             │
   │ Numéro de série : 04:7D:E1:A7:... (unique par AC)      │
   ├─────────────────────────────────────────────────────────┤
   │ IDENTITÉ DU TITULAIRE (Subject)                         │
   │   CN (Common Name)    : www.banque.fr                   │
   │   O  (Organization)   : Banque Nationale SA             │
   │   OU (Org. Unit)      : DSI                             │
   │   C  (Country)        : FR                              │
   │   L  (Locality)       : Paris                           │
   ├─────────────────────────────────────────────────────────┤
   │ IDENTITÉ DU SIGNATAIRE (Issuer)                         │
   │   CN : DigiCert TLS RSA SHA256 2020 CA1                 │
   │   O  : DigiCert Inc                                     │
   │   C  : US                                               │
   ├─────────────────────────────────────────────────────────┤
   │ VALIDITÉ                                                │
   │   Not Before : 2024-01-15 00:00:00 UTC                  │
   │   Not After  : 2025-01-14 23:59:59 UTC                  │
   ├─────────────────────────────────────────────────────────┤
   │ CLÉ PUBLIQUE DU TITULAIRE                               │
   │   Algorithme : RSA                                      │
   │   Taille     : 2048 bits                                │
   │   Clé        : 30 82 01 0a 02 82 01 01 00 b3 ... (256o)│
   ├─────────────────────────────────────────────────────────┤
   │ EXTENSIONS (X.509 v3)                                   │
   │   Subject Alternative Names (SAN) :                    │
   │     DNS:www.banque.fr                                   │
   │     DNS:banque.fr                                       │
   │     DNS:m.banque.fr                                     │
   │   Key Usage : Digital Signature, Key Encipherment       │
   │   Extended Key Usage : TLS Web Server Authentication    │
   │   CRL Distribution Points : http://crl.digicert.com/…  │
   │   OCSP : http://ocsp.digicert.com                       │
   │   Basic Constraints : CA:FALSE                          │
   ├─────────────────────────────────────────────────────────┤
   │ SIGNATURE DE L'AC                                       │
   │   Algorithme : SHA256withRSA                            │
   │   Valeur     : 3d a2 f0 8c 4b ... (256 octets)         │
   │   → L'AC a signé l'empreinte de tout ce qui précède    │
   └─────────────────────────────────────────────────────────┘
```

---

### II.C. Les Champs Essentiels X.509

```
   GUIDE DES CHAMPS X.509
   ═══════════════════════════════════════════════════════════════

   SUBJECT (Titulaire du certificat)
   ──────────────────────────────────────────────────────────────
   CN = Common Name
   → Serveur web : Nom de domaine (www.exemple.fr)
   → Certificat CA : Nom de l'autorité ("Ma Root CA")
   → Certificat client : Nom de la personne (Jean Dupont)

   O = Organization → Nom légal de l'organisation
   OU = Organizational Unit → Département (optionnel)
   C = Country → Code pays ISO 2 lettres (FR, US, DE...)
   ST = State/Province → Région
   L = Locality → Ville
   E = Email Address → Email (certificats client)

   ISSUER (Signataire — l'AC)
   ──────────────────────────────────────────────────────────────
   Mêmes champs que le Subject
   Pour un certificat auto-signé : Subject = Issuer

   SERIAL NUMBER
   ──────────────────────────────────────────────────────────────
   Numéro unique attribué par l'AC
   Utilisé pour la révocation (CRL, OCSP)

   VALIDITY PERIOD
   ──────────────────────────────────────────────────────────────
   Not Before : Date d'activation
   Not After  : Date d'expiration
   → Certificats Let's Encrypt : 90 jours (auto-renouvelés)
   → Certificats commerciaux : 1 an maximum (depuis 2020)
   → Certificats internes d'entreprise : Jusqu'à 10 ans possible

   SUBJECT ALTERNATIVE NAMES (SAN) — Extension critique
   ──────────────────────────────────────────────────────────────
   Liste EXHAUSTIVE des domaines couverts par le certificat
   → Obligatoire depuis Chrome 58 (2017) pour la validation
   → Remplace l'ancien champ CN pour la validation des domaines

   Exemples :
   DNS:exemple.fr          → Le domaine principal
   DNS:www.exemple.fr      → Sous-domaine www
   DNS:*.exemple.fr        → Wildcard (tous les sous-domaines)
   IP:192.168.1.1          → Adresse IP (certificats internes)

   BASIC CONSTRAINTS
   ──────────────────────────────────────────────────────────────
   CA:TRUE  → Ce certificat est une autorité de certification
              (peut signer d'autres certificats)
   CA:FALSE → Ce certificat est un certificat final
              (ne peut pas signer d'autres certificats)
```

---

## PARTIE III — La PKI : Infrastructure à Clés Publiques

### III.A. Les Acteurs de la PKI

```
   ACTEURS DE LA PKI
   ═══════════════════════════════════════════════════════════════

   AC RACINE (Root Certificate Authority)
   ──────────────────────────────────────────────────────────────
   Sommet de la hiérarchie de confiance.
   Certificat auto-signé (personne d'autre ne peut la certifier).
   Stockée HORS LIGNE dans un HSM (Hardware Security Module)
   dans une salle sécurisée (vault).

   → Intégrée directement dans les navigateurs et OS
     (Firefox contient ~150 AC racines dans son trust store)

   Exemples : DigiCert Root CA, Let's Encrypt ISRG Root X1,
              Sectigo, GlobalSign, AC gouvernementale française

   AC INTERMÉDIAIRE (Intermediate CA / Subordinate CA)
   ──────────────────────────────────────────────────────────────
   Signée par la Root CA.
   Opérationnelle au quotidien (la Root CA reste hors ligne).
   Signe les certificats finaux (serveurs, clients).

   Pourquoi ? Si l'AC intermédiaire est compromise :
   → On la révoque + On émet une nouvelle AC intermédiaire
   → La Root CA n'est pas compromise
   → Tous les certificats existants sous les autres
     AC intermédiaires restent valides

   ENTITÉ FINALE (End Entity / Leaf Certificate)
   ──────────────────────────────────────────────────────────────
   Certificat du serveur web, d'un client, d'un équipement.
   CA:FALSE (ne peut pas signer d'autres certificats).
   Durée de vie : 90 jours à 1 an.
```

---

### III.B. La Chaîne de Confiance

```
   CHAÎNE DE CONFIANCE (Chain of Trust)
   ═══════════════════════════════════════════════════════════════

   HIÉRARCHIE PKI TYPIQUE
   ──────────────────────────────────────────────────────────────

   ┌─────────────────────────────────┐
   │         ROOT CA                 │  ← Auto-signé, dans le trust store
   │  "DigiCert Global Root CA"      │    du navigateur / OS
   │  Validité : 25 ans              │    Stockée HORS LIGNE
   └──────────────┬──────────────────┘
                  │ Signe
                  ▼
   ┌─────────────────────────────────┐
   │       INTERMEDIATE CA           │  ← Signée par la Root CA
   │  "DigiCert TLS RSA SHA256 CA"   │    Opérationnelle en ligne
   │  Validité : 5-10 ans            │    Signe les certificats finaux
   └──────────────┬──────────────────┘
                  │ Signe
                  ▼
   ┌─────────────────────────────────┐
   │       CERTIFICAT FINAL          │  ← Signé par l'AC intermédiaire
   │  "www.banque.fr"                │    Installé sur le serveur web
   │  Validité : 90 jours à 1 an     │
   └─────────────────────────────────┘

   VALIDATION PAR LE NAVIGATEUR
   ──────────────────────────────────────────────────────────────
   ① Le serveur envoie son certificat FINAL + les INTERMÉDIAIRES
   ② Le navigateur vérifie la signature du certificat final
      par l'AC intermédiaire
   ③ Il vérifie la signature de l'AC intermédiaire par la Root CA
   ④ Il vérifie que la Root CA est dans son trust store
   ⑤ Il vérifie la date de validité à chaque étape
   ⑥ Il vérifie que le CN/SAN correspond au domaine visité
   ⑦ Il vérifie que le certificat n'est pas révoqué (CRL/OCSP)
   → Cadenas ✅ si tout est valide, alerte ❌ sinon
```

---

### III.C. Types de Certificats

```
   TYPES DE CERTIFICATS TLS/HTTPS
   ═══════════════════════════════════════════════════════════════

   DV — Domain Validation (Validation de Domaine)
   ──────────────────────────────────────────────────────────────
   L'AC vérifie UNIQUEMENT que vous contrôlez le domaine
   (via fichier sur le serveur ou enregistrement DNS).
   Délivré en quelques minutes.
   Prix : Gratuit (Let's Encrypt) à ~50€/an.
   Affichage : Cadenas simple 🔒
   Usage : Blog, site perso, API, tout site basique

   OV — Organization Validation (Validation d'Organisation)
   ──────────────────────────────────────────────────────────────
   L'AC vérifie domaine + existence légale de l'organisation
   (extrait Kbis, numéro SIRET, appel téléphonique...).
   Délivré en 1-5 jours.
   Prix : ~100-300€/an.
   Affichage : Cadenas 🔒 (infos org visibles dans le certificat)
   Usage : Sites d'entreprises, portails B2B

   EV — Extended Validation (Validation Étendue)
   ──────────────────────────────────────────────────────────────
   Vérification approfondie (identité légale, localisation, statut).
   Délivré en 1-2 semaines.
   Prix : ~300-1000€/an.
   Affichage : Cadenas 🔒 + Nom de l'organisation visible
   Usage : Banques, e-commerce, administrations

   WILDCARD (Certificat Joker)
   ──────────────────────────────────────────────────────────────
   Couvre un domaine ET tous ses sous-domaines directs.
   CN : *.exemple.fr
   → Valide pour : www.exemple.fr, api.exemple.fr, mail.exemple.fr
   → NON valide pour : sub.api.exemple.fr (sous-domaine de sous-domaine)
   Usage : Entreprise avec beaucoup de sous-domaines

   CERTIFICAT MULTI-DOMAINES (SAN)
   ──────────────────────────────────────────────────────────────
   Un seul certificat pour plusieurs domaines distincts.
   SAN: DNS:exemple.fr, DNS:exemple.com, DNS:exemple.org
   Usage : Sites multilingues, groupes d'entreprises

   CERTIFICAT CLIENT
   ──────────────────────────────────────────────────────────────
   Identifie une PERSONNE ou un APPAREIL (pas un serveur).
   Usage : Authentification forte (VPN, portail d'entreprise),
           signature de documents, messagerie chiffrée (S/MIME)
```

---

### III.D. Cycle de Vie d'un Certificat

```
   CYCLE DE VIE COMPLET
   ═══════════════════════════════════════════════════════════════

   ① GÉNÉRATION DE LA CLÉ PRIVÉE
   ──────────────────────────────────────────────────────────────
   Le titulaire génère une paire de clés (privée + publique).
   La clé PRIVÉE reste chez lui — Ne la transmets jamais !

   ② CRÉATION DE LA CSR (Certificate Signing Request)
   ──────────────────────────────────────────────────────────────
   Demande de certificat contenant :
   → La clé PUBLIQUE
   → Les informations d'identité (CN, O, C...)
   → Signée par la clé PRIVÉE (prouve la possession)

   ③ SOUMISSION À L'AC
   ──────────────────────────────────────────────────────────────
   La CSR est envoyée à l'Autorité de Certification.
   L'AC vérifie l'identité (DV/OV/EV selon le type).

   ④ SIGNATURE PAR L'AC
   ──────────────────────────────────────────────────────────────
   L'AC :
   → Ajoute les métadonnées (numéro de série, validité, extensions)
   → Signe le tout avec sa clé privée
   → Retourne le certificat signé (.crt / .pem)

   ⑤ INSTALLATION ET DÉPLOIEMENT
   ──────────────────────────────────────────────────────────────
   Le certificat + la chaîne d'AC intermédiaires
   sont installés sur le serveur web (nginx, Apache, IIS...).

   ⑥ RENOUVELLEMENT
   ──────────────────────────────────────────────────────────────
   Avant expiration : Nouvelle CSR → Nouveau certificat.
   Let's Encrypt : Renouvellement automatique (Certbot) tous les 90j.

   ⑦ RÉVOCATION (si compromis)
   ──────────────────────────────────────────────────────────────
   Si la clé privée est volée → Révoquer immédiatement.

   CRL (Certificate Revocation List)
   → L'AC publie une liste des numéros de série révoqués
   → Le navigateur télécharge périodiquement la CRL
   → Inconvénient : La liste peut être obsolète

   OCSP (Online Certificate Status Protocol)
   → Le navigateur interroge le serveur OCSP de l'AC en temps réel
   → Réponse immédiate : Valide / Révoqué / Inconnu
   → OCSP Stapling : Le serveur web intègre la réponse OCSP
     dans le TLS handshake (plus rapide, privé)
```

---

### III.E. Le Cadenas et la Chaîne Complète TLS

```
   CE QUI SE PASSE QUAND VOUS VISITEZ https://exemple.fr
   ═══════════════════════════════════════════════════════════════

   1. DNS : exemple.fr → 203.0.113.42
   2. TCP : Connexion sur port 443
   3. TLS HANDSHAKE :
      → Client Hello : "Je supporte TLS 1.3, voici mes suites crypto"
      → Server Hello : "On utilise TLS 1.3, AES-256-GCM-SHA384"
      → Certificate : Le serveur envoie son certificat + intermédiaires
      → Le CLIENT VÉRIFIE le certificat (chaîne + date + domaine + révoc.)
      → Key Exchange : Diffie-Hellman éphémère (ECDHE)
        → Génération d'une clé de session AES partagée (symétrique)
      → Finished : Canal chiffré AES-256-GCM établi ✅
   4. HTTP dans le tunnel TLS : GET / HTTP/1.1
   5. Cadenas vert dans le navigateur

   DURÉE DU TLS HANDSHAKE : ~50 ms (TLS 1.3, 1 aller-retour)
   DURÉE DU CHIFFREMENT AES : Négligeable (10 Gb/s)

   POURQUOI TLS 1.2 EST DÉPRÉCIÉ (et TLS 1.3 obligatoire)
   ──────────────────────────────────────────────────────────────
   TLS 1.2 : 2 allers-retours pour le handshake (plus lent)
             Supporte des suites crypto faibles (RC4, DES...)
             Vulnérable à des attaques (POODLE, BEAST, DROWN...)
   TLS 1.3 : 1 aller-retour, suites modernes uniquement,
             Perfect Forward Secrecy obligatoire
```

---

## V. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **PKI** | Public Key Infrastructure — Infrastructure gérant les clés publiques et certificats |
| **Certificat X.509** | Standard de certificat numérique (RFC 5280) contenant identité + clé publique + signature AC |
| **Root CA** | Autorité de Certification racine — auto-signée, stockée hors ligne, intégrée dans les trust stores |
| **Intermediate CA** | AC intermédiaire — signée par la Root CA, signe les certificats finaux au quotidien |
| **CSR** | Certificate Signing Request — Demande de certificat contenant clé publique + identité |
| **PEM** | Format texte base64 d'un certificat ou clé (-----BEGIN CERTIFICATE-----) |
| **DER** | Format binaire d'un certificat (équivalent binaire du PEM) |
| **SAN** | Subject Alternative Names — Extension X.509 listant tous les domaines couverts |
| **CN** | Common Name — Nom principal dans le Subject (domaine pour serveur, prénom/nom pour client) |
| **Trust store** | Magasin de certificats des AC racines de confiance du navigateur/OS |
| **CRL** | Certificate Revocation List — Liste des certificats révoqués publiée par l'AC |
| **OCSP** | Online Certificate Status Protocol — Vérification en temps réel de la révocation |
| **TLS Handshake** | Négociation initiale TLS établissant le canal chiffré |
| **DV / OV / EV** | Niveaux de validation : Domaine / Organisation / Étendue |
| **Wildcard** | Certificat *.domaine.fr couvrant tous les sous-domaines directs |
| **Certificat auto-signé** | Certificat signé par sa propre clé privée (pas de tiers de confiance) |
| **HSM** | Hardware Security Module — Matériel dédié à la protection des clés privées des AC |

---
