# 01 – Objectifs et ressources


## Informations Générales

| **Champ** | **Détail** |
|-----------|-----------|
| **Semaine** | S11 — Année 1 |
| **Bloc** | Bloc 3 — Cybersécurité des services informatiques |
| **Durée totale** | 4 heures |
| **Public** | Apprentis BTS SIO SISR — onzième semaine |
| **Modalité** | Présentiel — salle de cours + TP machines Linux/Windows |
| **Prérequis** | S3 (mots de passe, hachage) · S4 (chiffrement sauvegardes) |


---

## Compétences Visées


| **Code** | **Intitulé de la compétence** | **Niveau visé** |
|----------|-------------------------------|-----------------|
| **B3.2** | Mettre en œuvre les mesures de sécurité de base | Maîtrise |
| **B3.5** | Mettre en œuvre des mécanismes de chiffrement | Acquisition |

> 📌 **S11 BLOC 3 introduit la cryptographie — colonne vertébrale de toute la sécurité informatique.** HTTPS, VPN, TLS, chiffrement des sauvegardes, signature numérique : tout repose sur des algorithmes cryptographiques. Un technicien SISR qui ne comprend pas les fondements de la cryptographie ne peut pas sécuriser une infrastructure correctement. S11 pose les bases de la **cryptographie symétrique** — la plus rapide, la plus utilisée pour les données en masse.

---

## Objectifs Pédagogiques

**Cryptographie symétrique — Théorie :**
- ✅ Définir la **cryptographie** et ses objectifs (CIA + authenticité)
- ✅ Comprendre le **principe du chiffrement symétrique** (une clé = chiffrer + déchiffrer)
- ✅ Distinguer **chiffrement par bloc** et **chiffrement par flux**
- ✅ Maîtriser le fonctionnement d'**AES** (Advanced Encryption Standard)
- ✅ Comprendre les **modes opératoires** (ECB, CBC, CTR, GCM)
- ✅ Identifier le **problème de l'échange de clé** (limite du symétrique)

**TP — OpenSSL et GPG :**
- ✅ Chiffrer et déchiffrer un fichier avec **OpenSSL** (AES-256-CBC)
- ✅ Chiffrer et déchiffrer un fichier avec **GPG** (symétrique)
- ✅ Vérifier l'**intégrité** d'un fichier (hash SHA-256)
- ✅ Analyser la **différence de taille** fichier clair vs chiffré
- ✅ Comprendre l'importance du **mot de passe de déchiffrement**
