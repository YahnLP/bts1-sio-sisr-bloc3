# Corrigé S17

## Partie A

**Main courante (exemple)**

| Heure | Constat | ​Décision | Qui | Pourquoi |
|---|---|---|---|---|
| 08 h 10 | 3 postes avec message de rançon, fichiers `.locked` | Débrancher du réseau les postes touchés ; prévenir Mme Delmas | ​Pilote technique | Stopper la propagation |
| 08 h 25 | Pièce jointe ouverte dimanche soir | Isoler le portable de ce collaborateur (ne pas l'éteindre), conserver le courriel | Pilote | Cause probable, preuve |
| 08 h 40 | Serveur et NAS chiffrés ; USB de vendredi intact | Couper le serveur du réseau ; **ne pas brancher** le ​disque USB à un réseau infecté ; l'isoler | Pilote | Dernière sauvegarde saine |
| 09 h 10 | Menace de publication | Qualifier en violation de données ; alerter DPO ; préparer la ​notification | DPO | S08 |
| 09 h 40 | Client reçoit un courriel piégé | Prévenir les clients, bloquer l'envoi depuis le compte compromis | Communication | Éviter la propagation |
| 10 h 30 | Prestataire veut nettoyer | Refuser de nettoyer avant collecte ; suivre le plan | Responsable de crise | Préserver les preuves |
| 11 h 00 | Journaliste | Pas de ​commentaire technique ; message validé par la direction | Communication | Maîtriser la communication |

1. Rançongiciel avec **double extorsion** (chiffrement + menace de divulgation) : **disponibilité** atteinte (fichiers chiffrés) et **confidentialité** potentiellement atteinte (exfiltration).
2. Le NAS est chiffré : il n'est pas une ​sauvegarde fiable. Le disque USB de vendredi permettrait de restaurer (perte de la semaine : RPO de trois jours). Vérifier qu'il est sain (analyse sur un poste isolé, comparaison des fichiers) avant de l'utiliser ; ne le brancher qu'à un environnement propre.
3. Oui : c'est une **violation de données** si des ​données personnelles ont été copiées : documenter, **notifier la CNIL sous 72 h** (si risque), informer les personnes concernées si le risque est élevé, informer les clients du ​cabinet (qui sont aussi des responsables de traitement, le cabinet étant leur sous-traitant pour de nombreux traitements : prévenir les clients « dans les meilleurs délais »).
4. Arguments contre : aucune garantie de déchiffrement ni d'effacement des données ; finance les attaquants ; rançon peut ne pas régler la fuite ; les autorités déconseillent. Décision ​finale à la direction, après avis de l'assureur et des autorités ; une restauration est possible depuis la sauvegarde de vendredi.
5. Refuser : « nettoyer » détruirait les preuves, ​restaurer avant d'avoir éradiqué la cause (accès de l'attaquant) exposerait à une nouvelle attaque ; commencer par la collecte et l'analyse.
6. Notifications : CNIL oui, **72 h** (par la direction/DPO) ; clients oui, rapidement, par la direction ; assureur oui, **sous 48 h** selon le contrat ; police oui, plainte (direction) ; Cybermalveillance oui, pour assistance ; journaliste : réponse ​brève, validée par la direction.
7. Exemple : « Nous avons subi un incident informatique, nous avons pris les mesures nécessaires, déposé plainte et informé les autorités. Nous accompagnons nos clients. Aucune autre information ne peut être donnée à ce stade. »
8. Exemple : « Nous subissons un incident informatique. Si vous avez reçu un ​courriel de notre part contenant une pièce jointe depuis dimanche, ne l'ouvrez pas et supprimez-le. Nous vous recontactons par téléphone. »
9. Cause probable : courriel d'hameçonnage avec pièce jointe ouverte sur un poste. Prévention : ​sensibilisation (S01), protection du poste et filtrage des pièces jointes (S02), **sauvegarde hors ligne** et testée (S05), droits minimaux (S04), segmentation (S14), détection et journaux (S15), MFA (S03), mises à jour.
10. Ordre : isoler et collecter ; reconstruire/remettre à neuf le serveur et les postes touchés ; ​restaurer les données depuis la sauvegarde saine ; changer tous les mots de passe ; reconnecter progressivement avec surveillance ; vérifier l'intégrité des données restaurées ; reprendre l'activité.

## Partie B

11. Parce que les connexions et processus disparaissent à l'arrêt ou au redémarrage ; les journaux du disque, eux, persistent.
12. `sha256sum -c` indique `FAILED` pour `05-dernieres-connexions.txt` : l'intégrité n'est plus garantie, la ​pièce n'est plus utilisable comme preuve.
13. Sur un support externe (disque chiffré, serveur de preuves) : la machine analysée peut être compromise et ses ​fichiers modifiés par l'attaquant.
14. En **signant** le fichier `SHA256SUMS` avec une clé privée (S11) ou en le faisant horodater par un tiers.
15. Qui a collecté et remis ; la date et l'heure ; la description de la pièce (nom, empreinte, support).

## Partie C

Réponses libres. Exemples d'actions : sauvegardes hors ligne testées (responsable : prestataire, échéance 1 mois), formation anti-hameçonnage (associée, 2 mois), segmentation et pare-feu (prestataire, 3 mois), procédure d'incident et liste de contacts (associée, 1 mois).
