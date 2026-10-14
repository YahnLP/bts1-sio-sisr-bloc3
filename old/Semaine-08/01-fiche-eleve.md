---
author: YLP
title: 📚 FICHE DE COURS
---

# 📚 FICHE DE COURS ÉLÈVE
## "RGPD Module 4 · Travail et Données Personnelles"

*Version 1.0 — BTS SIO SISR — Année 1 — Semaine 8*

---

## 🎯 Compétences Travaillées

| **Code** | **Compétence** |
|----------|---------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base |
| **B3.3** | Gérer les incidents de sécurité |

---

## PARTIE I — Données Personnelles dans le Monde du Travail

### I.A. Quelles Données l'Employeur Collecte-t-il ?

```
   DONNÉES RH — CYCLE DE VIE DU SALARIÉ
   ═══════════════════════════════════════════════════════════════

   RECRUTEMENT
   ──────────────────────────────────────────────────────────────
   Données collectées :
   • CV : nom, prénom, adresse, email, téléphone, formation, expériences
   • Photo (facultative, ne peut pas être exigée)
   • Entretien : notes, appréciations
   • Tests : résultats, évaluations

   Durée de conservation :
   • Candidat recruté → Données intégrées au dossier salarié
   • Candidat non retenu → 2 ans maximum (CNIL)
   • ⚠️ Conserver un CV 5 ans "au cas où" = violation RGPD

   DONNÉES INTERDITES lors du recrutement :
   ❌ Origine ethnique ou nationalité (sauf poste l'exigeant)
   ❌ Situation familiale, grossesse
   ❌ Opinion politique, conviction religieuse
   ❌ État de santé (sauf médecine du travail)
   ❌ Orientation sexuelle

   PENDANT LE CONTRAT
   ──────────────────────────────────────────────────────────────
   Données légitimes :
   • État civil, coordonnées, RIB
   • Contrat de travail, salaire
   • Absences, congés, arrêts maladie (médecin du travail uniquement)
   • Formations suivies, évaluations annuelles
   • Données de badgeage / pointage

   Données de surveillance (encadrées) :
   • Logs informatiques (navigation, emails pro)
   • Géolocalisation (véhicules de service)
   • Vidéosurveillance (zones autorisées uniquement)

   FIN DU CONTRAT
   ──────────────────────────────────────────────────────────────
   Données conservées :
   • Dossier salarié : 5 ans après fin de contrat (Code du travail)
   • Fiches de paie : 5 ans
   • Données comptables (salaires) : 10 ans
   • Accès informatiques → Désactivation IMMÉDIATE (jour même)
   • Email pro → Redirection 6 mois maximum
```

---

### I.B. Surveillance des Salariés : Ce qui est Autorisé

**Principe fondamental :** Toute surveillance doit être **proportionnée, légitimement justifiée et transparente**.

```
   TABLEAU SURVEILLANCE : AUTORISÉ / INTERDIT
   ═══════════════════════════════════════════════════════════════

   SURVEILLANCE      │ AUTORISÉ SI...              │ INTERDIT
   ──────────────────┼─────────────────────────────┼─────────────────
   Logs navigation   │ ✅ Salariés informés         │ ❌ À leur insu
   web               │ ✅ Charte informatique        │ ❌ Sites perso
                     │ ✅ Audit ponctuel             │    bloqués sans
                     │                             │    avertissement
   ──────────────────┼─────────────────────────────┼─────────────────
   Emails pro        │ ✅ Salariés informés          │ ❌ Emails marqués
                     │ ✅ Charte informatique        │    "Personnel"
                     │ ✅ Si enquête sur incident    │ ❌ Lecture en
                     │                             │    temps réel
   ──────────────────┼─────────────────────────────┼─────────────────
   Keylogger /       │ ❌ JAMAIS autorisé           │ ❌ Toujours
   enregistrement    │   (surveillance excessive)   │    interdit
   frappe clavier    │                             │
   ──────────────────┼─────────────────────────────┼─────────────────
   Géolocalisation   │ ✅ Véhicule de service        │ ❌ Temps perso
   véhicule          │ ✅ Sécurité / optimisation   │    (week-end)
                     │ ✅ Salariés informés          │ ❌ Contrôle des
                     │                             │    pauses
   ──────────────────┼─────────────────────────────┼─────────────────
   Logiciel de       │ ✅ Si proportionné            │ ❌ Surveillance
   monitoring PC     │ ✅ Salariés informés          │    permanente
   (temps actif,     │ ✅ Charte informatique        │    de chaque
   apps utilisées)   │                             │    action
   ──────────────────┼─────────────────────────────┼─────────────────
   Écoute appels     │ ✅ Formation / qualité        │ ❌ À l'insu
   téléphoniques     │ ✅ Salariés informés          │    des salariés
                     │ ✅ Nombre limité              │
```

---

### I.C. La Charte Informatique

**Outil clé pour encadrer l'usage du SI et la surveillance :**

```
   QU'EST-CE QUE LA CHARTE INFORMATIQUE ?
   ═══════════════════════════════════════════════════════════════

   DÉFINITION
   ──────────────────────────────────────────────────────────────
   Document officiel définissant les règles d'usage du système
   informatique dans l'entreprise.

   CONTENU TYPE
   ──────────────────────────────────────────────────────────────
   ① Ressources informatiques autorisées (PC, téléphone, internet)
   ② Usages personnels tolérés (navigation perso limitée)
   ③ Données personnelles de l'entreprise (confidentialité)
   ④ Moyens de surveillance mis en place (TRANSPARENCE RGPD)
      → "Les logs de navigation sont conservés 1 an"
      → "Les emails professionnels peuvent être consultés"
   ⑤ Sanctions en cas de violation

   VALEUR JURIDIQUE
   ──────────────────────────────────────────────────────────────
   ✅ Annexée au règlement intérieur → Opposable aux salariés
   ✅ Signée à l'embauche → Preuve de l'information
   ✅ Protège l'employeur et le technicien IT

   RÔLE DU TECHNICIEN IT
   ──────────────────────────────────────────────────────────────
   • Participer à la rédaction (aspects techniques)
   • S'assurer que les outils de surveillance décrits sont conformes
   • Mettre en œuvre uniquement ce qui est prévu dans la charte
```

---

### I.D. Messagerie Professionnelle

**Jurisprudence clé : L'arrêt Nikon (Cour de cassation, 2 octobre 2001)**

```
   ARRÊT NIKON — PRINCIPE FONDATEUR
   ═══════════════════════════════════════════════════════════════

   FAITS : Un salarié Nikon avait envoyé des emails personnels
   depuis son PC professionnel. L'employeur les avait lus.

   DÉCISION : La Cour de cassation a affirmé que :

   "Le salarié a droit, même au temps et au lieu de travail,
   au respect de l'intimité de sa vie privée."

   → Les emails marqués "Personnel" ou "Privé" ne peuvent
     PAS être lus par l'employeur, même sur PC professionnel.

   → Les autres emails PRO peuvent être consultés
     (mais salariés informés via charte).

   RÈGLES PRATIQUES
   ──────────────────────────────────────────────────────────────
   ✅ Email marqué "Personnel" → Inviolable
   ✅ Dossier "Perso" dans la messagerie → Inviolable
   ✅ Emails pro → Accessibles (employeur informé au préalable)
   ❌ Lecture systématique en temps réel → Excessive
   ❌ Interception des mots de passe → Toujours illicite
```

---

## PARTIE II — Vidéosurveillance : Cadre Légal Complet

### II.A. Définitions et Distinctions

```
   VIDÉOSURVEILLANCE vs VIDÉOPROTECTION
   ═══════════════════════════════════════════════════════════════

   VIDÉOSURVEILLANCE (privée — RGPD)
   ──────────────────────────────────────────────────────────────
   Caméras installées dans des lieux PRIVÉS ou à USAGE PROFESSIONNEL
   • Locaux d'entreprise
   • Commerces, magasins
   • Parkings privés
   • Entrepôts, usines

   Réglementation : RGPD + CNIL
   Autorité : CNIL

   VIDÉOPROTECTION (publique — Code séc. intérieure)
   ──────────────────────────────────────────────────────────────
   Caméras installées sur la VOIE PUBLIQUE
   • Rues, places, transports en commun
   • Abords d'établissements scolaires
   • Installations sensibles (aéroports, gares)

   Réglementation : Code de la sécurité intérieure (CSI)
   Autorisation : Préfet de département
   Autorité : Commission départementale + CNIL
```

---

### II.B. Règles Fondamentales de la Vidéosurveillance en Entreprise

```
   10 RÈGLES OBLIGATOIRES (RGPD + CNIL)
   ═══════════════════════════════════════════════════════════════

   ① FINALITÉ LÉGITIME
   ──────────────────────────────────────────────────────────────
   Finalités autorisées :
   ✅ Sécurité des personnes (prévention agressions)
   ✅ Protection des biens (prévention vols)
   ✅ Contrôle des accès (entrées/sorties)
   ✅ Surveillance de zones dangereuses (machinerie lourde)

   Finalités INTERDITES :
   ❌ Surveiller le travail des salariés en permanence
   ❌ Contrôler leur productivité à la seconde
   ❌ Surveiller les représentants du personnel

   ② ZONES AUTORISÉES ET INTERDITES
   ──────────────────────────────────────────────────────────────
   AUTORISÉ de filmer :
   ✅ Entrées et sorties des bâtiments
   ✅ Zones de caisse (prévention vols)
   ✅ Zones de stockage de valeurs (coffres, entrepôts)
   ✅ Parking privé
   ✅ Couloirs, halls d'accueil

   INTERDIT de filmer :
   ❌ Toilettes, vestiaires
   ❌ Locaux syndicaux
   ❌ Salle de repos / cafétéria
   ❌ Poste de travail individuel (surveillance permanente)
   ❌ Bureau d'un salarié (sans justification exceptionnelle)

   ③ DURÉE DE CONSERVATION MAXIMALE : 30 JOURS
   ──────────────────────────────────────────────────────────────
   Les enregistrements doivent être supprimés après 30 jours.

   EXCEPTIONS :
   ✅ Réquisition judiciaire (en cas de plainte) → Conservation prolongée
   ✅ Incident constaté → Extraire l'enregistrement avant purge

   OBLIGATION TECHNIQUE DU TECHNICIEN IT :
   → Configurer la purge automatique à 30 jours
   → Documenter la configuration dans le registre RGPD

   ④ INFORMATION OBLIGATOIRE DES PERSONNES FILMÉES
   ──────────────────────────────────────────────────────────────
   AFFICHAGE VISIBLE à chaque entrée de zone filmée :
   ┌─────────────────────────────────────┐
   │  📷 Vidéosurveillance               │
   │  Locaux sous vidéosurveillance      │
   │  Responsable : [Nom/Entreprise]     │
   │  Contact : [email/téléphone]        │
   │  Conservation : 30 jours maximum    │
   │  Droit d'accès : [contact RGPD]     │
   └─────────────────────────────────────┘

   SALARIÉS : Information supplémentaire obligatoire
   → Via charte informatique, règlement intérieur, note de service

   ⑤ ACCÈS AUX ENREGISTREMENTS — PERSONNES HABILITÉES
   ──────────────────────────────────────────────────────────────
   ✅ Direction, responsable sécurité
   ✅ Forces de l'ordre (sur réquisition)
   ✅ La personne filmée (droit d'accès RGPD)
   ❌ Tout le monde (accès public interdit)
   ❌ N'importe quel salarié

   ⑥ ENREGISTREMENT EN TEMPS RÉEL
   ──────────────────────────────────────────────────────────────
   ✅ Visualisation en temps réel autorisée (sécurité)
   ✅ Enregistrement autorisé (dans la limite 30 jours)
   ❌ Streaming public (diffusion des images sur internet)

   ⑦ INFORMATION DE LA CNIL (si ≥ 50 salariés)
   ──────────────────────────────────────────────────────────────
   Les organismes publics et grandes entreprises doivent avoir
   un DPO désigné (qui gère le registre des traitements incluant
   la vidéosurveillance).

   ⑧ INFORMATION DES REPRÉSENTANTS DU PERSONNEL
   ──────────────────────────────────────────────────────────────
   ✅ CSE (Comité Social et Économique) doit être informé et consulté
   AVANT l'installation d'un système de vidéosurveillance.

   ⑨ ANALYSE D'IMPACT (AIPD) si surveillance étendue
   ──────────────────────────────────────────────────────────────
   Si le système couvre de nombreux espaces ou concerne
   de nombreuses personnes → AIPD obligatoire avant installation.

   ⑩ PAS DE MICRO
   ──────────────────────────────────────────────────────────────
   ❌ Les caméras NE PEUVENT PAS enregistrer le son
   (violation du secret des conversations)
   Exception : Urgences graves (sur autorisation)
```

---

### II.C. Rôle Pratique du Technicien IT

```
   CHECKLIST INSTALLATION VIDÉOSURVEILLANCE CONFORME
   ═══════════════════════════════════════════════════════════════

   AVANT L'INSTALLATION
   ──────────────────────────────────────────────────────────────
   ☐ Vérifier que la finalité est légitime (pas surveiller les salariés)
   ☐ Cartographier les zones à filmer (éviter zones interdites)
   ☐ Consulter le CSE (représentants du personnel)
   ☐ Vérifier si AIPD nécessaire

   LORS DE L'INSTALLATION
   ──────────────────────────────────────────────────────────────
   ☐ Orienter les caméras uniquement vers zones autorisées
   ☐ Vérifier l'absence de micro actif (audio désactivé)
   ☐ Configurer la conservation : 30 jours maximum
   ☐ Configurer la purge automatique (task scheduler / cron)
   ☐ Restreindre les accès (droits limités aux personnes habilitées)
   ☐ Activer les logs d'accès au système

   APRÈS L'INSTALLATION
   ──────────────────────────────────────────────────────────────
   ☐ Installer les panneaux d'affichage à chaque entrée de zone
   ☐ Mettre à jour le registre des traitements RGPD
   ☐ Informer les salariés (note de service + charte info)
   ☐ Documenter la configuration (rapport technique)
   ☐ Planifier un test de la purge automatique

   MAINTENANCE
   ──────────────────────────────────────────────────────────────
   ☐ Vérifier régulièrement la purge automatique
   ☐ Mettre à jour les firmwares des caméras
   ☐ Revue annuelle des accès
   ☐ Vérifier la conformité si nouvelles caméras ajoutées
```

---
