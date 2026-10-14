---
author: YLP
title: 📄 ANNEXE 2
---

# 📄 ANNEXE 2 — SCHÉMA CHAÎNE DE CONFIANCE

```
═══════════════════════════════════════════════════════════════
         HIÉRARCHIE PKI COMPLÈTE — DE LA ROOT AU SERVEUR
═══════════════════════════════════════════════════════════════

  TRUST STORE NAVIGATEUR / OS
  ┌─────────────────────────────────────────────────────────┐
  │ DigiCert │ Let's Encrypt │ Comodo │ GlobalSign │ ...     │
  │ (~150 Root CAs intégrées dans Chrome / Firefox / Windows│
  └────────────────────────┬────────────────────────────────┘
                           │ Fait confiance à
                           ▼
  ┌─────────────────────────────────────────────────────────┐
  │              ROOT CA — Hors ligne                        │
  │  Certificat auto-signé (Issuer = Subject)                │
  │  Validité : 20-25 ans                                    │
  │  Stockée dans un HSM dans un vault physique sécurisé     │
  │  Utilisée 1-2 fois par an pour signer les intermédiaires│
  └────────────────────────┬────────────────────────────────┘
                           │ Signe (annuellement)
                           ▼
  ┌─────────────────────────────────────────────────────────┐
  │           INTERMEDIATE CA — En ligne                    │
  │  Signée par la Root CA                                   │
  │  Validité : 5-10 ans                                     │
  │  Opérationnelle quotidiennement                          │
  │  Compromission : Révocable sans impact sur la Root       │
  └────────────────────────┬────────────────────────────────┘
                           │ Signe (en continu)
                           ▼
  ┌─────────────────────────────────────────────────────────┐
  │         CERTIFICAT FINAL (Leaf Certificate)             │
  │  www.banque.fr / www.exemple.fr / vpn.entreprise.fr      │
  │  CA:FALSE (ne peut pas signer d'autres certificats)      │
  │  Validité : 90 jours (Let's Encrypt) à 1 an             │
  │  Installé sur le serveur web / VPN / messagerie          │
  └─────────────────────────────────────────────────────────┘

  VALIDATION PAR LE NAVIGATEUR (de bas en haut)
  ──────────────────────────────────────────────────────────
  1. Le serveur envoie : Certificat final + Certificat(s) intermédiaire(s)
  2. Navigateur vérifie : Signature du cert final par l'intermédiaire ✓
  3. Navigateur vérifie : Signature de l'intermédiaire par la Root ✓
  4. Navigateur vérifie : Root est dans le trust store ✓
  5. Navigateur vérifie : Dates de validité ✓
  6. Navigateur vérifie : CN/SAN correspond au domaine ✓
  7. Navigateur vérifie : Certificats non révoqués (OCSP) ✓
  → 🔒 Cadenas vert

═══════════════════════════════════════════════════════════════
PKI EN ENTREPRISE (Active Directory Certificate Services)
──────────────────────────────────────────────────────────────
Root CA offline → Intermediate CA (AD CS) → Certificats :
  • Certificats serveurs internes (intranet, VPN)
  • Certificats clients (auth réseau 802.1X)
  • Certificats de signature (documents, emails)
  • Certificats machine (BitLocker, TPM)
Déploiement trust store : GPO → Tous les postes Windows reçoivent
automatiquement le certificat Root CA dans leur trust store.
═══════════════════════════════════════════════════════════════
```

---
