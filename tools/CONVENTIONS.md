# Conventions de rédaction du site (à relire avant toute modification)

1. **Tout changement de contenu est validé par l'enseignant** avant publication sur `main`.
2. **Gabarit d'une séance** (`docs/phase-N-nom/Sxx-nom/`) : `README.md` (fiche séance), `01-cours.md` (et `01b-…` si le cours a plusieurs parties), `02-tp.md` (et `02b-…`), `03-aide-memoire.md`, annexes `annexe-….md`, dossier `tp/` (ressources du TP : configurations, fichiers `.json` du simulateur). Les images vont dans `docs/images/`.
3. **Principes d'un TP :** « But » et « Contraintes » ; **« J'anticipe »** avant chaque manipulation ; commandes données quand on ne peut pas les deviner, toujours accompagnées d'un **« Je comprends »** ; questions « pourquoi » ; **bilan final** rattaché aux compétences du référentiel du BTS SIO SISR (page `docs/ressources/referentiel.md`). Un TP de sécurité s'appuie sur des **machines virtuelles de laboratoire** isolées ; le simulateur réseau et Packet Tracer ne servent qu'à comprendre et s'entraîner.
4. **Réponses :** les blocs `<details><summary>Voir la réponse</summary>` (ou « Éléments de réponse ») deviennent des zones de réponse manuscrites à l'export PDF. Les blancs `______` et les cellules vides de tableau deviennent des cases à remplir. Les « Notes pour l'enseignant » ne sont pas imprimées.
5. **Titres :** pas d'emoji dans les titres de la nouvelle structure.
6. **Corrigés :** dans `corriges/` à la racine, hors du dossier `docs/` (non publiés sur le site).
7. **Licences :** documents en CC BY-NC-SA 4.0. Toute licence d'outil tiers non vérifiée est marquée « à vérifier » dans `docs/ressources/licences.md` ; n'en inventer aucune. Les outils cités sont détectés par mots-clés dans `docs/xtra/extra.js` (tableau `TOOLS`).
8. **Contenu technique :** ne rien affirmer qu'on n'a pas vérifié ; signaler les doutes dans le texte (encadré ou « Notes pour l'enseignant »).
9. **Compétences :** codes uniquement via `docs/ressources/referentiel.md` (page à vérifier sur le texte officiel).
10. **Simulateurs :** le simulateur réseau est celui du dépôt bloc 2 (lien dans `docs/ressources/outils.md`). Packet Tracer est cité sans être distribué (licence Cisco). Une séance ne dépend jamais d'un seul outil propriétaire.
11. **Vérification avant commit :** `mkdocs build --strict` doit passer.
12. **Numérotation :** les séances sont numérotées S01 à S19, avec une colonne « Semaine » (01 à 19) sans date : les 19 semaines d'alternance sont réparties sur l'année et ne sont pas consécutives.
13. **Mots de passe de TP :** les identifiants communs d'un TP sont des identifiants de laboratoire (environnement contrôlé, identiques pour toute la classe). Ils ne sont jamais repris dans une réalisation présentée à l'épreuve.
14. **Régénérer le glossaire :** `python3 scripts/gen_glossaire.py` produit `docs/ressources/glossaire.md` et `includes/abbr.md` à partir de `scripts/glossaire_data.py`.

15. **Cybersécurité :** aucun TP n'invite à attaquer un système qui n'est pas le laboratoire ; les statistiques et coûts chiffrés ne sont cités qu'avec leur source et leur année ; les cas réels sont distingués des cas fictifs (les cas fictifs sont annoncés comme tels). L'épreuve du bloc 3 est l'**E7** (écrite, 4 h).
