---
author: YLP
title: 📐 Exemples & Modèles
---

# Exemples & Modèles
## Templates pour le Projet

---

## 📐 MODÈLE 1 : Schéma Réseau

### Structure Attendue

```
┌─────────────────────────────────────────────────────────┐
│                      INTERNET                           │
│                   (Non Fiable)                          │
└────────────────────┬────────────────────────────────────┘
                     │
              ┌──────▼──────┐
              │  Firewall   │  Règles : Internet → DMZ (80,443)
              │  Externe    │           Internet → LAN (BLOCK)
              │  (pfSense)  │
              └──────┬──────┘
                     │
        ┌────────────┴────────────┐
        │         DMZ             │  192.168.100.0/24
        │    (Semi-Fiable)        │
        │                         │
        │  [SRV-WEB]              │  .10 - Apache (80,443)
        │  [SRV-VPN] (optionnel)  │  .20 - VPN Concentrator
        │                         │
        └────────────┬────────────┘
                     │
              ┌──────▼──────┐
              │  Firewall   │  Règles : LAN → DMZ (80,443)
              │  Interne    │           LAN → Internet (80,443)
              │             │           DMZ → LAN (BLOCK)
              └──────┬──────┘
                     │
        ┌────────────┴────────────┐
        │         LAN             │  192.168.1.0/24
        │      (Fiable)           │
        │                         │
        │  [SRV-DC]      .10      │  Active Directory
        │  [SRV-FILES]   .20      │  Fichiers partagés
        │  [SRV-SQL]     .30      │  Base données
        │  [PC-01...45]  .50-.95  │  Postes utilisateurs
        │                         │
        └─────────────────────────┘
```

---

## 📋 MODÈLE 2 : Documentation GPO

### Template Fiche GPO

```
═══════════════════════════════════════════════════════════
                    GPO : [NOM GPO]
═══════════════════════════════════════════════════════════

NOM COMPLET : GPO-Securite-MDP-Domaine

CIBLE (OU) : Domain Controllers / OU=Utilisateurs

TYPE : Ordinateur ☐  Utilisateur ☑

CHEMIN GPO :
Computer Configuration > Policies > Windows Settings > 
Security Settings > Account Policies > Password Policy

PARAMÈTRES CONFIGURÉS :
┌──────────────────────────────────────────────────────┐
│ Paramètre                    │ Valeur   │ Défaut     │
├──────────────────────────────────────────────────────┤
│ Enforce password history     │ 12       │ 0          │
│ Maximum password age         │ 90 days  │ 42 days    │
│ Minimum password age         │ 1 day    │ 0          │
│ Minimum password length      │ 12       │ 7          │
│ Password must meet complexity│ Enabled  │ Disabled   │
└──────────────────────────────────────────────────────┘

JUSTIFICATION :
Cette GPO renforce la sécurité des mots de passe selon les 
recommandations ANSSI 2021 :
- 12 caractères minimum (protection brute force)
- Complexité obligatoire (maj+min+chiffre+symbole)
- Historique 12 (évite réutilisation immédiate)
- Renouvellement 90j (compromis sécurité/usabilité)

CAPTURE ÉCRAN :
[Insérer capture configuration GPO]

═══════════════════════════════════════════════════════════
```

---

## 📊 MODÈLE 3 : Matrice NTFS

### Template Excel/Word

```
STRUCTURE DOSSIERS \\SRV-FILES\
═══════════════════════════════════════════════════════════

\SRV-FILES\
  ├─ Commun\              (Lecture tous, Modification Direction+IT)
  ├─ Comptabilite\        (Modification Compta, Lecture Direction, Contrôle IT)
  ├─ RH\                  (Modification RH, Lecture Direction, Contrôle IT)
  ├─ Developpement\       (Modification Dev, Lecture Direction, Contrôle IT)
  ├─ Commercial\          (Modification Commercial, Lecture Direction, Contrôle IT)
  └─ Direction\           (Modification Direction, Contrôle IT)

MATRICE PERMISSIONS
═══════════════════════════════════════════════════════════

| Dossier         | Direction | Compta | RH  | Dev | Commercial | IT      |
|-----------------|-----------|--------|-----|-----|------------|---------|
| **Commun**      | Modif     | Lect   | Lect| Lect| Lect       | Contrôle|
| **Comptabilite**| Lect      | Modif  | ❌  | ❌  | ❌         | Contrôle|
| **RH**          | Lect      | ❌     | Modif|❌  | ❌         | Contrôle|
| **Developpement**|Lect      | ❌     | ❌  |Modif| ❌         | Contrôle|
| **Commercial**  | Lect      | ❌     | ❌  | ❌  | Modif      | Contrôle|
| **Direction**   | Modif     | ❌     | ❌  | ❌  | ❌         | Contrôle|

LÉGENDE :
- Lect       : Lecture seule
- Modif      : Modification (Lecture + Écriture + Suppression)
- Contrôle   : Contrôle total (+ gestion permissions)
- ❌         : Aucun accès

JUSTIFICATIONS :
- Comptabilité N'A PAS accès RH (confidentialité salaires)
- RH N'A PAS accès Comptabilité (séparation des tâches)
- Direction a LECTURE sur tous les services (supervision)
- IT a CONTRÔLE TOTAL (administration système)
- Dossier Commun = Documentation interne accessible à tous
```

---

## 💾 MODÈLE 4 : Plan de Sauvegarde

### Template Document

```
═══════════════════════════════════════════════════════════
              PLAN DE SAUVEGARDE DATACORP SARL
═══════════════════════════════════════════════════════════

STRATÉGIE GLOBALE :
• Type : Complète hebdomadaire + Différentielle quotidienne
• Règle 3-2-1 respectée
• Chiffrement : AES-256 (RGPD + protection ransomware)
• Rétention : 30 jours local, 12 mois cloud

TABLEAU DÉTAILLÉ :
┌───────────────────────────────────────────────────────────┐
│ Quoi      │Quand     │Où         │Comment  │Rétention    │
├───────────────────────────────────────────────────────────┤
│SRV-FILES  │Quotidien │NAS local  │Veeam    │30 jours     │
│           │02:00     │Synology   │Backup   │             │
├───────────────────────────────────────────────────────────┤
│SRV-SQL    │Quotidien │NAS local  │SQL      │30 jours     │
│(BDD)      │03:00     │           │Agent    │             │
├───────────────────────────────────────────────────────────┤
│SRV-DC     │Quotidien │NAS local  │Windows  │30 jours     │
│(AD)       │04:00     │           │Server   │             │
│           │          │           │Backup   │             │
├───────────────────────────────────────────────────────────┤
│Archive    │1er du    │AWS S3     │Veeam    │12 mois      │
│mensuelle  │mois      │(hors site)│Cloud    │             │
└───────────────────────────────────────────────────────────┘

VÉRIFICATION RÈGLE 3-2-1 :
✅ 3 copies : 1 production + 1 NAS + 1 cloud
✅ 2 supports : NAS local + Cloud AWS
✅ 1 hors site : AWS S3 (datacenter distant)

PROCÉDURE TEST RESTAURATION (MENSUEL) :
1. Choisir sauvegarde aléatoire (semaine N-2)
2. Restaurer sur VM isolée (pas production)
3. Vérifier intégrité :
   - Fichiers accessibles
   - BDD SQL fonctionnelle
   - AD consultable
4. Chronométrer temps restauration
5. Documenter dans journal (OK/KO + durée)

PLANNING TESTS 2026 :
• Janvier : SRV-FILES
• Février : SRV-SQL
• Mars : SRV-DC
• [rotation mensuelle]

═══════════════════════════════════════════════════════════
```

---

## 🔒 MODÈLE 5 : Configuration HTTPS

### Template Procédure

```
═══════════════════════════════════════════════════════════
        CONFIGURATION HTTPS — SRV-WEB (APACHE)
═══════════════════════════════════════════════════════════

CHOIX CERTIFICAT : Let's Encrypt (Gratuit, Auto-renouvelé)

JUSTIFICATION :
• Gratuit (budget limité)
• Reconnu par tous navigateurs
• Auto-renouvellement tous les 90j (via cron)
• Adapté site vitrine public

PROCÉDURE INSTALLATION :
═══════════════════════════════════════════════════════════

ÉTAPE 1 : Installation Certbot
──────────────────────────────────────────────────────────
sudo apt update
sudo apt install certbot python3-certbot-apache

ÉTAPE 2 : Obtention certificat
──────────────────────────────────────────────────────────
sudo certbot --apache -d www.datacorp.fr -d datacorp.fr

# Certbot configure automatiquement Apache
# Certificats stockés : /etc/letsencrypt/live/datacorp.fr/

ÉTAPE 3 : Vérification configuration Apache
──────────────────────────────────────────────────────────
sudo nano /etc/apache2/sites-available/datacorp-ssl.conf

<VirtualHost *:443>
    ServerName www.datacorp.fr
    DocumentRoot /var/www/html
    
    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/datacorp.fr/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/datacorp.fr/privkey.pem
    
    # Protocoles sécurisés uniquement
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite HIGH:!aNULL:!MD5
</VirtualHost>

ÉTAPE 4 : Redirection HTTP → HTTPS
──────────────────────────────────────────────────────────
sudo nano /etc/apache2/sites-available/datacorp.conf

<VirtualHost *:80>
    ServerName www.datacorp.fr
    Redirect permanent / https://www.datacorp.fr/
</VirtualHost>

ÉTAPE 5 : Activation et redémarrage
──────────────────────────────────────────────────────────
sudo a2enmod ssl
sudo a2ensite datacorp-ssl
sudo systemctl restart apache2

ÉTAPE 6 : Test
──────────────────────────────────────────────────────────
# Navigateur : https://www.datacorp.fr
# Vérifier cadenas vert
# SSL Labs : https://www.ssllabs.com/ssltest/

ÉTAPE 7 : Auto-renouvellement (Cron)
──────────────────────────────────────────────────────────
sudo certbot renew --dry-run  # Test
sudo crontab -e
# Ajouter :
0 3 * * * certbot renew --quiet

═══════════════════════════════════════════════════════════

CAPTURE VALIDATION :
[Insérer screenshot navigateur avec cadenas HTTPS]

═══════════════════════════════════════════════════════════
```

---

*Exemples & Modèles S17 BLOC 3 — BTS SIO SISR*
