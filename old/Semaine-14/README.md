# 01 – Objectifs et ressources


---

## Informations Générales

| **Champ** | **Détail** |
|-----------|-----------|
| **Semaine** | S14 — Année 1 |
| **Bloc** | Bloc 3 — Cybersécurité des services informatiques |
| **Durée totale** | 4 heures |
| **Public** | Apprentis BTS SIO SISR — quatorzième semaine |
| **Modalité** | Présentiel — salle de cours + TP |
| **Prérequis** | S11 (cryptographie symétrique AES) · S13 (PKI, certificats X.509) · Notions réseau IP/routage |

---

## Compétences RNCP Visées

| **Code** | **Intitulé de la compétence** | **Niveau visé** |
|----------|-------------------------------|-----------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base | Maîtrise |
| **B3.5** | Mettre en œuvre des mécanismes de chiffrement | Maîtrise |
| **B3.7** | Configurer et administrer un VPN | Acquisition |

> 📌 **S14 BLOC 3 réunit deux sujets profondément liés.** Un VPN sans cryptographie asymétrique n'existe pas — les certificats X.509 (S13) et la cryptographie asymétrique sont le fondement de l'authentification VPN. La séance articule d'abord la théorie complète de la cryptographie asymétrique (complément de S11 et S13), puis montre concrètement comment elle s'applique dans l'architecture VPN.

---

## Objectifs Pédagogiques

**Chiffrement Asymétrique :**
- ✅ Maîtriser le principe **clé publique / clé privée** (usages distincts)
- ✅ Comprendre l'**échange de clé Diffie-Hellman** (et sa version ECDH)
- ✅ Comprendre le **chiffrement hybride** (asymétrique + symétrique)
- ✅ Relier les certificats X.509 (S13) au chiffrement asymétrique
- ✅ Identifier les usages concrets (TLS, SSH, GPG, email S/MIME)

**VPN :**
- ✅ Définir un **VPN** et expliquer le concept de **tunnelisation**
- ✅ Distinguer les **2 grands types** : Site-à-Site et Nomade (Remote Access)
- ✅ Comprendre les **protocoles VPN** (IPsec, OpenVPN, WireGuard, SSL/TLS)
- ✅ Identifier les **composants** d'une infrastructure VPN
- ✅ Comparer les **cas d'usage** et choisir le bon type de VPN
- ✅ Comprendre le rôle du **chiffrement** dans le VPN

---