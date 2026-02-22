---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Taxonomie des Malwares · Types et Caractéristiques"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 2*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.1** | Identifier les principales menaces de sécurité |
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |

---

## PARTIE I — Classification des Malwares

### I.A. Définition Générale

**Malware** = **MAL**icious soft**WARE** = Logiciel malveillant.

C'est le **terme générique** qui englobe tous les logiciels conçus pour nuire :
- Voler des données
- Endommager un système
- Prendre le contrôle d'un ordinateur
- Extorquer de l'argent
- Espionner l'utilisateur

```
   MALWARE (terme générique)
   ═══════════════════════════════════════════════════════════════
   
   Sous-catégories :
   ├── Virus          (nécessite un hôte)
   ├── Ver            (autonome, propagation réseau)
   ├── Trojan         (se fait passer pour légitime)
   ├── Ransomware     (chiffre et demande rançon)
   ├── Spyware        (espionne)
   ├── Adware         (publicités)
   ├── Rootkit        (masque sa présence)
   └── Keylogger      (enregistre les touches clavier)
```

---

### I.B. Critères de Classification

Les malwares se distinguent selon 3 critères principaux :

**① MODE DE PROPAGATION**
- Nécessite-t-il une action humaine ? (virus)
- Se propage-t-il automatiquement ? (ver)

**② OBJECTIF**
- Vol de données (spyware)
- Destruction (virus destructeur)
- Extorsion (ransomware)
- Contrôle à distance (trojan/backdoor)

**③ VISIBILITÉ**
- Visible (ransomware affiche un message)
- Furtif (rootkit, spyware)

---

## PARTIE II — Le Virus

### II.A. Définition

Un **virus** est un code malveillant qui :
1. **S'attache à un programme hôte** (fichier .exe, .doc, .pdf)
2. **Nécessite une action humaine** pour s'exécuter (ouvrir le fichier)
3. **Se réplique** en infectant d'autres fichiers

```
   ANALOGIE : VIRUS BIOLOGIQUE
   ═══════════════════════════════════════════════════════════════
   
   Virus informatique           Virus biologique (grippe)
   ──────────────────           ────────────────────────
   S'attache à un fichier       S'attache à une cellule
   Nécessite une action         Nécessite un contact (éternuer)
   (ouvrir le fichier)
   Se réplique dans             Se réplique dans le corps
   d'autres fichiers
   Peut détruire des fichiers   Peut détruire des cellules
```

---

### II.B. Cycle de Vie d'un Virus

```
PHASE 1 — INFECTION
─────────────────────────────────────────────────────────────
L'utilisateur ouvre un fichier infecté
Ex : double-clic sur "photo.jpg.exe"

↓

PHASE 2 — ACTIVATION
─────────────────────────────────────────────────────────────
Le code malveillant s'exécute
Le virus s'installe dans la mémoire

↓

PHASE 3 — RÉPLICATION
─────────────────────────────────────────────────────────────
Le virus cherche d'autres fichiers à infecter
Il s'attache à des .exe, .doc, .xls...

↓

PHASE 4 — PAYLOAD (charge utile)
─────────────────────────────────────────────────────────────
Le virus exécute son action malveillante :
• Suppression de fichiers
• Corruption de données
• Affichage de messages
• Vol d'informations
```

---

### II.C. Exemple : Virus Melissa (1999)

**Le premier virus majeur par email**

```
NOM : Melissa
DATE : Mars 1999
TYPE : Macro virus (infecte documents Word)
VECTEUR : Email avec pièce jointe Word

FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. L'utilisateur reçoit un email :
   Objet : "Message important de [nom d'un ami]"
   Pièce jointe : list.doc

2. L'utilisateur ouvre list.doc
   → Macro malveillante s'active automatiquement

3. Le virus s'envoie aux 50 premiers contacts Outlook
   → Propagation exponentielle (1 → 50 → 2500 → 125 000...)

4. Payload : Insère du texte dans les documents Word

IMPACT
─────────────────────────────────────────────────────────────
• 1 million d'ordinateurs infectés en 3 jours
• Serveurs email saturés (Microsoft, Intel... déconnectés)
• Coût estimé : 80 millions $ (nettoyage + perte productivité)

AUTEUR
─────────────────────────────────────────────────────────────
David L. Smith (New Jersey)
Condamné à 20 mois de prison + 5000 $ d'amende
```

---

## PARTIE III — Le Ver (Worm)

### III.A. Définition

Un **ver** est un malware qui :
1. **Se propage automatiquement** (sans action humaine)
2. **Exploite des failles réseau** pour se répliquer
3. **Est autonome** (pas besoin d'un fichier hôte)

```
   DIFFÉRENCE VIRUS vs VER
   ═══════════════════════════════════════════════════════════════
   
   VIRUS                         VER
   ─────────────────            ────────────────────────
   S'attache à un fichier       Autonome (fichier complet)
   
   Nécessite action humaine     Se propage automatiquement
   (double-clic)                (exploite failles réseau)
   
   Propagation lente            Propagation rapide (minutes)
   (dépend des utilisateurs)    
   
   Exemple : Melissa            Exemple : Conficker
```

---

### III.B. Mode de Propagation

```
PROPAGATION D'UN VER
═══════════════════════════════════════════════════════════════

① EXPLOITATION D'UNE FAILLE
─────────────────────────────────────────────────────────────
Le ver scanne le réseau à la recherche d'ordinateurs
vulnérables (ex : port SMB 445 ouvert, service non patché)

↓

② INFECTION
─────────────────────────────────────────────────────────────
Le ver exploite la faille pour s'installer sur l'ordinateur
cible (sans interaction utilisateur)

↓

③ RÉPLICATION
─────────────────────────────────────────────────────────────
L'ordinateur infecté devient lui-même vecteur
Il scanne et infecte d'autres machines

↓

④ CROISSANCE EXPONENTIELLE
─────────────────────────────────────────────────────────────
1 PC infecté → 10 PC → 100 PC → 1000 PC... (en quelques heures)
```

---

### III.C. Exemple : Ver Conficker (2008)

**L'un des vers les plus répandus de l'histoire**

```
NOM : Conficker (ou Downadup, Kido)
DATE : Novembre 2008 - 2010
TYPE : Ver réseau
VECTEUR : Faille Windows (MS08-067)

FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. Exploite une vulnérabilité Windows (service RPC)
   → Faille corrigée par Microsoft en octobre 2008

2. Se propage automatiquement via :
   • Réseau local (partages Windows)
   • Clés USB
   • Mots de passe faibles (attaque par dictionnaire)

3. Crée un réseau de machines zombies (botnet)
   → 9-15 millions d'ordinateurs infectés

4. Payload : Télécharge d'autres malwares, envoie du spam

IMPACT
─────────────────────────────────────────────────────────────
• 15 millions de PC infectés (estimation)
• Hôpitaux britanniques paralysés (2017 : réinfection)
• Forces armées françaises touchées
• Ministère de la Défense allemand

PROTECTION
─────────────────────────────────────────────────────────────
Installer le patch Microsoft MS08-067 (disponible 1 mois avant)
```

---

## PARTIE IV — Le Trojan (Cheval de Troie)

### IV.A. Définition

Un **trojan** (cheval de Troie) est un malware qui :
1. **Se fait passer pour un logiciel légitime** (faux jeu, faux antivirus, fausse mise à jour)
2. **Trompe l'utilisateur** pour qu'il l'installe volontairement
3. **Ouvre une porte dérobée** (backdoor) pour permettre l'accès à distance

```
   RÉFÉRENCE MYTHOLOGIQUE
   ═══════════════════════════════════════════════════════════════
   
   Cheval de Troie (mythologie grecque)
   
   Les Grecs offrent un grand cheval en bois aux Troyens
   → Les Troyens pensent que c'est un cadeau (apparence légitime)
   → Ils le font entrer dans la ville
   → La nuit, des soldats grecs cachés à l'intérieur sortent
   → Ils ouvrent les portes de la ville (porte dérobée)
   → L'armée grecque envahit Troie
   
   Trojan informatique
   
   Un logiciel se présente comme utile/légitime
   → L'utilisateur l'installe volontairement
   → Une fois installé, le malware s'active
   → Il ouvre un accès distant à l'attaquant
   → L'attaquant prend le contrôle du PC
```

---

### IV.B. Caractéristiques d'un Trojan

**Ne se propage PAS automatiquement :**
- Un trojan n'infecte pas d'autres fichiers (contrairement au virus)
- Il ne se propage pas sur le réseau (contrairement au ver)
- Il compte sur l'utilisateur pour se propager (téléchargement, email)

**Ouvre une backdoor (porte dérobée) :**
```
Une fois installé, le trojan permet à l'attaquant de :
• Prendre le contrôle du PC à distance (RAT - Remote Access Trojan)
• Voler des fichiers
• Enregistrer les touches clavier (keylogger)
• Activer la webcam et le micro
• Installer d'autres malwares (ransomware, spyware)
```

---

### IV.C. Exemple : Emotet (2014-2021)

**Le trojan le plus dangereux de la décennie**

```
NOM : Emotet
DATE : 2014-2021 (démantelé en janvier 2021)
TYPE : Trojan bancaire devenu botnet
VECTEUR : Emails de phishing avec pièces jointes Word malveillantes

FONCTIONNEMENT
─────────────────────────────────────────────────────────────
1. Email de phishing très réaliste :
   Ex : "Re: Facture impayée" (réponse à une conversation réelle)
   Pièce jointe : facture.doc

2. L'utilisateur ouvre le document Word
   → Message : "Activer les macros pour voir le contenu"
   → L'utilisateur active les macros

3. Macro télécharge et exécute Emotet

4. Emotet s'installe et :
   • Vole les contacts Outlook (pour envoyer de nouveaux emails)
   • Télécharge d'autres malwares (TrickBot, Ryuk ransomware)
   • Crée un réseau de PC zombies (botnet)

IMPACT
─────────────────────────────────────────────────────────────
• Qualifié de "malware le plus dangereux" par Europol
• Millions de PC infectés dans le monde
• Utilisé pour déployer des ransomwares (Ryuk → millions $ rançons)
• Ville de Francfort (Allemagne) : 500 000 € de dégâts

DÉMANTÈLEMENT
─────────────────────────────────────────────────────────────
Opération internationale (Europol, FBI, Interpol)
Janvier 2021 : Infrastructure démantelée
Serveurs saisis dans 8 pays
```

---

## PARTIE V — Le Spyware (Logiciel Espion)

### V.A. Définition

Un **spyware** (logiciel espion) est un malware qui :
1. **Espionne** l'utilisateur à son insu
2. **Collecte des données** (mots de passe, historique web, fichiers)
3. **Envoie les données** à l'attaquant

```
   TYPES DE SPYWARES
   ═══════════════════════════════════════════════════════════════
   
   ① KEYLOGGER (enregistreur de frappes)
   ──────────────────────────────────────────────────────────────
   Enregistre tout ce que vous tapez au clavier :
   • Mots de passe
   • Numéros de carte bancaire
   • Messages privés
   
   ② ADWARE (publiciel)
   ──────────────────────────────────────────────────────────────
   Affiche des publicités intrusives
   Suit votre navigation pour profiler vos habitudes
   
   ③ INFOSTEALER (voleur d'informations)
   ──────────────────────────────────────────────────────────────
   Vole :
   • Cookies de session (pour usurper votre identité)
   • Fichiers sensibles
   • Mots de passe stockés dans le navigateur
   
   ④ STALKERWARE (logiciel de harcèlement)
   ──────────────────────────────────────────────────────────────
   Souvent installé par un conjoint jaloux ou un parent :
   • Localise le téléphone en temps réel
   • Lit les SMS et emails
   • Enregistre les appels
```

---

### V.B. Signes d'Infection par Spyware

```
SYMPTÔMES POSSIBLES
═══════════════════════════════════════════════════════════════

☐ PC plus lent que d'habitude (CPU utilisé par le spyware)
☐ Fenêtres pop-up publicitaires intempestives
☐ Page d'accueil du navigateur changée sans votre accord
☐ Nouveaux programmes installés que vous ne reconnaissez pas
☐ Batterie du téléphone se vide rapidement (enregistrement en arrière-plan)
☐ Trafic réseau anormal (données envoyées à l'extérieur)
```

---

### V.C. Exemple : Pegasus (2016-2023)

**Le spyware le plus sophistiqué au monde**

```
NOM : Pegasus
DÉVELOPPEUR : NSO Group (entreprise israélienne)
TYPE : Spyware militaire (vendu aux gouvernements)
CIBLE : Téléphones (iOS, Android)

CAPACITÉS
─────────────────────────────────────────────────────────────
Une fois installé, Pegasus peut :
• Lire tous les messages (SMS, WhatsApp, Signal, Telegram)
• Écouter les appels téléphoniques
• Activer le micro et enregistrer les conversations
• Activer la caméra et prendre des photos/vidéos
• Localiser le téléphone en temps réel
• Extraire les fichiers (photos, contacts, emails)
• Enregistrer les frappes clavier
• Accéder aux applications (banque, réseaux sociaux)

INFECTION
─────────────────────────────────────────────────────────────
• "Zero-click" : Pas besoin que la victime clique sur un lien
• Exploitation de failles (iMessage, WhatsApp)
• La victime ne sait pas qu'elle est infectée

VICTIMES CONNUES
─────────────────────────────────────────────────────────────
• Jamal Khashoggi (journaliste saoudien assassiné en 2018)
• Emmanuel Macron (Président français, 2021)
• 50 000+ numéros de téléphone ciblés (journalistes, militants,
  avocats, politiciens)

SCANDALE
─────────────────────────────────────────────────────────────
Révélé par une enquête internationale (Forbidden Stories, 2021)
Apple et WhatsApp portent plainte contre NSO Group
Gouvernement américain blackliste NSO Group
```

---

## PARTIE VI — Récapitulatif Comparatif

| **Type** | **Propagation** | **Action humaine** | **Objectif** | **Exemple** |
|---|---|---|---|---|
| **Virus** | S'attache à fichiers | ✅ Oui (ouvrir fichier) | Destruction, réplication | Melissa |
| **Ver** | Réseau automatique | ❌ Non (exploite failles) | Propagation massive | Conficker |
| **Trojan** | Téléchargement volontaire | ✅ Oui (installation) | Accès distant, backdoor | Emotet |
| **Ransomware** | Email, téléchargement | ✅ Oui (clic) | Extorsion d'argent | WannaCry |
| **Spyware** | Discret | Variable | Espionnage, vol données | Pegasus |

---

