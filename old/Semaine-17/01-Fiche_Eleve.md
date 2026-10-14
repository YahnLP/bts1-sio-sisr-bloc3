---
author: YLP
title: 📖 Fiche de Cours Élève
---

# Fiche de Cours Élève
## Sécurisation Infrastructure : Zones Réseau · GPO · NTFS · Sauvegardes · HTTPS

*BTS SIO SISR — Année 1 — Semaines 17-18*

---

## 🎯 Compétences RNCP

| Code | Compétence |
|------|------------|
| B3.2 | Mettre en œuvre mesures sécurité de base |
| B3.4 | Sécuriser les accès et les données |
| B2.3 | Appliquer politiques de sécurité |

---

# PARTIE I — ZONES RÉSEAU (LAN / DMZ / INTERNET)

## 1. Architecture Réseau Sécurisée

### 1.1 Les 3 Zones

```
INTERNET (Zone Non Fiable)
══════════════════════════════════════════════════════════════
         ↕ Pare-feu (Firewall externe)
DMZ — ZONE DÉMILITARISÉE (Semi-Fiable)
──────────────────────────────────────────────────────────────
• Serveurs exposés à Internet :
  - Serveur web public (HTTP/HTTPS)
  - Serveur mail (SMTP/IMAP)
  - Serveur VPN (concentrateur)
• Accès : Internet → DMZ (règles strictes)
         DMZ → LAN (interdit ou très limité)
         
         ↕ Pare-feu (Firewall interne)
LAN — RÉSEAU LOCAL (Zone Fiable)
──────────────────────────────────────────────────────────────
• Postes de travail
• Serveurs internes :
  - Fichiers (SRV-FILES)
  - Base de données (SRV-SQL)
  - Active Directory (SRV-DC)
• Accès : LAN → DMZ (autorisé)
         LAN → Internet (autorisé via proxy)
```

**Principe** : Si un serveur en DMZ est compromis, l'attaquant ne peut PAS pivoter vers le LAN (pare-feu bloque).

---

### 1.2 Pourquoi Segmenter ?

**Exemple TechSoft (non segmenté)** :
```
Attaque serveur web → Compromission
→ Accès direct réseau interne (même switch)
→ Exfiltration données + Ransomware
```

**Avec DMZ (segmenté)** :
```
Attaque serveur web → Compromission
→ Tentative accès LAN → BLOQUÉE par firewall
→ Incident limité à la DMZ
→ Données internes protégées
```

---

### 1.3 Règles Pare-feu Typiques

| Source | Destination | Port | Action | Justification |
|--------|-------------|------|--------|---------------|
| Internet | DMZ Web | 80, 443 | **Autoriser** | Accès site public |
| Internet | DMZ Mail | 25, 587, 993 | **Autoriser** | Réception/envoi mail |
| Internet | LAN | Tous | **BLOQUER** | LAN non exposé |
| DMZ | LAN | Tous | **BLOQUER** | Isolation DMZ |
| LAN | DMZ | 80, 443 | **Autoriser** | Accès site interne |
| LAN | Internet | 80, 443 | **Autoriser** | Navigation web |

---

## 2. Schéma Réseau Type

```
                   INTERNET
                      │
                      │
                 ┌────▼────┐
                 │ Firewall│
                 │ Externe │
                 └────┬────┘
                      │
            ┌─────────┴─────────┐
            │       DMZ         │
            │                   │
            │  [SRV-WEB]        │
            │  192.168.100.10   │
            │                   │
            │  [SRV-VPN]        │
            │  192.168.100.20   │
            └─────────┬─────────┘
                      │
                 ┌────▼────┐
                 │ Firewall│
                 │ Interne │
                 └────┬────┘
                      │
            ┌─────────┴─────────┐
            │       LAN         │
            │   192.168.1.0/24  │
            │                   │
            │  [SRV-DC] AD      │
            │  [SRV-FILES]      │
            │  [SRV-SQL]        │
            │  [PC-01 à PC-40]  │
            └───────────────────┘
```

---

# PARTIE II — GPO (STRATÉGIES DE GROUPE)

## 1. Définition

**GPO** (Group Policy Object) = Stratégie de groupe appliquée automatiquement aux ordinateurs/utilisateurs d'un domaine Active Directory.

**Avantage** : Configuration centralisée (1 GPO → 1000 PC).

---

## 2. GPO de Sécurité Essentielles

### 2.1 Politique de Mot de Passe

**Chemin GPO** : `Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`

**Paramètres recommandés** :

| Paramètre | Valeur | Justification |
|-----------|--------|---------------|
| **Longueur minimale** | 12 caractères | Protection brute force |
| **Complexité** | Activée | Maj + min + chiffre + symbole |
| **Historique** | 12 mots de passe | Éviter réutilisation |
| **Âge maximum** | 90 jours | Renouvellement régulier |
| **Âge minimum** | 1 jour | Éviter changements multiples |

---

### 2.2 Politique de Verrouillage

**Chemin GPO** : `Account Policies > Account Lockout Policy`

| Paramètre | Valeur | Justification |
|-----------|--------|---------------|
| **Seuil verrouillage** | 5 tentatives | Protection brute force |
| **Durée verrouillage** | 30 minutes | Équilibre sécurité/usabilité |
| **Réinitialisation compteur** | 30 minutes | Après dernière tentative |

---

### 2.3 Pare-feu Windows

**Chemin GPO** : `Computer Configuration > Policies > Windows Settings > Security Settings > Windows Defender Firewall`

**Paramètres** :
- Profil Domaine : **Activé**
- Profil Privé : **Activé**
- Profil Public : **Activé** (règles strictes)
- Bloquer connexions entrantes par défaut : **Oui**
- Autoriser connexions sortantes par défaut : **Oui**

---

### 2.4 Autres GPO Utiles

**Restriction logiciels** :
- Bloquer exécution depuis `%TEMP%`, `%APPDATA%` (anti-malware)

**Mise à jour Windows** :
- Installation automatique mises à jour (nuit)

**Écran de verrouillage** :
- Verrouillage auto après 10 min inactivité

**Désactivation ports USB** :
- Empêcher branchement clés USB non autorisées

---

## 3. Appliquer une GPO

**Procédure** :
1. Serveur AD → Ouvrir `gpmc.msc` (Gestion stratégies de groupe)
2. Clic droit sur OU cible (ex : `OU=Postes,DC=datacorp,DC=local`)
3. "Créer un objet GPO et le lier ici"
4. Nommer : `GPO-Securite-Postes`
5. Clic droit → Modifier → Configurer paramètres
6. Sur les PC : `gpupdate /force` (application immédiate)

---

# PARTIE III — DROITS NTFS

## 1. Principe Moindre Privilège

**Règle d'or** : Un utilisateur doit avoir UNIQUEMENT les droits nécessaires à son travail.

**Mauvaise pratique** : Tout le monde "Contrôle total" sur `\\SRV-FILES\Commun`

**Bonne pratique** : Matrice de droits par service.

---

## 2. Permissions NTFS

| Permission | Lecture | Écriture | Modification | Suppression | Exécution |
|------------|---------|----------|--------------|-------------|-----------|
| **Lecture** | ✅ | ❌ | ❌ | ❌ | ✅ |
| **Lecture et exécution** | ✅ | ❌ | ❌ | ❌ | ✅ |
| **Écriture** | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Modification** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Contrôle total** | ✅ | ✅ | ✅ | ✅ | ✅ + Permissions |

---

## 3. Matrice de Droits par Service (Exemple)

**Structure dossiers** :
```
\\SRV-FILES\
  ├─ Commun\          (tous en lecture)
  ├─ Comptabilite\    (Groupe Compta)
  ├─ RH\              (Groupe RH)
  ├─ Projets\         (Groupe Projets)
  └─ Direction\       (Direction uniquement)
```

**Matrice** :

| Dossier | Groupe Compta | Groupe RH | Groupe Projets | Direction | IT |
|---------|---------------|-----------|----------------|-----------|-----|
| **Commun** | Lecture | Lecture | Lecture | Modification | Contrôle total |
| **Comptabilite** | Modification | ❌ | ❌ | Lecture | Contrôle total |
| **RH** | ❌ | Modification | ❌ | Lecture | Contrôle total |
| **Projets** | ❌ | ❌ | Modification | Lecture | Contrôle total |
| **Direction** | ❌ | ❌ | ❌ | Modification | Contrôle total |

**Justification** :
- Comptabilité n'a PAS accès aux dossiers RH (confidentialité)
- Direction a accès en lecture à tout (supervision)
- IT a contrôle total (administration)

---

## 4. Configuration NTFS

**Procédure** :
1. Clic droit dossier → Propriétés → Onglet Sécurité
2. Désactiver héritage : "Désactiver l'héritage" → Convertir
3. Supprimer "Utilisateurs" et "Tout le monde"
4. Ajouter groupe : Ajouter → "Groupe-Compta" → Modifier
5. Répéter pour chaque groupe
6. Appliquer → OK

---

# PARTIE IV — SAUVEGARDES

## 1. Règle 3-2-1

```
RÈGLE 3-2-1 DES SAUVEGARDES
══════════════════════════════════════════════════════════════

3 → TROIS copies des données
    • 1 original (données production)
    • 2 sauvegardes

2 → DEUX supports différents
    • Exemple : Disque local + NAS réseau
    • OU : Disque local + Cloud

1 → UNE copie hors site
    • Protection incendie, inondation, ransomware
    • Cloud ou site distant géographiquement
```

---

## 2. Types de Sauvegardes

| Type | Contenu | Fréquence | Temps restauration |
|------|---------|-----------|---------------------|
| **Complète** | TOUS les fichiers | Hebdomadaire (dimanche) | Rapide (1 seul fichier) |
| **Différentielle** | Fichiers modifiés depuis dernière COMPLÈTE | Quotidienne | Moyen (Complète + Dernière diff) |
| **Incrémentielle** | Fichiers modifiés depuis dernière backup | Toutes les 6h | Lent (Complète + Toutes les incr) |

**Recommandation** : Complète hebdo + Différentielle quotidienne (bon compromis).

---

## 3. Plan de Sauvegarde Exemple

**Entreprise DataCorp** :

| Quoi | Quand | Où | Outil | Rétention |
|------|-------|-----|-------|-----------|
| **Serveur fichiers** | Quotidien 2h | NAS local | Veeam Backup | 30 jours |
| **Base SQL** | Quotidien 3h | NAS local | SQL Server Agent | 30 jours |
| **Archive mensuelle** | 1er du mois | Cloud AWS S3 | Veeam Cloud | 12 mois |
| **Test restauration** | Mensuel | VM test | Manuel | — |

**Chiffrement** : Sauvegardes chiffrées AES-256 (RGPD + protection ransomware).

---

## 4. Test de Restauration

**⚠️ CRITIQUE** : Une sauvegarde non testée = Pas de sauvegarde.

**Procédure mensuelle** :
1. Choisir sauvegarde aléatoire (1 semaine aléatoire)
2. Restaurer sur VM isolée
3. Vérifier intégrité fichiers
4. Chronométrer temps restauration
5. Documenter résultat (OK / KO)

---

# PARTIE V — HTTPS ET CERTIFICATS SSL/TLS

## 1. Pourquoi HTTPS ?

**HTTP** (port 80) :
- ❌ Données en CLAIR (lisibles par attaquant)
- ❌ Pas d'authentification serveur
- ❌ Pas d'intégrité (données modifiables en transit)

**HTTPS** (port 443) :
- ✅ Chiffrement TLS (AES-256-GCM)
- ✅ Authentification serveur (certificat X.509)
- ✅ Intégrité (HMAC)

**Obligation** : Google Chrome affiche "Non sécurisé" si HTTP (depuis 2018).

---

## 2. Certificat SSL/TLS

**Certificat X.509** (vu S13) contient :
- Nom domaine (CN : www.datacorp.fr)
- Clé publique du serveur
- Signature CA (Let's Encrypt, DigiCert...)
- Validité (ex : 90 jours Let's Encrypt)

**Chaîne de confiance** :
```
Root CA (Navigateur) → Intermediate CA → Certificat serveur
```

---

## 3. Obtenir un Certificat

### Option 1 : Let's Encrypt (Gratuit, Auto-Renouvelé)

**Pour site public** :

```bash
# Installation Certbot (Linux)
sudo apt install certbot python3-certbot-apache

# Obtention certificat
sudo certbot --apache -d www.datacorp.fr

# Auto-renouvellement (cron)
sudo certbot renew
```

### Option 2 : Certificat Payant (DigiCert, Sectigo)

**Pour site e-commerce** (assurance, support).

Prix : 50-300 €/an.

### Option 3 : Certificat Auto-Signé

**Pour intranet uniquement** (navigateur affiche alerte).

```bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
```

---

## 4. Configurer HTTPS (Apache)

**Fichier** : `/etc/apache2/sites-available/default-ssl.conf`

```apache
<VirtualHost *:443>
    ServerName www.datacorp.fr
    DocumentRoot /var/www/html
    
    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/datacorp.fr/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/datacorp.fr/privkey.pem
    
    # Protocoles sécurisés seulement
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite HIGH:!aNULL:!MD5
</VirtualHost>
```

**Activation** :
```bash
sudo a2enmod ssl
sudo a2ensite default-ssl
sudo systemctl restart apache2
```

**Test** : https://www.datacorp.fr → Cadenas vert

---

## 5. Redirection HTTP → HTTPS

**Forcer HTTPS** :

```apache
<VirtualHost *:80>
    ServerName www.datacorp.fr
    Redirect permanent / https://www.datacorp.fr/
</VirtualHost>
```

→ Toute requête HTTP redirigée automatiquement vers HTTPS.

---

# VOCABULAIRE CLÉ

| Terme | Définition |
|-------|------------|
| **LAN** | Local Area Network — Réseau local interne |
| **DMZ** | Zone Démilitarisée — Réseau semi-fiable pour serveurs publics |
| **GPO** | Group Policy Object — Stratégie de groupe Active Directory |
| **NTFS** | Système fichiers Windows avec permissions ACL |
| **Principe moindre privilège** | Donner uniquement droits nécessaires |
| **Règle 3-2-1** | 3 copies, 2 supports, 1 hors site |
| **Complète** | Sauvegarde de tous les fichiers |
| **Différentielle** | Fichiers modifiés depuis dernière complète |
| **HTTPS** | HTTP sécurisé par TLS/SSL (port 443) |
| **Certificat X.509** | Certificat numérique identifiant serveur |
| **Let's Encrypt** | CA gratuite, certificats 90 jours auto-renouvelés |

---

*Fiche de Cours S17 BLOC 3 — BTS SIO SISR*
