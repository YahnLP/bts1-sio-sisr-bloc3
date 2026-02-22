---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Mots de Passe Robustes · Science et Bonnes Pratiques"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 3*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.1** | Identifier les principales menaces de sécurité (attaques) |

---

## PARTIE I — L'Entropie (Force Mathématique)

### I.A. Définition

L'**entropie** d'un mot de passe mesure le nombre de **combinaisons possibles** qu'un attaquant doit tester pour le deviner.

```
   FORMULE DE L'ENTROPIE
   ═══════════════════════════════════════════════════════════════
   
   Nombre de combinaisons = Taille de l'alphabet ^ Longueur
   
   Exemples :
   
   ① PIN de 4 chiffres (0-9)
   ──────────────────────────────────────────────────────────────
   Alphabet : 10 chiffres (0, 1, 2... 9)
   Longueur : 4 caractères
   Combinaisons : 10^4 = 10 000 possibilités
   
   ② Mot de passe de 8 minuscules (a-z)
   ──────────────────────────────────────────────────────────────
   Alphabet : 26 lettres
   Longueur : 8 caractères
   Combinaisons : 26^8 = 208 milliards
   
   ③ Mot de passe de 12 caractères (a-Z, 0-9, symboles)
   ──────────────────────────────────────────────────────────────
   Alphabet : 26 + 26 + 10 + 33 = 95 caractères
   Longueur : 12 caractères
   Combinaisons : 95^12 = 5,4 × 10^23 (540 000 Md de Md)
```

---

### I.B. Temps de Craquage

Le temps nécessaire pour craquer un mot de passe dépend de :
1. **Nombre de combinaisons** (entropie)
2. **Vitesse de l'attaquant** (essais par seconde)

```
   PUISSANCE DE CALCUL MODERNE
   ═══════════════════════════════════════════════════════════════
   
   ① PC GRAND PUBLIC (carte graphique RTX 4090)
   ──────────────────────────────────────────────────────────────
   100 milliards de hash MD5 par seconde
   (utilisé pour craquer des mots de passe stockés)
   
   ② SUPERORDINATEUR / BOTNET
   ──────────────────────────────────────────────────────────────
   1 000 milliards d'essais par seconde
   
   ③ SERVICE EN LIGNE (Gmail, Facebook...)
   ──────────────────────────────────────────────────────────────
   10-100 essais par seconde (limitation intentionnelle)
   → Impossible de craquer par brute force directement
```

**Calcul du temps :**

```
Temps = Nombre de combinaisons ÷ Vitesse d'essais

Exemple : Mot de passe "password" (8 minuscules)
─────────────────────────────────────────────────────────────
Combinaisons : 26^8 = 208 milliards
Vitesse : 100 milliards/seconde
Temps : 208 Md ÷ 100 Md/s = 2 secondes

Exemple : Mot de passe "P@ssW0rd!" (9 caractères complexes)
─────────────────────────────────────────────────────────────
Combinaisons : 95^9 = 6,3 × 10^17
Vitesse : 100 milliards/seconde
Temps : 6,3 × 10^17 ÷ 10^11/s = 6,3 millions de secondes
                                = 73 jours
```

---

## PARTIE II — Les Attaques sur Mots de Passe

### II.A. Brute Force (Force Brute)

**Principe :** Tester **toutes les combinaisons possibles** jusqu'à trouver le bon mot de passe.

```
   ATTAQUE BRUTE FORCE
   ═══════════════════════════════════════════════════════════════
   
   ÉTAPE 1 : Essayer "aaaaaaa"
   ÉTAPE 2 : Essayer "aaaaaab"
   ÉTAPE 3 : Essayer "aaaaaac"
   ...
   ÉTAPE N : Essayer "zzzzzzz"
   
   Si le mot de passe est "marmotte" :
   → L'attaquant le trouvera après des milliards d'essais
   
   TEMPS :
   Dépend uniquement de la longueur et de la complexité
   (voir tableau temps de craquage)
```

**Protection :**
- Utiliser des mots de passe longs (16+ caractères)
- Les services en ligne limitent le nombre de tentatives (10 essais → compte bloqué temporairement)

---

### II.B. Attaque par Dictionnaire

**Principe :** Tester des **mots courants** et des **combinaisons prévisibles** au lieu de toutes les combinaisons.

```
   DICTIONNAIRE D'ATTAQUE
   ═══════════════════════════════════════════════════════════════
   
   ① MOTS DU DICTIONNAIRE (français, anglais, espagnol...)
   ──────────────────────────────────────────────────────────────
   password, motdepasse, 123456, admin, root, soleil, dragon...
   
   ② VARIANTES PRÉVISIBLES
   ──────────────────────────────────────────────────────────────
   Password1, P@ssword, p@ssw0rd, Password123!, Motdepasse2024
   
   ③ INFORMATIONS PERSONNELLES
   ──────────────────────────────────────────────────────────────
   prenom+datedenaissance : Sophie1990, Marc2005
   prenom+ville : ParisPierre, ToulouseJulie
   
   ④ MOTS DE PASSE LEAKÉS (bases de données volées)
   ──────────────────────────────────────────────────────────────
   Fichiers de millions de mots de passe réels récupérés
   lors de fuites (LinkedIn, Adobe, Yahoo...)
```

**Liste rockyou.txt :**
- Base de données de **14 millions** de mots de passe réels
- Provient d'une fuite de la société RockYou en 2009
- Utilisée par tous les hackers pour des attaques par dictionnaire

**Top 10 des mots de passe les plus utilisés (2023) :**
```
1. 123456           6. password
2. password         7. 12345678
3. 123456789        8. qwerty
4. 12345            9. 123123
5. qwerty123       10. 1q2w3e4r
```

> ⚠️ **Ces mots de passe sont craqués en < 1 seconde.**

**Protection :**
- Ne JAMAIS utiliser de mots du dictionnaire
- Ne PAS utiliser d'informations personnelles
- Utiliser des phrases de passe aléatoires

---

### II.C. Rainbow Tables (Tables Arc-en-ciel)

**Contexte :** Quand les mots de passe sont **stockés**, ils sont **hachés** (transformés en empreinte).

```
   HASH (Fonction de Hachage)
   ═══════════════════════════════════════════════════════════════
   
   Mot de passe : "password"
   │
   ↓ Fonction de hachage (MD5, SHA-256, bcrypt...)
   │
   Hash : "5f4dcc3b5aa765d61d8327deb882cf99"
   
   Propriétés :
   • Impossible de retrouver "password" à partir du hash
     (fonction à sens unique)
   • Le même mot de passe donne toujours le même hash
   • Un changement minime change complètement le hash
```

**Attaque par Rainbow Table :**

Au lieu de hacher chaque tentative (lent), l'attaquant utilise des **tables pré-calculées** :

```
   RAINBOW TABLE
   ═══════════════════════════════════════════════════════════════
   
   Mot de passe   │ Hash MD5
   ───────────────┼─────────────────────────────────────────────
   password       │ 5f4dcc3b5aa765d61d8327deb882cf99
   123456         │ e10adc3949ba59abbe56e057f20f883e
   qwerty         │ d8578edf8458ce06fbc5bb76a58c5ca4
   admin          │ 21232f297a57a5a743894a0e4a801fc3
   ...            │ ...
   (Millions)     │ (Millions)
```

**Fonctionnement :**
1. L'attaquant récupère un fichier de hash (base de données volée)
2. Il compare chaque hash à sa rainbow table
3. Si match → mot de passe trouvé instantanément

**Protection :**
- **Salting** : Ajouter une chaîne aléatoire unique à chaque mot de passe avant hachage
  ```
  Mot de passe : "password"
  Salt : "x8K$mP2@"
  Hash : SHA-256("passwordx8K$mP2@") = ...différent pour chaque utilisateur
  → Les rainbow tables ne fonctionnent plus
  ```

---

## PARTIE III — Bonnes Pratiques

### III.A. Longueur AVANT Complexité

**Principe démontré :**

```
   COMPARAISON
   ═══════════════════════════════════════════════════════════════
   
   Mot de passe A : "Tr0ubl€@" (8 caractères, très complexe)
   ──────────────────────────────────────────────────────────────
   Temps de craquage : 8 mois
   Facilité à retenir : ★☆☆☆☆ (difficile)
   
   Mot de passe B : "jadore-les-croissants-au-chocolat"
                    (37 caractères, minuscules + tirets uniquement)
   ──────────────────────────────────────────────────────────────
   Temps de craquage : Plusieurs milliards d'années
   Facilité à retenir : ★★★★★ (très facile)
   
   → Mot de passe B est INFINIMENT plus sûr ET plus facile
```

**Recommandations :**
- **Minimum absolu :** 12 caractères
- **Recommandé :** 16+ caractères
- **Idéal :** 20+ caractères (phrase de passe)

---

### III.B. Méthodes de Création

**① PHRASE DE PASSE (Passphrase)**

Utiliser une phrase complète, facile à retenir.

```
✅ BONS EXEMPLES
─────────────────────────────────────────────────────────────
"J'aime manger 3 croissants au chocolat le matin !"
→ 53 caractères, facile à retenir, impossible à craquer

"Mon chat s'appelle Moustache et il a 7 ans"
→ 44 caractères

"Le ciel est bleu, l'herbe est verte, je suis heureux"
→ 53 caractères
```

**② MÉTHODE DICEWARE**

Tirer des mots aléatoires avec des dés (ou générateur).

```
DICEWARE
─────────────────────────────────────────────────────────────
Liste de 7 776 mots (1 à 6 sur 5 dés)

Exemple : Lancer 5 dés = 4-3-6-2-1 → Mot "plage"
          Lancer 5 dés = 2-5-1-4-3 → Mot "orange"
          ...

Résultat : "plage-orange-nuage-piano-soleil-tigre"
→ 6 mots aléatoires, 42 caractères
→ Facile à retenir (visualiser une histoire)
→ Impossible à deviner (aléatoire)
```

**③ GÉNÉRATEUR ALÉATOIRE (Gestionnaire de Mots de Passe)**

Laisser le gestionnaire générer un mot de passe complètement aléatoire.

```
✅ EXEMPLE GÉNÉRÉ PAR BITWARDEN
─────────────────────────────────────────────────────────────
9Xk$mP2@vL4#Qw7!pN3Tz&5uI0

→ 26 caractères aléatoires
→ Impossible à retenir (mais stocké dans le gestionnaire)
→ Impossible à craquer
```

---

### III.C. Unicité ABSOLUE

**Règle d'or :** **1 site = 1 mot de passe unique**

```
   POURQUOI L'UNICITÉ EST CRITIQUE
   ═══════════════════════════════════════════════════════════════
   
   SCÉNARIO : Vous utilisez le même mot de passe partout
   ──────────────────────────────────────────────────────────────
   Email : jean.dupont@gmail.com
   Mot de passe : "MonSuperMDP123!"
   
   Comptes avec ce MDP :
   • Gmail
   • Facebook
   • LinkedIn
   • Site e-commerce XYZ
   • Forum ABC
   
   JANVIER 2024 : Le site e-commerce XYZ est piraté
   ──────────────────────────────────────────────────────────────
   → Base de données volée : 2 millions d'emails + mots de passe
   → Votre email + MDP publié sur le dark web
   
   FÉVRIER 2024 : Des hackers testent les identifiants volés
   ──────────────────────────────────────────────────────────────
   → Ils essaient jean.dupont@gmail.com + MonSuperMDP123!
     sur Gmail → ✅ Succès ! Accès à votre boîte email
   → Ils essaient sur Facebook → ✅ Succès !
   → Ils essaient sur LinkedIn → ✅ Succès !
   → Ils essaient sur PayPal → ✅ Succès !
   
   RÉSULTAT : TOUS VOS COMPTES SONT COMPROMIS
   ──────────────────────────────────────────────────────────────
   À cause d'UNE SEULE fuite sur UN SEUL site
```

**Vérifier si vos comptes ont été compromis :**
- Site : https://haveibeenpwned.com
- Saisir votre email → Voir les fuites connues

**Solution :** Utiliser un gestionnaire de mots de passe qui génère des mots de passe **uniques** pour chaque site.

---

## PARTIE IV — Gestionnaires de Mots de Passe

### IV.A. Pourquoi Utiliser un Gestionnaire ?

**Le problème humain :**
- Impossible de retenir 50+ mots de passe complexes et uniques
- Les utilisateurs réutilisent les mêmes mots de passe (dangereux)
- Ou utilisent des variations prévisibles (Gmail123!, Facebook123!)

**La solution : Gestionnaire de mots de passe**

```
   FONCTIONNEMENT
   ═══════════════════════════════════════════════════════════════
   
   ① VOUS RETENEZ : 1 seul mot de passe maître (très robuste)
   
   ② LE GESTIONNAIRE RETIENT : Tous vos autres mots de passe
   
   ③ AVANTAGES
   ──────────────────────────────────────────────────────────────
   • Génère des mots de passe aléatoires uniques
   • Les stocke de manière chiffrée
   • Auto-remplissage sur les sites web
   • Synchronisation multi-appareils
   • Alerte si un site a été piraté
```

---

### IV.B. Comparatif des Gestionnaires

| **Gestionnaire** | **Type** | **Prix** | **Points forts** | **Inconvénients** |
|---|---|---|---|---|
| **Bitwarden** | Cloud + Auto-hébergeable | Gratuit / 10 $/an | Open source, audité, gratuit complet | Interface moins moderne |
| **1Password** | Cloud | 36 $/an | Interface excellente, support pro | Payant, pas open source |
| **KeePass** | Local (fichier) | Gratuit | 100% local, open source | Pas de synchro cloud native |
| **Dashlane** | Cloud | 60 $/an | Interface moderne, VPN inclus | Cher |
| **LastPass** | Cloud | Gratuit / 36 $/an | Populaire | Failles sécurité passées, gratuit limité |

**Recommandation pour débutants :** **Bitwarden**
- Gratuit et complet
- Open source (code auditable)
- Extension navigateur + app mobile
- Synchronisation automatique
- Générateur de mots de passe intégré

---

### IV.C. Sécurité d'un Gestionnaire

**Question fréquente :** *"Si mon gestionnaire est piraté, tous mes mots de passe sont volés ?"*

**Réponse :** Non, grâce au **chiffrement zero-knowledge**.

```
   CHIFFREMENT ZERO-KNOWLEDGE
   ═══════════════════════════════════════════════════════════════
   
   ① SUR VOTRE APPAREIL
   ──────────────────────────────────────────────────────────────
   Mot de passe maître : "MonPhraseDePasse!"
   │
   ↓ Dérivation de clé (PBKDF2, 100 000 itérations)
   │
   Clé de chiffrement : [256 bits aléatoires]
   │
   ↓ Chiffrement AES-256
   │
   Base de données chiffrée → Envoi au cloud
   
   ② SUR LES SERVEURS BITWARDEN
   ──────────────────────────────────────────────────────────────
   Stockage : Base de données CHIFFRÉE uniquement
   
   ⚠️ Bitwarden NE CONNAÎT PAS votre mot de passe maître
   ⚠️ Bitwarden NE PEUT PAS déchiffrer vos données
   
   ③ SI BITWARDEN EST PIRATÉ
   ──────────────────────────────────────────────────────────────
   Les attaquants récupèrent : Bases de données chiffrées
   Ils NE PEUVENT PAS les déchiffrer (sans votre mot de passe maître)
   
   → Vos mots de passe restent en sécurité
```

**Risque réel :** Si vous **oubliez** votre mot de passe maître → Perte totale (irréversible)

**Solution :** Utiliser une **phrase de passe longue et mémorable**, écrite sur papier et stockée dans un lieu sûr (coffre-fort physique).

---
