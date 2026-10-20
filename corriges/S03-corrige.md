# Corrigé S03

## Partie A (hypothèse 10¹⁰ essais/s)

| Mot de passe | Entropie ≈ | Temps pour tout essayer ≈ |
|---|---|---|
| 6 chiffres | 20 bits | 0,0001 s |
| 10 minuscules | 47 bits | 26¹⁰ = 1,4 × 10¹⁴ ​essais, soit environ 4 heures |
| 10 caractères parmi 95 | 66 bits | 95¹⁰ = 6 × 10¹⁹ essais, soit environ 190 ans |
| 14 caractères parmi 62 | 83 bits | environ 39 millions d'années |
| 5 mots (7 776) | 65 bits | environ 90 ans |
| 7 mots (7 776) | 90 bits | environ 5 milliards d'années |

## Partie B : mots de passe en clair des comptes fictifs

| Compte | Mot de passe | Dans `dico.txt` ? |
|---|---|---|
| alice | `soleil` | oui |
| bruno | `azerty123` | oui |
| chloe | `motdepasse` | oui |
| david | `Football2008` | oui |
| emma | `N0uvelle-Voiture!` | non (17 caractères, non prévisible) |
| farid | `le-chat-dort-sur-le-canape-rouge` | non (phrase de passe longue) |

Résultat ​attendu : quatre comptes retrouvés en moins d'une seconde, deux restent sûrs.
