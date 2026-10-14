# 01 – Objectifs et ressources


---

## Informations Générales

| **Champ** | **Détail** |
|-----------|-----------|
| **Semaine** | S13 — Année 1 |
| **Bloc** | Bloc 3 — Cybersécurité des services informatiques |
| **Durée totale** | 4 heures |
| **Public** | Apprentis BTS SIO SISR — treizième semaine |
| **Modalité** | Présentiel — salle de cours + TP machines Linux/Windows |
| **Prérequis** | S11 (cryptographie symétrique, AES, OpenSSL) · Notions de réseaux (HTTPS, TLS) |

---

## Compétences Visées

| **Code** | **Intitulé de la compétence** | **Niveau visé** |
|----------|-------------------------------|-----------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base | Maîtrise |
| **B3.5** | Mettre en œuvre des mécanismes de chiffrement | Maîtrise |
| **B3.6** | Administrer une infrastructure à clés publiques | Acquisition |

> 📌 **S13 est la séance qui fait enfin comprendre pourquoi le cadenas HTTPS apparaît dans un navigateur.** La PKI (Public Key Infrastructure) est l'une des infrastructures les plus fondamentales d'Internet — et pourtant l'une des moins comprises. Un technicien SISR qui ne maîtrise pas les certificats X.509 ne peut pas administrer un serveur web sécurisé, configurer un VPN, déployer de la messagerie chiffrée, ou gérer une CA d'entreprise. S13 donne les clés théoriques ET pratiques.

---

## Objectifs Pédagogiques

**Certificats et PKI — Théorie :**
- ✅ Comprendre le **problème de confiance** que résout la PKI
- ✅ Définir un **certificat numérique** et ses composants
- ✅ Maîtriser le **standard X.509** (champs, structure, extensions)
- ✅ Comprendre la **chaîne de confiance** (Root CA → Intermediate CA → Leaf)
- ✅ Distinguer les **types de certificats** (DV, OV, EV, wildcard, client)
- ✅ Comprendre le **cycle de vie** d'un certificat (demande, signature, révocation)
- ✅ Connaître les **mécanismes de révocation** (CRL, OCSP)

**TP OpenSSL :**
- ✅ Créer une **clé privée RSA** et **EC** avec OpenSSL
- ✅ Générer une **CSR** (Certificate Signing Request)
- ✅ Créer un **certificat auto-signé** (pour serveur de test)
- ✅ Créer une **mini-CA locale** (Root CA + certificat signé)
- ✅ **Inspecter** un certificat (lire les champs X.509)
- ✅ Déployer un certificat sur un **serveur HTTPS minimal**
