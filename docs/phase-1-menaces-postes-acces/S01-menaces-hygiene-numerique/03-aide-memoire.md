# Aide-mémoire – Menaces et hygiène numérique

*BTS SIO SISR 1re année – Bloc 3 – S01*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Les quatre principes

| Principe | Question |
|---|---|
| Disponibilité | Accessible quand on en a besoin ? |
| Intégrité | Exact et non modifié ? |
| Confidentialité | Lisible seulement par les personnes autorisées ? |
| Preuve | Peut-on prouver qui a fait quoi ? |

**Risque** = une menace qui exploite une vulnérabilité, avec une gravité et une vraisemblance. On **prévient**, on **limite**, ou on **accepte** en connaissance de cause.

## Devant un message suspect

1. **Ne pas cliquer**, ne pas ouvrir la pièce jointe.
2. Lire **l'adresse réelle** de l'expéditeur et **survoler** les liens.
3. Chercher la **pression** (urgence, menace, gain).
4. **Vérifier par un autre canal** (téléphone, site officiel saisi à la main).
5. **Signaler** au service informatique.

## Contrôles d'hygiène sur un poste Windows

| Contrôle | Commande PowerShell |
|---|---|
| Dernier correctif | `Get-HotFix \| Sort-Object InstalledOn -Descending \| Select-Object -First 5` |
| Antivirus | `Get-MpComputerStatus` |
| Pare-feu | `Get-NetFirewallProfile` |
| SMBv1 | `Get-SmbServerConfiguration \| Select-Object EnableSMB1Protocol` |
| Groupes du compte | `whoami /groups` |

## Rançongiciel : les parades

- **Prévenir** : mises à jour, droits limités, messages et pièces jointes contrôlés ;
- **Limiter** : segmentation, sauvegardes hors ligne ;
- **Réagir** : isoler la machine, ne pas payer sans conseil, préserver les preuves, restaurer.
