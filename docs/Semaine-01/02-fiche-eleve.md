---
author: YLP
title: 01 📚 Fiche élève
---

# 📚 FICHE DE COURS ÉLÈVE
## "Ransomware · Phishing · Cas Concrets"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 1*

---

## PARTIE III — Le Ransomware (Rançongiciel)

### III.A. Définition

Un **ransomware** (ou rançongiciel en français) est un **logiciel malveillant** qui **chiffre** les données de la victime et demande une **rançon** pour les déchiffrer.

```
   FONCTIONNEMENT D'UN RANSOMWARE
   ═══════════════════════════════════════════════════════════════
   
   ① INFECTION
   ──────────────────────────────────────────────────────────────
   • Email avec pièce jointe malveillante
   • Lien vers un site compromis
   • Clé USB infectée
   • Exploitation d'une faille (RDP, SMB)
   
   ② CHIFFREMENT
   ──────────────────────────────────────────────────────────────
   Le ransomware chiffre tous les fichiers accessibles :
   • Documents (.docx, .pdf, .xlsx)
   • Images (.jpg, .png)
   • Bases de données (.sql, .db)
   • Sauvegardes accessibles (si mal configurées)
   
   Algorithme : AES-256 (militaire, incassable)
   Clé de déchiffrement : Connue seulement par l'attaquant
   
   ③ DEMANDE DE RANÇON
   ──────────────────────────────────────────────────────────────
   Affichage d'un message :
   "Vos fichiers sont chiffrés. Payez X € en Bitcoin pour
   récupérer vos données."
   
   Montant typique :
   • Particuliers : 500-2000 €
   • PME : 10 000-100 000 €
   • Grandes entreprises : 1-50 millions €
   
   ④ DEUX ISSUES POSSIBLES
   ──────────────────────────────────────────────────────────────
   A) La victime paie → L'attaquant envoie la clé (parfois)
   B) La victime ne paie pas → Perte définitive des données
                              (sauf si sauvegardes)
```

---

### III.B. Statistiques (France, 2023)

- **54%** des entreprises françaises ont été victimes d'une tentative de ransomware
- **1 attaque toutes les 11 secondes** dans le monde
- **Coût moyen** d'une attaque : 4,5 millions € (dont rançon + reconstruction + perte d'activité)
- **Taux de paiement** : 32% des victimes paient la rançon
- **Taux de récupération** : Même en payant, seulement 65% des données sont récupérées

> ⚠️ **Payer la rançon ne garantit PAS la récupération des données et finance les cybercriminels.**

---

### III.C. Cas Concret : WannaCry (Mai 2017)

**Le plus grand ransomware de l'histoire**

```
   WANNACRY — CHRONOLOGIE
   ═══════════════════════════════════════════════════════════════
   
   12 MAI 2017
   ──────────────────────────────────────────────────────────────
   • 14h00 : Première infection au Royaume-Uni (NHS)
   • 15h00 : 16 hôpitaux britanniques paralysés
   • 17h00 : Propagation en Europe (Espagne, Allemagne, France)
   • 20h00 : Renault, Nissan arrêtent la production (France, UK)
   • 23h00 : 100 000 ordinateurs infectés dans 150 pays
   
   13 MAI 2017
   ──────────────────────────────────────────────────────────────
   • Propagation continue (Asie, Amérique)
   • Deutsche Bahn (trains allemands) : écrans infectés
   • FedEx (logistique USA) : systèmes bloqués
   • 300 000 ordinateurs infectés dans 150 pays
   
   VICTIMES NOTABLES
   ──────────────────────────────────────────────────────────────
   • NHS (santé UK) : 19 000 rendez-vous annulés
   • Renault : 5 usines arrêtées (France)
   • Telefónica (télécoms Espagne)
   • Ministère de l'Intérieur russe
   
   COÛT TOTAL MONDIAL : 4 MILLIARDS € (estimation Europol)
   
   VULNÉRABILITÉ EXPLOITÉE
   ──────────────────────────────────────────────────────────────
   CVE-2017-0144 (EternalBlue) — Faille Windows SMB
   
   Patch Microsoft disponible depuis : 14 MARS 2017 (2 mois avant !)
   
   → Les victimes n'avaient PAS installé les mises à jour
```

**Leçon :** Une simple mise à jour Windows aurait empêché l'infection.

---

## PARTIE IV — Le Phishing (Hameçonnage)

### IV.A. Définition

Le **phishing** (hameçonnage) est une technique d'**arnaque** visant à **voler des informations personnelles** (mots de passe, données bancaires) en se faisant passer pour un organisme de confiance.

```
   MÉTAPHORE DE LA PÊCHE
   ═══════════════════════════════════════════════════════════════
   
   Phishing = Pêche à l'hameçon
   
   🎣 L'hameçon : Email ou SMS qui semble légitime
   🐟 Le poisson : La victime (vous)
   🪝 L'appât : Urgence, promotion, alerte sécurité
   
   Si vous mordez (cliquez) → Vous êtes ferré (piégé)
```

---

### IV.B. Types de Phishing

**① EMAIL PHISHING (le plus courant)**

Exemple typique :

```
De : service-client@paypa1.com  ← Attention au '1' à la place du 'l'
Objet : Alerte sécurité — Action requise

Bonjour,

Nous avons détecté une activité suspecte sur votre compte PayPal.

Pour des raisons de sécurité, votre compte a été temporairement
suspendu.

Cliquez ici pour vérifier votre identité et réactiver votre compte :
[Lien malveillant]

Si vous ne le faites pas sous 24h, votre compte sera définitivement
fermé.

Cordialement,
L'équipe PayPal
```

**Signaux d'alerte :**
- ❌ Expéditeur : `paypa1.com` (fake, vrai = paypal.com)
- ❌ Urgence artificielle ("24h", "suspendu")
- ❌ Lien : Ne PAS cliquer (survoler pour voir la vraie URL)
- ❌ Ton anxiogène

**② SPEAR PHISHING (ciblé)**

Attaque personnalisée contre une personne précise (cadre, dirigeant).

Exemple :

```
De : pdg@entreprise-abc.fr  ← Spoofing (usurpation d'identité)
À : comptable@entreprise-abc.fr
Objet : Virement urgent

Bonjour Sophie,

Je suis en déplacement à l'étranger et je n'ai pas accès à mes
outils habituels.

J'ai besoin que tu effectues un virement urgent de 50 000 € vers
le compte suivant (nouveau fournisseur) :

IBAN : FR76 XXXX XXXX XXXX XXXX XXXX XXX

Merci de faire cela en priorité.

Cordialement,
Jean Dupont (PDG)
```

**Technique :** L'attaquant se renseigne sur l'entreprise (LinkedIn, site web) et usurpe l'identité du PDG.

**③ SMISHING (SMS phishing)**

Exemple :

```
📱 SMS reçu :
"Colis en attente. Frais de douane à payer : 2,50 €
Cliquez ici : http://chronopost-fr.tk/colis12345"
```

**④ VISHING (Voice phishing — téléphone)**

Exemple :

```
☎️ Appel téléphonique :
"Bonjour, je vous appelle de la Banque Populaire. Nous avons
détecté une transaction suspecte de 1200 € sur votre compte.
Pour la bloquer, j'ai besoin de votre code de sécurité..."
```

---

### IV.C. Comment Détecter un Phishing ?

**Checklist de vérification :**

```
☐ 1. VÉRIFIER L'EXPÉDITEUR
   ─────────────────────────────────────────────────────────
   Survoler le nom pour voir l'adresse email complète
   
   ✅ service@paypal.com
   ❌ service@paypa1.com
   ❌ service@paypal-secure.tk
   ❌ no-reply@email-paypal.info

☐ 2. ANALYSER LE TON
   ─────────────────────────────────────────────────────────
   ❌ Urgence excessive ("24h", "immédiat", "urgent")
   ❌ Menaces ("compte fermé", "amende", "poursuite")
   ❌ Promesses irréalistes ("Vous avez gagné 10 000 €")

☐ 3. INSPECTER LES LIENS
   ─────────────────────────────────────────────────────────
   SURVOLER (sans cliquer) le lien pour voir la vraie URL
   
   Lien affiché : www.paypal.com
   Vraie URL (en survolant) : www.paypa1-secure.tk ← FAKE

☐ 4. VÉRIFIER L'ORTHOGRAPHE
   ─────────────────────────────────────────────────────────
   ❌ Fautes d'orthographe grossières
   ❌ Formulation bizarre
   ❌ Traduction automatique (Google Translate)

☐ 5. PIÈCES JOINTES SUSPECTES
   ─────────────────────────────────────────────────────────
   ❌ Fichier .exe, .zip, .scr
   ❌ Double extension : facture.pdf.exe
   ❌ Nom bizarre : "facture_urgent_2024.zip"
```

**Que faire en cas de doute ?**
1. **NE PAS CLIQUER** sur les liens
2. Aller directement sur le site officiel (taper l'URL manuellement)
3. Appeler l'organisme concerné (numéro officiel)
4. Signaler l'email comme phishing

---

### IV.D. Cas Concret : Attaque par CEO Fraud (2019)

**Entreprise Toyota Boshoku (sous-traitant Toyota)**

```
CHRONOLOGIE
═══════════════════════════════════════════════════════════════

AOÛT 2019
──────────────────────────────────────────────────────────────
L'équipe finance de Toyota Boshoku (Europe) reçoit un email :

De : ceo@toyotaboshoku.com  ← Adresse usurpée
Objet : Acquisition confidentielle — Urgent

"Bonjour,

Nous finalisons l'acquisition confidentielle d'une entreprise
concurrente. Pour des raisons de discrétion, ce projet est connu
uniquement de la direction.

J'ai besoin que vous effectuiez un virement de 37 millions €
vers le compte de notre conseiller juridique en Hongrie.

IBAN : HU98 XXXX XXXX XXXX XXXX XXXX XXXX

Cette opération est urgente et confidentielle. Ne pas en parler.

Cordialement,
Le CEO"

RÉSULTAT
──────────────────────────────────────────────────────────────
✅ L'employé a effectué le virement (37 millions €)
❌ C'était un email de phishing (spear phishing)
❌ L'argent a été transféré vers des comptes à Hongrie, puis
   dispersé dans 20 pays en quelques heures
❌ Récupération : 0 € (argent perdu)

PERTE TOTALE : 37 MILLIONS €

CONSÉQUENCES
──────────────────────────────────────────────────────────────
• Le directeur financier a été licencié
• Procédures judiciaires contre les employés
• Impact sur la réputation de l'entreprise
• Renforcement drastique des procédures de validation
```

**Leçon :** Toujours **valider par un autre canal** (appel téléphonique) les demandes de virements urgents.

---

## V. Vocabulaire Clé

| **Terme** | **Définition** |
|-----------|---------------|
| **Hygiène numérique** | Bonnes pratiques de sécurité au quotidien |
| **Ransomware** | Malware qui chiffre les données et demande une rançon |
| **Phishing** | Arnaque visant à voler des informations en se faisant passer pour un tiers de confiance |
| **Spear phishing** | Phishing ciblé contre une personne précise |
| **Smishing** | Phishing par SMS |
| **Vishing** | Phishing par téléphone (voix) |
| **Malware** | Logiciel malveillant (virus, cheval de Troie, ransomware...) |
| **2FA / MFA** | Authentification à deux facteurs / multi-facteurs |
| **VPN** | Virtual Private Network — réseau privé virtuel chiffré |
| **ANSSI** | Agence Nationale de la Sécurité des Systèmes d'Information (France) |
| **CVE** | Common Vulnerabilities and Exposures — identifiant de vulnérabilité |

---
