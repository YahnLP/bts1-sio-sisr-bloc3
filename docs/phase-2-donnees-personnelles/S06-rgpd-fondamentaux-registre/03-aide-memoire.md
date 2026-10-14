# Aide-mémoire – RGPD : notions, acteurs et principes

*BTS SIO SISR 1re année – Bloc 3 – S06*

> Un mot ou un sigle inconnu ? Passe la souris dessus, ou ouvre le [glossaire](../../ressources/glossaire.md).

## Notions

| Terme | À retenir |
|---|---|
| Donnée personnelle | Identifie une personne, **directement ou indirectement** (IP comprise) |
| Donnée sensible | Santé, origine, opinions, religion, syndicat, génétique, biométrie, vie sexuelle : **interdite sauf exception** |
| Traitement | **Toute opération** sur des données |
| Responsable | Décide **finalités et moyens** |
| Sous-traitant | Traite **pour le compte** du responsable (contrat, article 28) |
| DPO | Conseille et contrôle ; obligatoire dans certains cas |

## Les sept principes (article 5)

1. Licéité, loyauté, transparence
2. Limitation des **finalités**
3. **Minimisation**
4. **Exactitude**
5. Limitation de la **conservation**
6. **Intégrité et confidentialité**
7. **Responsabilité** : démontrer la conformité

## Registre des traitements (article 30)

Pour chaque traitement : **finalité · base légale · personnes · données · destinataires · transferts hors UE · durée · mesures de sécurité**.

## Sanctions

CNIL : jusqu'à **20 M€ ou 4 % du chiffre d'affaires mondial** (10 M€ ou 2 % pour d'autres manquements), mises en demeure, limitation ou interdiction.

## Chercher des données personnelles (labo)

| Cible | Commande |
|---|---|
| Courriels | `grep -rEoh '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}' dossier` |
| Téléphones | `grep -rEn '(\+33 ?\|0)[1-9]([ .]?[0-9]{2}){4}' dossier` |
| IBAN | `grep -rEn 'FR[0-9]{2}( ?[0-9A-Z]{4}){5} ?[0-9A-Z]{3}' dossier` |
| Mots-clés | `grep -rEil 'mot1\|mot2' dossier` |

> [!WARNING]
> Ces recherches se font **dans un dossier de laboratoire** ou dans le cadre d'une mission autorisée. Les motifs ne trouvent pas les noms de personnes.
