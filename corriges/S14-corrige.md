# Corrigé S14

## Partie A

Les équipements personnels vont dans une zone à part (ou le Wi-Fi invités) avec accès limité aux services publiés, jamais au réseau des serveurs. Éléments attendus du schéma : Internet → pare-feu → **DMZ** (serveur web) ; **LAN** postes ; **Serveurs** (fichiers, base) ; **Administration** (poste d'administrateur) ; **Wi-Fi invités** ​isolé ; **Imprimantes** dans une zone dédiée ; **VPN** qui aboutit au pare-feu avec des droits limités.

Matrice (exemple) :

| De ↓ / Vers → | Internet | DMZ (web) | Serveurs | Administration | Imprimantes |
|---|---|---|---|---|---|
| **Internet** | — | 443 | Non | Non | Non |
| **Postes (LAN)** | 80, 443 | 443 | 445 (fichiers) | Non | 9100, 631 |
| **Wi-Fi invités** | 80, 443 | Non | Non | Non | Non |
| **Télétravail (VPN)** | — | Non | 445 (fichiers) | Non | Non |
| **DMZ (web)** | mises à jour | — | 3306 (base) | Non | Non |
| **Administration** | Oui | 22 | 22 | — | 443 |

3. Zone **Serveurs** internes ; seul le **serveur web** (port 3306 par exemple) et l'administration peuvent lui parler. Jamais Internet ni les postes.
4. Zone isolée, avec uniquement ​Internet (DNS, web).
5. Il reste dans la DMZ ; il atteint la **base** sur le seul port autorisé, ce qui est un risque : d'où le moindre privilège du compte de base (S04), la journalisation et la détection (S15). Il ne peut pas joindre les postes ni l'administration.
6. **Tout ​refuser** (*deny all*) : seul ce qui est listé est autorisé.

## Partie B

7. Typiquement SSH (22) et éventuellement d'autres services installés par défaut ; chaque service non nécessaire doit être arrêté.
8. Valeur propre à chaque VM : on la note pour comparer avant/après, pas pour la comparer à une valeur type.
9. Exemples : authentification SSH, ​absence de pare-feu actif, paquets non à jour, durcissement du noyau, fichiers d'audit absents.

## Partie C

10. Une erreur dans le fichier peut empêcher `sshd` de redémarrer, donc **couper tout accès distant**. `sshd -t` vérifie la syntaxe sans toucher au ​service.
11. Sans mot de passe accepté, la **force brute** et le **bourrage d'identifiants** ne fonctionnent plus : il faut posséder la clé privée.
12. `~/.ssh/id_lab` (droits 600). On la protège par une **phrase secrète** (`ssh-keygen` la demande) et un agent (`ssh-agent`).
13. Sinon le pare-feu bloquerait la ​session SSH en cours ou les suivantes, et on perdrait l'accès au serveur.
14. Aucune réponse (« filtré ») : le pare-feu **jette** le paquet, ce qui ralentit un scan. « Fermé » renvoie un refus explicite.
15. `sudo ufw allow from 192.168.56.0/24 to any port 443 proto tcp`
16. Exemples : `avahi-daemon` (découverte ​réseau), `cups` (impression) : non nécessaires sur un serveur, donc surface d'attaque en moins.
17. Les correctifs de sécurité arrivent vite, sans intervention. Risque : une mise à jour qui casse un service. On le limite avec un lot **test** avant production, une sauvegarde/snapshot, et en n'automatisant que les ​mises à jour de **sécurité**.
18. En général, oui ; les suggestions restantes concernent des points de contexte (partitions séparées, durcissement du noyau, etc.).
19. Un score mesure la conformité à une liste, pas la **sécurité réelle** : certaines ​mesures peuvent être inadaptées au contexte. On vise le **risque réduit**, avec des écarts **documentés**.
20. Exemple : « SSH : mot de passe et root désactivés (fichier 10-durcissement.conf) pour supprimer la force brute. Retour arrière : supprimer le fichier, `sudo systemctl reload ssh`. Pare-feu : refus par défaut, SSH ouvert depuis `adm` ; retour : `sudo ufw disable`. »

## Partie D

Attendu : seuls les ports nécessaires ; `passwordauthentication no`, `permitrootlogin no` ; `Status: active` ; service des ​mises à jour automatique actif.
