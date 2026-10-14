---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Authentification Multi-Facteurs (MFA)"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 3*

---

## PARTIE V — Les 3 Facteurs d'Authentification

### V.A. Définition

Un **facteur d'authentification** est un élément utilisé pour **prouver votre identité**.

Il existe **3 catégories** de facteurs :

```
   LES 3 FACTEURS
   ═══════════════════════════════════════════════════════════════
   
   ① CE QUE JE SAIS (Knowledge Factor)
   ──────────────────────────────────────────────────────────────
   Information que vous connaissez :
   • Mot de passe
   • Code PIN
   • Question secrète ("Nom de jeune fille de votre mère ?")
   
   Mnémotechnique : SAvoir
   
   ② CE QUE J'AI (Possession Factor)
   ──────────────────────────────────────────────────────────────
   Objet physique que vous possédez :
   • Téléphone (SMS, app)
   • Clé physique (YubiKey, Titan Key)
   • Carte à puce
   • Badge
   
   Mnémotechnique : Avoir
   
   ③ CE QUE JE SUIS (Inherence Factor)
   ──────────────────────────────────────────────────────────────
   Caractéristique biométrique :
   • Empreinte digitale
   • Reconnaissance faciale (Face ID)
   • Iris / rétine
   • Voix
   
   Mnémotechnique: Être
```

---

### V.B. Authentification Simple vs Multi-Facteurs

```
   AUTHENTIFICATION SIMPLE (1 facteur)
   ═══════════════════════════════════════════════════════════════
   
   Gmail classique :
   1. Email : jean.dupont@gmail.com
   2. Mot de passe : MonMotDePasse123!
   ✅ Accès autorisé
   
   Facteurs : 1 seul (ce que je sais)
   
   RISQUE :
   Si un attaquant connaît votre mot de passe → Il entre
   
   
   AUTHENTIFICATION MULTI-FACTEURS (2+ facteurs)
   ═══════════════════════════════════════════════════════════════
   
   Gmail avec 2FA :
   1. Email : jean.dupont@gmail.com
   2. Mot de passe : MonMotDePasse123!  ← Facteur 1 (ce que je sais)
   3. Code à 6 chiffres (envoyé sur téléphone) ← Facteur 2 (ce que j'ai)
   ✅ Accès autorisé
   
   Facteurs : 2 (ce que je sais + ce que j'ai)
   
   PROTECTION :
   Si un attaquant connaît votre mot de passe MAIS n'a pas votre
   téléphone → Il NE PEUT PAS entrer
```

---

### V.C. 2FA vs MFA

**2FA** = **Two**-Factor Authentication = **Authentification à 2 facteurs**
- Utilise exactement **2 facteurs** différents
- Exemple : Mot de passe + SMS

**MFA** = **Multi**-Factor Authentication = **Authentification multi-facteurs**
- Utilise **2 facteurs ou plus**
- Exemple : Mot de passe + empreinte digitale + code SMS (3 facteurs)

> 📌 **2FA est un sous-ensemble de MFA.** En pratique, le terme "MFA" est souvent utilisé pour désigner la 2FA.

---

## PARTIE VI — Types de Second Facteur

### VI.A. SMS (Code par Texto)

```
FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. Vous saisissez votre mot de passe
2. Le service envoie un code à 6 chiffres par SMS
3. Vous saisissez le code (valide 5 minutes)
4. Accès autorisé

EXEMPLE : "Votre code de connexion : 483 729"

AVANTAGES
─────────────────────────────────────────────────────────────
✅ Simple (tout le monde a un téléphone)
✅ Pas besoin d'application supplémentaire

INCONVÉNIENTS
─────────────────────────────────────────────────────────────
❌ SIM swapping (piratage de carte SIM)
❌ Interception SMS (rare mais possible)
❌ Dépend du réseau mobile (pas de réseau = pas de code)

SÉCURITÉ : ★★☆☆☆ (Mieux que rien, mais vulnérable)
```

---

### VI.B. Application TOTP (Time-based One-Time Password)

**Applications :** Google Authenticator, Authy, Microsoft Authenticator

```
FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. Lors de l'activation de la 2FA :
   • Le service génère un QR code secret
   • Vous scannez le QR code avec l'application
   • Le secret est stocké dans l'application

2. À chaque connexion :
   • L'application génère un code à 6 chiffres
   • Le code change toutes les 30 secondes
   • Vous saisissez le code
   • Accès autorisé

EXEMPLE :
Google Authenticator affiche :
Gmail : 482 739 (15s)
GitHub : 923 481 (22s)
...

AVANTAGES
─────────────────────────────────────────────────────────────
✅ Fonctionne hors ligne (pas besoin de réseau)
✅ Plus sécurisé que SMS (pas d'interception possible)
✅ Gratuit

INCONVÉNIENTS
─────────────────────────────────────────────────────────────
❌ Si vous perdez votre téléphone → Problème d'accès
   (Solution : codes de récupération à sauvegarder)

SÉCURITÉ : ★★★★☆ (Très bien)
```

---

### VI.C. Clé Physique (FIDO2 / U2F)

**Exemples :** YubiKey, Google Titan Key, Thetis

```
FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. Vous branchez la clé USB (ou NFC)
2. Vous saisissez votre mot de passe
3. Vous touchez le bouton sur la clé physique
4. Accès autorisé

La clé contient une puce cryptographique qui prouve votre
identité sans transmettre de secret (protocole FIDO2)

AVANTAGES
─────────────────────────────────────────────────────────────
✅ Résistant au phishing (impossible d'usurper)
✅ Pas de batterie, pas de connexion réseau requise
✅ Très rapide (toucher le bouton)
✅ Peut stocker des dizaines de comptes

INCONVÉNIENTS
─────────────────────────────────────────────────────────────
❌ Coût : 25-60 € par clé
❌ Si vous perdez la clé → Problème d'accès
   (Solution : avoir 2 clés, une de secours)

SÉCURITÉ : ★★★★★ (Maximum)
```

---

### VI.D. Biométrie (Empreinte Digitale, Face ID)

```
FONCTIONNEMENT
─────────────────────────────────────────────────────────────
• Empreinte digitale : Capteur lit l'empreinte
• Face ID (iPhone) : Caméra 3D scanne le visage
• Iris : Caméra scanne l'iris de l'œil

AVANTAGES
─────────────────────────────────────────────────────────────
✅ Très pratique (pas besoin de taper un code)
✅ Difficile à usurper (avec capteurs modernes)
✅ Rapide

INCONVÉNIENTS
─────────────────────────────────────────────────────────────
❌ Problème de confidentialité (données biométriques sensibles)
❌ Irrévocable (si compromis, impossible de "changer" d'empreinte)
❌ Peut être trompé (empreinte 3D, photo haute résolution)
❌ Ne fonctionne pas toujours (doigt mouillé, Face ID avec masque)

SÉCURITÉ : ★★★☆☆ (Bon mais controversé)
```

---

### VI.E. Comparatif Récapitulatif

| **Type** | **Sécurité** | **Praticité** | **Coût** | **Vulnérabilité** | **Recommandation** |
|---|---|---|---|---|---|
| **SMS** | ★★☆☆☆ | ★★★★★ | Gratuit | SIM swapping | ⚠️ Mieux que rien |
| **App TOTP** | ★★★★☆ | ★★★★☆ | Gratuit | Perte téléphone | ✅ Recommandé |
| **Clé physique** | ★★★★★ | ★★★☆☆ | 25-60 € | Perte clé | ✅ Maximum sécurité |
| **Biométrie** | ★★★☆☆ | ★★★★★ | Inclus appareil | Irrévocable | ⚠️ À combiner avec autre |

**Recommandation générale :**
1. **Minimum :** App TOTP (Google Authenticator, Authy)
2. **Idéal :** Clé physique (YubiKey) pour comptes critiques (email, banque)
3. **À éviter seul :** Biométrie (toujours combiner avec mot de passe)

---

## VII. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Entropie** | Mesure du nombre de combinaisons possibles d'un mot de passe |
| **Brute force** | Attaque testant toutes les combinaisons possibles |
| **Attaque par dictionnaire** | Attaque testant des mots courants et combinaisons prévisibles |
| **Rainbow table** | Table pré-calculée de hash pour craquer des mots de passe |
| **Hash** | Empreinte cryptographique d'un mot de passe (fonction à sens unique) |
| **Salt** | Chaîne aléatoire ajoutée au mot de passe avant hachage |
| **Phrase de passe (Passphrase)** | Phrase complète utilisée comme mot de passe (longue et facile à retenir) |
| **Gestionnaire MDP** | Logiciel stockant et générant des mots de passe chiffrés |
| **Zero-knowledge** | Chiffrement où le fournisseur ne peut pas accéder aux données |
| **MFA / 2FA** | Authentification multi-facteurs / à 2 facteurs |
| **TOTP** | Time-based One-Time Password — code temporaire à 6 chiffres |
| **FIDO2** | Standard d'authentification par clé physique |

---
