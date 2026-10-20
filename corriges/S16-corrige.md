# Corrigé S16

## Partie A

1. Pour éviter de toucher à des machines non autorisées (systèmes de production, voisins) : ce qui n'est pas ​explicitement inclus est exclu.
2. On **arrête**, on n'y touche pas, on **informe** le responsable du périmètre et on note le fait ; on ne la scanne pas sans nouvelle autorisation.
3. Le client n'est pas propriétaire de l'infrastructure de l'hébergeur : seul l'hébergeur peut autoriser un scan de ses systèmes.

## Partie B

4. `adm` et `srv` (et la passerelle si elle répond).
5. Typiquement `21/tcp` vsftpd, `22/tcp` OpenSSH, `80/tcp` nginx (versions affichées par `-sV`).
6. `Anonymous FTP login allowed`. N'importe qui peut lire (voire déposer) des fichiers sans compte.
7. Tous les ports (65 535) ​demandent beaucoup plus de temps ; on les scanne en audit complet, mais on commence par les ports courants quand le temps est limité.
8. ​Beaucoup de connexions refusées ou courtes dans `journalctl` ; des requêtes inhabituelles dans le journal d'accès de nginx : un scan est visible (S15).

## Partie C

| # | Problème | Référence | Gravité | Exposition | Valeur | Priorité |
|---|---|---|---|---|---|---|
| 1 | SMBv1 actif sur un serveur Windows 2012 R2 (fin de support) | CVE-2017-0144 | 8,1 élevé | LAN | Comptabilité : élevée | 2 |
| 2 | vsftpd 2.3.4 : version à porte ​dérobée | CVE-2011-2523 | 9,8 critique | LAN | Faible (à supprimer) mais point d'entrée | 1 |
| 3 | Telnet : mots de passe en clair | Mauvaise pratique | Élevée (pas de score) | LAN | ​Moyenne | 3 |
| 4 | MySQL 5.1 accessible depuis le réseau, fin de vie | Plusieurs CVE | Variable | LAN | Moyenne | 4 |
| 5 | Apache 2.2 en fin de vie | Plusieurs CVE | Variable | LAN | Faible | 5 |
| 6 | RDP ouvert sur le serveur de comptabilité | Bonne pratique : restreindre (VPN, MFA) | Moyenne | LAN | Élevée | 6 |
| 7 | VNC sur le poste de la directrice | Bonne pratique : mot de ​passe fort, restriction | Moyenne | LAN | Élevée (poste de direction) | 7 |
| 8 | Serveur web public : TLS fort, versions à jour | — | Aucun constat | Internet | Élevée | 8 (surveiller) |

9. (1) vsftpd 2.3.4 : critique, porte dérobée, accès immédiat ; (2) SMBv1 sur le serveur de comptabilité : très exploité par des ​rançongiciels ; (3) Telnet et FTP anonyme : confidentialité nulle. Tous sur le réseau interne, mais un poste infecté suffit.
10. **Désactiver SMBv1** (`Set-SmbServerConfiguration -EnableSMB1Protocol $false`) et **arrêter** Telnet/FTP : quelques minutes, sans investissement.
11. **Supprimer** la machine (la direction l'a déjà prévu) ou à défaut l'**isoler** dans un VLAN sans accès. Mettre à jour un système en fin de vie ne ​règle pas tout ; la suppression retire d'un coup tous les constats.
12. Un scan **authentifié** (versions exactes, correctifs, configuration) et un contrôle du poste directrice (VNC) ; les postes et mots de passe ne sont pas visibles d'un scan externe.
13. La bannière peut afficher une version sans correspondre au correctif réellement installé (certains systèmes rétroportent les correctifs de sécurité sans changer la ​version affichée) : on vérifie sur la machine (`apt list --installed`, `dpkg -l`, informations de correctifs).

## Partie D

14. Exemple : « L'audit a trouvé huit points ; trois sont urgents et concentrés sur un ancien serveur que vous comptiez supprimer : sa suppression règle l'essentiel. Le serveur du site web est bien configuré. »
15. Critique exposée : correction ou mesure de contournement **immédiate** (quelques ​jours au plus). Moyenne sur poste isolé : intégrer au cycle normal de mises à jour (quelques semaines), avec suivi.
