# Corrigé S02

## Partie A

Voir les « Éléments de réponse » du TP. Précisions : `Test-Path` renvoie `False` ; `Get-MpThreatDetection` affiche une ligne avec le nom de la menace (« Virus:DOS/EICAR_Test_File » ou équivalent) et le chemin du fichier. La détection est à **signature** (EICAR n'a aucun comportement).

## Partie B

| Élément | Valeur attendue |
|---|---|
| Moteurs détectant `notepad.exe` | **Aucun** ou presque (fichier légitime de Windows, très répandu). Les valeurs varient selon les moteurs et la date |
| Moteurs détectant EICAR | **Presque tous** (la grande majorité des moteurs reconnaissent le fichier de test) |
| CVE-2017-0144 | Note CVSS 3.x courante : **8,1** (élevée) ; vulnérabilité du protocole **SMBv1** de Microsoft Windows ; fiche publiée en **mars 2017** (à vérifier sur la base) |
| Produit concerné | Microsoft Windows (serveur SMB) |

L'empreinte SHA-256 officielle du fichier EICAR (68 octets) est publiée sur eicar.org : elle sert de **vérification** (à comparer à ce que donne `Get-FileHash` sur un fichier identique).

Question finale : voir les éléments de réponse du TP (exploitation observée, exposition, valeur des données, absence de segmentation).

## Partie C

1. Dépend de la VM. Exemples : `Confirm-SecureBootUEFI` → `False` ou erreur (BIOS) ; `Get-Tpm` → `TpmPresent : False` ; `manage-bde` → « Entièrement déchiffré » (BitLocker non activé). Chaque réponse doit être **expliquée** par la configuration de la VM.
2. Voir les éléments de réponse du TP.

**Politique de correctifs (exemple, à justifier)**

| Catégorie | Délai maximal | Test préalable | Qui valide | Remarque |
|---|---|---|---|---|
| Critique, machine **exposée** | 48 h (ou mesure de contournement immédiate) | Test rapide sur une machine pilote | Responsable informatique | Priorité absolue : serveur web exposé |
| Critique, machine interne | 7 jours | Groupe pilote de 3 à 5 postes | Responsable informatique | Redémarrage planifié en dehors des heures de travail |
| Importante | 30 jours | Groupe pilote | Technicien | Cycle mensuel de mises à jour |
| Faible | 90 jours ou prochain cycle | Aucun spécifique | Technicien | Regroupées avec les mises à jour fonctionnelles |
| Fin de support | Plan de migration | Test de compatibilité | Direction | Isoler en attendant (segmentation) |

(Ces délais sont des exemples d'exercice, pas des obligations légales.)
