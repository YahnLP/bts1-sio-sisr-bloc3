# Corrigé S15

## Partie A

1. **18** échecs (16 + 2). **Deux** adresses : `203.0.113.50` (16) et `198.51.100.7` (2).
2. Ce sont des comptes très courants : les robots essaient une liste de noms classiques sans savoir lesquels existent ; `invalid user` montre que le compte n'existe pas.
3. Deux échecs puis un succès avec le **mot de passe** : peut être une erreur de frappe de l'utilisateur légitime, mais c'est une **adresse inconnue** qui se connecte par mot de passe : vérifier auprès de l'utilisateur, consulter les connexions habituelles (`192.0.2.10` utilise une clé), forcer le changement de mot de passe, activer le MFA ou l'authentification par clé.
4. `grep "Accepted" auth-lab.log | awk '{print $9, $11}'` (champs : utilisateur puis adresse source) ou `grep Accepted auth-lab.log` seul.
5. Bloquer l'adresse (pare-feu, Fail2ban), vérifier qu'aucun succès n'a eu lieu, désactiver le mot de passe SSH, alerter le responsable, conserver les journaux.

## Partie B

6. Une adresse bannie : `192.168.56.20` (l'adresse de `adm`).
7. Perdre l'accès d'administration au serveur au moment où l'on en a besoin. On l'évite avec `ignoreip` (liste blanche) et une console de secours.
8. Oui, en **usurpant** l'adresse d'un utilisateur ou en provoquant des échecs volontaires depuis son réseau : c'est un déni de service par bannissement. D'où la durée limitée et la liste blanche.
9. Non : chaque adresse ne fait que 1 ou 2 essais. Il faut l'authentification par **clé**, le **MFA**, des mots de passe forts (S03) et une détection sur l'ensemble.
10. L'authentification par clé supprime la possibilité de deviner un mot de passe ; le bannissement ne fait que limiter la vitesse des essais.

## Partie C

11. Exemple : `10/14/2026-09:12:03.123456  [**] [1:1000002:1] LAB - balayage de ports probable [**] {TCP} 192.168.56.20:44312 -> 192.168.56.10:80`.
12. Trop d'alertes sur du trafic normal (**faux positifs**) : les analystes arrêtent de les lire.
13. Passer en mode **en ligne** (NFQUEUE ou équivalent), changer l'action `alert` en `drop`. Risque : bloquer un trafic légitime ; coupure du service si le sondeur tombe.
14. Oui (scan « lent » ou distribué) : on ajoute des règles à seuil plus long, la corrélation dans un SIEM, et on réduit l'exposition (pare-feu : S14).

## Partie D

15. « Compte pour lequel l'ouverture de session a échoué » (nom du compte) et « Informations sur le réseau » (adresse source). Le type d'ouverture de session (2 interactive, 3 réseau, 10 distante) aide à interpréter.
16. 4624/4625 (connexions), 4720 (compte créé), 4732 (ajout à un groupe d'administration), 4740 (compte verrouillé), 1102 (journal effacé), 4672 (privilèges spéciaux).
17. Parce qu'un attaquant efface les journaux pour **cacher ses traces** : l'événement ne devrait presque jamais se produire en usage normal.
