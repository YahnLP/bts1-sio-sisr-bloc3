---
author: YLP
title: 01 📚 Fiche élève
---

# 📚 FICHE DE COURS ÉLÈVE
## "Hygiène Numérique · 10 Règles Essentielles ANSSI"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 1*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.1** | Identifier les principales menaces de sécurité |
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |

---

## PARTIE I — Qu'est-ce que l'Hygiène Numérique ?

### I.A. Définition

**L'hygiène numérique** est l'ensemble des **bonnes pratiques de sécurité** à adopter au quotidien pour protéger ses données personnelles et professionnelles.

```
   ANALOGIE : HYGIÈNE CORPORELLE vs HYGIÈNE NUMÉRIQUE
   ─────────────────────────────────────────────────────────────

   Hygiène corporelle                Hygiène numérique
   ──────────────────                ─────────────────
   Se laver les mains                Mettre à jour ses logiciels
   Se brosser les dents              Changer ses mots de passe
   Manger sainement                  Éviter les sites douteux
   Faire du sport                    Faire des sauvegardes
   
   → Prévenir les maladies           → Prévenir les cyberattaques
```

**Pourquoi c'est important ?**
- 1 entreprise sur 2 victime d'une cyberattaque chaque année (ANSSI 2023)
- 90% des cyberattaques exploitent le **facteur humain** (erreur, négligence)
- Coût moyen d'une cyberattaque pour une PME : **200 000 €**

---

### I.B. Le Facteur Humain : Maillon Faible de la Sécurité

```
   LA CHAÎNE DE SÉCURITÉ
   ─────────────────────────────────────────────────────────────
   
   Firewall ★★★★★  → 99,9% des attaques bloquées
   Antivirus ★★★★☆ → 95% des malwares détectés
   Chiffrement ★★★★★ → Communications sécurisées
   Sauvegardes ★★★★★ → Données récupérables
   
   MAIS...
   
   Utilisateur qui clique sur un lien malveillant → 100% compromis
   
   ▶ Le facteur humain est le maillon le plus faible
```

**Citation célèbre :**
> *"Il n'y a qu'un seul point d'entrée pour 99% des attaques : l'utilisateur final."* — Kevin Mitnick, ancien hacker devenu consultant en sécurité

---

## PARTIE II — Les 10 Règles d'Hygiène Numérique (ANSSI)

### Règle 1 — Choisir des Mots de Passe Robustes

**Règle :**
Un mot de passe robuste contient :
- **Minimum 12 caractères** (idéal : 16+)
- **Majuscules et minuscules** (A-Z, a-z)
- **Chiffres** (0-9)
- **Caractères spéciaux** (@, #, !, %, etc.)

**Exemples :**

```
❌ MAUVAIS MOTS DE PASSE
─────────────────────────────────────────────────────────────
• azerty         → Trop simple, dans les dictionnaires
• password123    → Prévisible
• 123456         → Cassé en < 1 seconde
• MonPrenom2024  → Trop prévisible (infos publiques)
• motdepasse     → Mot du dictionnaire

✅ BONS MOTS DE PASSE
─────────────────────────────────────────────────────────────
• J'aime3Pomm€s&2Ban@nes! (phrase mnémotechnique)
• Tr0ubl€m@k€r#2024$  (16 caractères, complexe)
• 9Xk$mP2@vL4#Qw7 (généré aléatoirement)
```

**Méthode de création :**
```
MÉTHODE DE LA PHRASE SECRÈTE
─────────────────────────────────────────────────────────────
1. Choisir une phrase que vous retiendrez
   "J'ai 2 chats et 3 poissons rouges à la maison"

2. Prendre les initiales + chiffres + ponctuation
   "J'2c&3pr@lm"

3. Ajouter des majuscules et caractères spéciaux
   "J'2C&3pR@Lm!"

Résultat : Mot de passe robuste de 11 caractères
```

**Gestionnaire de mots de passe recommandé :**
- Bitwarden (open source, gratuit)
- KeePass (local, gratuit)
- 1Password (payant mais pro)

> ⚠️ **JAMAIS** : Réutiliser le même mot de passe sur plusieurs sites !

---

### Règle 2 — Mettre à Jour Régulièrement ses Logiciels

**Pourquoi c'est crucial ?**

Chaque mise à jour corrige des **failles de sécurité** (vulnérabilités).

```
   EXEMPLE : WannaCry (mai 2017)
   ─────────────────────────────────────────────────────────────
   Ransomware qui a infecté 300 000 ordinateurs dans 150 pays
   
   Vulnérabilité exploitée : CVE-2017-0144 (faille Windows SMB)
   
   Microsoft avait publié un patch 2 MOIS AVANT l'attaque
   
   Victimes : Entreprises qui n'avaient PAS fait les mises à jour
   
   → Une simple mise à jour aurait empêché l'infection
```

**Que mettre à jour ?**
- ✅ Système d'exploitation (Windows, Linux, macOS)
- ✅ Navigateur web (Chrome, Firefox, Edge)
- ✅ Logiciels (Office, Adobe, Java, etc.)
- ✅ Antivirus
- ✅ Applications mobiles

**Fréquence :**
- **Critiques** : Immédiatement (failles de sécurité)
- **Normales** : Hebdomadaire (Windows Update le mardi)

---

### Règle 3 — Faire des Sauvegardes Régulières

**Règle des 3-2-1 :**

```
   RÈGLE 3-2-1 DES SAUVEGARDES
   ─────────────────────────────────────────────────────────────
   
   3 copies de vos données
   ├── 1 copie principale (disque dur interne)
   ├── 1 copie locale (disque dur externe)
   └── 1 copie distante (cloud, coffre)
   
   2 supports différents
   ├── Disque dur externe (NAS)
   └── Cloud (Google Drive, OneDrive, Backblaze)
   
   1 copie hors site
   └── Cloud OU disque externe stocké ailleurs (coffre, autre bureau)
```

**Pourquoi ?**
- Ransomware chiffre vos fichiers → restauration depuis sauvegarde
- Panne matérielle → données récupérables
- Suppression accidentelle → récupération possible

**Fréquence recommandée :**
- Données personnelles : **Hebdomadaire**
- Données professionnelles : **Quotidienne** (automatisée)

---

### Règle 4 — Utiliser un Antivirus à Jour

**Rôle de l'antivirus :**
- Détecte et bloque les **malwares** (virus, chevaux de Troie, ransomwares)
- Analyse les fichiers téléchargés
- Surveille les comportements suspects

**Antivirus recommandés :**

| **Antivirus** | **Type** | **Efficacité** | **Prix** |
|---|---|---|---|
| Windows Defender | Intégré Windows | ★★★★☆ | Gratuit |
| Kaspersky | Commercial | ★★★★★ | 30-50 €/an |
| Bitdefender | Commercial | ★★★★★ | 40-60 €/an |
| Avast | Freemium | ★★★☆☆ | Gratuit/payant |

> ⚠️ **Un antivirus ne remplace PAS la vigilance humaine.** Il ne détecte que 95% des menaces connues.

---

### Règle 5 — Éviter les Réseaux Wi-Fi Publics (ou Utiliser un VPN)

**Risques des Wi-Fi publics (café, gare, aéroport) :**
- **Interception** : Un attaquant peut capturer vos données (mots de passe, emails)
- **Faux point d'accès** : L'attaquant crée un faux Wi-Fi "Free WiFi" pour intercepter
- **Man-in-the-Middle** : L'attaquant se place entre vous et le site web

**Solution : VPN (Virtual Private Network)**

```
   SANS VPN                          AVEC VPN
   ────────────────────              ────────────────────
   
   Vous → Wi-Fi → Internet           Vous → Wi-Fi → VPN → Internet
          ↑                                  ↑
   Données visibles                  Données chiffrées
   par l'attaquant                   invisibles
```

**VPN recommandés :**
- ProtonVPN (suisse, open source)
- Mullvad (anonymat renforcé)
- NordVPN (grand public)

---

### Règle 6 — Activer la Double Authentification (2FA)

**Définition :**
La **double authentification** (ou authentification à deux facteurs) ajoute une **deuxième couche de sécurité** après le mot de passe.

```
   CONNEXION CLASSIQUE              CONNEXION AVEC 2FA
   ───────────────────              ──────────────────
   
   1. Mot de passe                  1. Mot de passe
   ✅ Accès autorisé                2. Code à 6 chiffres (SMS/app)
                                    ✅ Accès autorisé
   
   Si un attaquant                  Si un attaquant vole votre
   vole votre mot de passe          mot de passe, il ne peut
   → Il entre facilement            PAS entrer (pas le 2ème facteur)
```

**Types de 2FA :**

| **Type** | **Exemple** | **Sécurité** |
|---|---|---|
| SMS | Code reçu par SMS | ★★☆☆☆ (interception SIM swap) |
| Application | Google Authenticator, Authy | ★★★★☆ |
| Clé physique | YubiKey, Titan Key | ★★★★★ |

**Où activer la 2FA ?**
- ✅ Gmail, Outlook (emails)
- ✅ Banques en ligne
- ✅ Réseaux sociaux (Facebook, Instagram, LinkedIn)
- ✅ Services cloud (Google Drive, Dropbox)

---

### Règle 7 — Séparer Usages Personnels et Professionnels

**Principe :**
- **Email pro** pour le travail uniquement
- **Email perso** pour les achats en ligne, réseaux sociaux, newsletters
- **Ordinateur pro** pour le travail uniquement
- **Ordinateur perso** pour les loisirs

**Pourquoi ?**
- Limite la propagation en cas de compromission
- Respect de la vie privée et du RGPD
- Évite les conflits (données perso sur serveur entreprise)

---

### Règle 8 — Être Vigilant face aux Emails et aux Liens

**Signaux d'alerte d'un email suspect :**

```
✅ EMAIL LÉGITIME                   ❌ EMAIL SUSPECT
────────────────────               ─────────────────
Expéditeur connu                   Expéditeur inconnu ou bizarre
@banque-populaire.fr               @banque-populaire-fr.com
                                   @b4nque-populaire.fr
                                   
Orthographe correcte               Fautes d'orthographe
                                   "Votre compte a été
                                   suspendu. Cliké ici"
                                   
Pas d'urgence                      Urgence artificielle
"Relevé de compte mensuel"         "URGENT : Compte bloqué
                                   sous 24h !"
                                   
Lien vers site officiel            Lien bizarre
https://www.banque-populaire.fr    http://banque-secure.tk
```

> 💡 **Règle d'or :** En cas de doute, NE PAS CLIQUER. Aller directement sur le site officiel (taper l'URL manuellement).

---

### Règle 9 — Chiffrer ses Données Sensibles

**Chiffrement = Rendre illisibles vos données sans la clé**

```
   FICHIER NON CHIFFRÉ              FICHIER CHIFFRÉ
   ───────────────────              ───────────────
   
   Contenu lisible :                Contenu illisible :
   "Numéro CB: 1234 5678            "X8#mK$2@vL4Qw7pN!jR
   9012 3456"                       3Tz&5uI0@eWs..."
   
   Si volé → exploitable            Si volé → inutilisable
                                    (sans la clé de déchiffrement)
```

**Outils de chiffrement :**
- **Fichiers** : VeraCrypt (conteneur chiffré)
- **Disques** : BitLocker (Windows), LUKS (Linux)
- **Communications** : Signal, Telegram (messages)

---

### Règle 10 — Éteindre ou Verrouiller sa Session en Absence

**Risques de laisser sa session ouverte :**
- Accès physique par un tiers malveillant
- Vol de données
- Actions malveillantes en votre nom

**Bonne pratique :**
- **Verrouiller** dès que vous quittez votre poste (même 2 minutes)
- **Raccourci Windows** : `Windows + L`
- **Raccourci Linux** : `Ctrl + Alt + L`
- **Raccourci macOS** : `Ctrl + Cmd + Q`

**En entreprise :** Activer le verrouillage automatique après 5 minutes d'inactivité (GPO).

---
