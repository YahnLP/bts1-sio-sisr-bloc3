---
author: YLP
title: 🖥️ FICHE TP
---

# 🖥️ TP — DEMANDE DE DROIT D'ACCÈS + RÉDACTION MENTIONS

*Durée : 30 minutes — Individuel*

---

## Exercice 1 — Traiter une Demande de Droit d'Accès (15 min)

**Contexte :**
Vous êtes technicien IT chez **CycloShop**, un site de vente de vélos en ligne.

Vous recevez cet email le 3 mars 2024 :

```
De : sophie.martin@gmail.com
À : rgpd@cycloshop.fr
Objet : Demande d'accès à mes données personnelles

Madame, Monsieur,

Conformément à l'article 15 du RGPD, je souhaite exercer mon
droit d'accès aux données personnelles me concernant.

Pourriez-vous m'indiquer quelles données vous détenez sur moi
ainsi que les informations sur leur traitement ?

Cordialement,
Sophie Martin
```

**Données disponibles dans le système :**

```sql
-- Résultat de la requête :
users : id=4521, prenom="Sophie", nom="Martin",
        email="sophie.martin@gmail.com",
        date_inscription="2022-06-14",
        adresse="12 rue des Lilas, 69003 Lyon"

orders : 3 commandes (2022, 2023, 2024)
         Total dépensé : 847 €

newsletter_prefs : abonnée=true, dernière_ouverture="2024-02-10"
```

**Mission :**

```
A. Vérifiez-vous l'identité de Sophie avant de répondre ?
   ☐ Oui, car elle est abonnée à la newsletter
   ☐ Non, l'email suffit
   ☐ Oui, si la demande concerne des données très sensibles

   Justification : ________________________________________

B. Quel est le délai de réponse maximum ?
   Date de réception : 3 mars 2024
   Date limite de réponse : ________________________________

C. Rédigez l'email de réponse complet (minimum 10 lignes)
──────────────────────────────────────────────────────────────

De     : rgpd@cycloshop.fr
À      : sophie.martin@gmail.com
Objet  : [À compléter]

[Rédigez la réponse complète]
______________________________________________________________
______________________________________________________________
______________________________________________________________
______________________________________________________________
______________________________________________________________
______________________________________________________________
______________________________________________________________
______________________________________________________________

D. Dans quel format fournirez-vous les données ? Pourquoi ?
──────────────────────────────────────────────────────────────
Format choisi : ☐ PDF  ☐ CSV  ☐ JSON  ☐ Tableau Word

Justification : ________________________________________
```

---

## Exercice 2 — Rédiger les Mentions d'Information (15 min)

**Contexte :**
CycloShop vous demande de rédiger les **mentions d'information** pour leur **nouveau formulaire d'inscription newsletter**.

**Données collectées :** Prénom, Email
**Finalité :** Envoi d'une newsletter mensuelle sur les promotions
**Base légale :** Consentement
**Conservation :** 3 ans sans activité (ou jusqu'au désabonnement)
**Hébergeur :** OVH (France)
**Responsable :** CycloShop SAS, 45 av. du Vélo, 75011 Paris

**Rédiger :**

```
A. Mention courte (2-3 lignes) à afficher sous le formulaire :
──────────────────────────────────────────────────────────────
_______________________________________________________________
_______________________________________________________________
_______________________________________________________________

B. La case de consentement doit-elle être pré-cochée ?
   ☐ Oui, pour simplifier l'inscription
   ☐ Non, car le consentement doit être actif et univoque

C. Le formulaire doit-il avoir un lien vers la politique de
   confidentialité complète ?
   ☐ Oui  ☐ Non — Justification : _________________________

D. Rédigez le texte du bouton et de la case à cocher :
   Bouton : [______________________________________________]
   Case   : [______________________________________________]
```

---
