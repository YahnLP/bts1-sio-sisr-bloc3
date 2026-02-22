---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "Durées de Conservation · Archivage · Purge Automatique"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 7*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.3** | Gérer les incidents de sécurité |

---

## PARTIE I — Principe de Limitation de Conservation

### I.A. Définition (Art. 5.1.e RGPD)

> *"Les données à caractère personnel doivent être conservées sous une forme permettant l'identification des personnes concernées pendant une durée n'excédant pas celle nécessaire au regard des finalités pour lesquelles elles sont traitées."*

**En langage simple :**
> Les données personnelles ne peuvent pas être conservées **indéfiniment**. Dès que leur utilité prend fin, elles doivent être **supprimées ou anonymisées**.

---

### I.B. Les 3 Phases de Vie d'une Donnée

```
   CYCLE DE VIE D'UNE DONNÉE PERSONNELLE
   ═══════════════════════════════════════════════════════════════

   PHASE 1 — BASE ACTIVE (Conservation courante)
   ──────────────────────────────────────────────────────────────
   Données régulièrement utilisées
   Accès fréquent par les équipes opérationnelles
   Stockage : Base de données principale, serveurs de fichiers

   Exemple : Client actif → Données dans le CRM
   Durée : Pendant toute la durée de la relation + quelques années

                              ↓
              (Fin de la relation / utilité terminée)
                              ↓

   PHASE 2 — ARCHIVAGE INTERMÉDIAIRE
   ──────────────────────────────────────────────────────────────
   Données encore nécessaires pour des obligations légales
   (comptabilité, litiges, garanties)
   Accès rare, sur demande spécifique
   Stockage : Serveur d'archivage, accès restreint

   Exemple : Client inactif depuis 3 ans → Données en archive
   (factures conservées 10 ans pour comptabilité)
   Accès : Directeur financier, comptable, juriste uniquement

                              ↓
         (Fin des obligations légales / délais écoulés)
                              ↓

   PHASE 3 — SUPPRESSION OU ANONYMISATION
   ──────────────────────────────────────────────────────────────
   Les données ne sont plus nécessaires → Fin de vie
   ① Suppression : Effacement définitif et irréversible
   ② Anonymisation : Suppression des identifiants
      → Données conservées pour statistiques uniquement

   Exemple : Client inactif 10 ans → Données supprimées
   (ou anonymisées si statistiques utiles)
```

---

### I.C. Tableau des Durées Légales

| **Type de données** | **Base légale** | **Conservation active** | **Archivage** |
|---|---|---|---|
| **Données clients** (contrats, commandes) | Code civil | 3 ans après dernier contact | 5 ans (prescription) |
| **Données comptables** (factures, bilans) | Code de commerce | 10 ans | 10 ans |
| **Données fiscales** | Code général des impôts | 6 ans | 6 ans |
| **Données RH** (dossiers salariés) | Code du travail | Durée du contrat + 5 ans | 5 ans |
| **Fiches de paie** | Code du travail | 5 ans | 5 ans |
| **Logs informatiques** | LCEN + CNIL | 1 an | 1 an |
| **Vidéosurveillance** | Code de la sécurité intérieure | **30 jours maximum** | Interdit |
| **Cookies** | Directive ePrivacy + CNIL | **13 mois maximum** | Non applicable |
| **Données de prospection** | RGPD + CNIL | 3 ans sans interaction | — |
| **Curriculum vitae** (candidats non retenus) | CNIL | 2 ans | — |
| **Données médicales** (patients) | Code de la santé | 20 ans | 20 ans |
| **Données de navigation** (hébergeurs) | LCEN | 1 an | 1 an |

> 📌 **Règle CNIL :** En l'absence de texte légal, la durée de conservation doit être proportionnelle à la finalité. Prévoir des durées et les documenter dans le registre des traitements.

---

### I.D. Implémentation Technique : La Purge Automatique

**Le problème :** Les durées de conservation sont inutiles sans mécanisme automatique de suppression.

**Solution : Tâche automatisée (CRON job + script SQL)**

```
   EXEMPLE — Purge des données clients inactifs (3 ans)
   ═══════════════════════════════════════════════════════════════

   SCRIPT SQL (purge_clients.sql)
   ──────────────────────────────────────────────────────────────
   -- Étape 1 : Logger les données avant suppression (audit)
   INSERT INTO audit_purge (table_name, record_id, purge_date, reason)
   SELECT 'clients', id, NOW(), 'Inactivité > 3 ans'
   FROM clients
   WHERE last_activity < DATE_SUB(NOW(), INTERVAL 3 YEAR)
   AND data_deleted = 0;

   -- Étape 2 : Anonymiser (si besoin de conserver les stats)
   UPDATE clients
   SET
     nom = 'SUPPRIME',
     prenom = 'SUPPRIME',
     email = CONCAT('deleted_', id, '@purge.local'),
     telephone = NULL,
     adresse = NULL,
     date_naissance = NULL,
     data_deleted = 1,
     date_deletion = NOW()
   WHERE last_activity < DATE_SUB(NOW(), INTERVAL 3 YEAR)
   AND data_deleted = 0;

   -- Étape 3 : Supprimer si aucune obligation légale
   DELETE FROM clients
   WHERE last_activity < DATE_SUB(NOW(), INTERVAL 10 YEAR)
   AND data_deleted = 1;
   -- (après 10 ans → même les archives comptables sont purgées)


   TÂCHE CRON (Linux) — Exécution chaque nuit à 2h
   ──────────────────────────────────────────────────────────────
   # crontab -e
   0 2 * * * mysql -u rgpd_user -p'motdepasse' ma_base < /opt/scripts/purge_clients.sql >> /var/log/purge_rgpd.log 2>&1


   SCRIPT WINDOWS (PowerShell + Task Scheduler)
   ──────────────────────────────────────────────────────────────
   # purge_clients.ps1
   $date = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
   Invoke-Sqlcmd -Query "
     UPDATE clients SET nom='SUPPRIME', email=CONCAT('del_',id,'@purge.local')
     WHERE last_activity < DATEADD(year, -3, GETDATE())
     AND data_deleted = 0
   " -ServerInstance "SERVEUR\INSTANCE"
   Write-Log "Purge exécutée : $date"
```

---

### I.E. Purge des Logs Informatiques

**Durée légale des logs :** 1 an (LCEN + recommandation CNIL)

```
   GESTION DES LOGS CONFORME RGPD
   ═══════════════════════════════════════════════════════════════

   STRUCTURE RECOMMANDÉE
   ──────────────────────────────────────────────────────────────
   /var/log/
   ├── application/
   │   ├── app-2024-01.log    ← Conservation 12 mois
   │   ├── app-2024-02.log
   │   └── ...
   ├── access/
   │   ├── access-2024-01.log ← Contient IP (donnée perso)
   │   └── ...
   └── audit/
       └── audit-2024-01.log  ← Logs RGPD (accès aux données)

   ROTATION AUTOMATIQUE (logrotate - Linux)
   ──────────────────────────────────────────────────────────────
   # /etc/logrotate.d/application
   /var/log/application/*.log {
     monthly          # Rotation mensuelle
     rotate 12        # Conserver 12 mois
     compress         # Compresser les anciens logs
     delaycompress    # Ne pas compresser le log d'hier
     missingok        # Pas d'erreur si log absent
     notifempty       # Pas de rotation si fichier vide
     postrotate
       # Script de suppression après 12 mois
       find /var/log/application/ -name "*.log.gz" -mtime +365 -delete
     endscript
   }
```

---

## PARTIE II — Sécurisation des Données (Art. 25 et 32 RGPD)

### II.A. Les 2 Principes Fondateurs

**Article 25 — Privacy by Design (Protection dès la Conception)**

```
   PRIVACY BY DESIGN : 7 PRINCIPES FONDATEURS
   ═══════════════════════════════════════════════════════════════

   ① PROACTIF, PAS RÉACTIF
   ──────────────────────────────────────────────────────────────
   Anticiper les risques AVANT qu'ils se produisent
   ❌ "On verra si on a des problèmes"
   ✅ "Comment protéger les données dès la conception ?"

   ② PROTECTION PAR DÉFAUT
   ──────────────────────────────────────────────────────────────
   Les paramètres par défaut doivent être les plus protecteurs
   ❌ Profil public par défaut (réseau social)
   ✅ Profil privé par défaut → L'utilisateur choisit de le rendre public

   ③ INTÉGRATION DANS LA CONCEPTION
   ──────────────────────────────────────────────────────────────
   La protection n'est pas une surcouche ajoutée après
   ❌ Développer l'app, puis "ajouter la sécurité RGPD"
   ✅ Intégrer la protection dès les premières maquettes

   ④ FONCTIONNALITÉ TOTALE (pas de compromis)
   ──────────────────────────────────────────────────────────────
   Protection ET fonctionnalité vont ensemble
   ❌ "Plus c'est sécurisé, moins c'est fonctionnel"
   ✅ Trouver la solution qui assure les deux

   ⑤ SÉCURITÉ DE BOUT EN BOUT
   ──────────────────────────────────────────────────────────────
   Protection pendant tout le cycle de vie des données
   De la collecte à la suppression

   ⑥ VISIBILITÉ ET TRANSPARENCE
   ──────────────────────────────────────────────────────────────
   Rendre les pratiques vérifiables et auditables

   ⑦ CENTRÉ SUR L'UTILISATEUR
   ──────────────────────────────────────────────────────────────
   Les personnes concernées restent au centre des décisions
```

**Article 25 — Privacy by Default (Protection par Défaut)**

```
   EXEMPLES CONCRETS
   ═══════════════════════════════════════════════════════════════

   APPLICATION MOBILE
   ──────────────────────────────────────────────────────────────
   ❌ NON CONFORME :
   • Géolocalisation activée par défaut
   • Partage contacts activé par défaut
   • Publicités personnalisées activées par défaut

   ✅ CONFORME :
   • Géolocalisation DÉSACTIVÉE par défaut
   • L'app demande la permission quand la fonctionnalité est utilisée
   • Données minimales collectées (juste ce qu'il faut)

   RÉSEAU SOCIAL
   ──────────────────────────────────────────────────────────────
   ❌ NON CONFORME : Profil public par défaut (visible de tous)
   ✅ CONFORME : Profil privé par défaut → Visible amis seulement
```

---

### II.B. Mesures de Sécurité Requises (Art. 32)

**Le RGPD n'impose pas de mesures précises — il impose des mesures PROPORTIONNÉES au risque.**

```
   MESURES TECHNIQUES ET ORGANISATIONNELLES
   ═══════════════════════════════════════════════════════════════

   CATÉGORIE 1 — CHIFFREMENT
   ──────────────────────────────────────────────────────────────
   ✅ Chiffrement des données au repos (bases de données, fichiers)
      → MySQL : chiffrement TDE (Transparent Data Encryption)
      → Fichiers : VeraCrypt, LUKS, BitLocker

   ✅ Chiffrement des données en transit (communications)
      → HTTPS/TLS 1.3 pour les sites web
      → VPN pour les accès distants
      → SFTP/FTPS pour les transferts de fichiers

   ✅ Chiffrement des sauvegardes
      → Jamais stocker des sauvegardes non chiffrées hors site

   CATÉGORIE 2 — CONTRÔLE DES ACCÈS
   ──────────────────────────────────────────────────────────────
   ✅ Principe du moindre privilège (accès minimal nécessaire)
      → DBA : Accès total BDD
      → Développeur : Accès BDD dev/test uniquement
      → Commercial : Accès aux seules données clients de son périmètre

   ✅ Authentification forte (MFA) pour les accès sensibles
   ✅ Revue périodique des droits (tous les 6 mois)
   ✅ Suppression immédiate des accès (départ salarié)

   CATÉGORIE 3 — TRAÇABILITÉ ET AUDIT
   ──────────────────────────────────────────────────────────────
   ✅ Logs de tous les accès aux données personnelles
      Qui, quoi, quand, depuis où
      → SELECT sur tables données perso = loggué

   ✅ Alertes sur comportements anormaux
      → Accès massif de données hors heures ouvrées
      → Export inhabituel (10 000 lignes d'un coup)

   CATÉGORIE 4 — CONTINUITÉ ET DISPONIBILITÉ
   ──────────────────────────────────────────────────────────────
   ✅ Sauvegardes régulières et testées (vu en S4)
   ✅ Plan de reprise d'activité (PRA)
   ✅ Tests de restauration réguliers

   CATÉGORIE 5 — ORGANISATION
   ──────────────────────────────────────────────────────────────
   ✅ Sensibilisation et formation des salariés
   ✅ Politique de gestion des mots de passe
   ✅ Politique BYOD (appareils personnels)
   ✅ Procédure de gestion des incidents
   ✅ Clause de confidentialité dans les contrats
```

---

### II.C. L'Analyse d'Impact (AIPD / PIA)

**AIPD** = Analyse d'Impact relative à la Protection des Données
**PIA** = Privacy Impact Assessment (anglais)

**Définition :** Évaluation préalable des risques d'un traitement à **risque élevé** pour les personnes.

```
   QUAND RÉALISER UNE AIPD ? (Obligatoire)
   ═══════════════════════════════════════════════════════════════

   Le RGPD rend l'AIPD obligatoire si le traitement est
   "susceptible d'engendrer un risque élevé pour les droits
   et libertés des personnes" (Art. 35)

   CRITÈRES DÉCLENCHEURS (2 critères = AIPD obligatoire)
   ──────────────────────────────────────────────────────────────
   ☐ Évaluation / scoring (profilage)
   ☐ Décision automatisée avec effet significatif
   ☐ Surveillance systématique (caméras, localisation)
   ☐ Données sensibles (santé, biométrie, opinion...)
   ☐ Grande échelle (nombreuses personnes)
   ☐ Croisement de données (combinaison de plusieurs sources)
   ☐ Personnes vulnérables (enfants, patients, salariés)
   ☐ Usage innovant d'une technologie nouvelle

   EXEMPLES CONCRETS
   ──────────────────────────────────────────────────────────────
   ✅ AIPD OBLIGATOIRE :
   • Système de badge biométrique pour accès locaux
   • Application de suivi GPS des commerciaux
   • Logiciel RH avec scoring des salariés
   • Base de données de santé régionale

   ❌ AIPD NON OBLIGATOIRE :
   • Gestion des contacts email d'une newsletter
   • Site e-commerce classique
   • Registre des entrées/sorties des visiteurs (papier)
```

---
