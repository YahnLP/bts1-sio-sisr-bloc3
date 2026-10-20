# Annexe – Cas InnoTech (fictif) : dossiers, groupes et besoins

*BTS SIO SISR 1re année – Bloc 3 – S04 – support du [TP](02-tp.md)*

> [!NOTE]
> **InnoTech SARL** est une entreprise **fictive** : PME de services numériques de 30 salariés. Toute ressemblance avec une organisation réelle est fortuite.

## Les dossiers du serveur de fichiers

<figure class="graphe diagramme"><svg viewBox="0 0 510 280" style="max-width:510px" role="img" aria-label="Dossiers du serveur de fichiers de l&#x27;entreprise" xmlns="http://www.w3.org/2000/svg">
<line x1="26" y1="34" x2="26" y2="55" class="dg-line"/>
<line x1="26" y1="55" x2="50" y2="55" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="89" class="dg-line"/>
<line x1="26" y1="89" x2="50" y2="89" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="123" class="dg-line"/>
<line x1="26" y1="123" x2="50" y2="123" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="157" class="dg-line"/>
<line x1="26" y1="157" x2="50" y2="157" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="191" class="dg-line"/>
<line x1="26" y1="191" x2="50" y2="191" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="225" class="dg-line"/>
<line x1="26" y1="225" x2="50" y2="225" class="dg-line"/>
<line x1="26" y1="34" x2="26" y2="259" class="dg-line"/>
<line x1="26" y1="259" x2="50" y2="259" class="dg-line"/>
<rect x="12" y="8" width="146" height="26" rx="6" class="dg-dark"/>
<text x="85.0" y="26" text-anchor="middle" class="dg-w">\\SERVEUR\Data\</text>
<rect x="50" y="42" width="90" height="26" rx="6" class="dg-box"/>
<text x="95.0" y="60" text-anchor="middle" class="dg-t">Clients\</text>
<text x="150.0" y="60" text-anchor="start" class="dg-i">contrats, fiches clients, devis</text>
<rect x="50" y="76" width="90" height="26" rx="6" class="dg-box"/>
<text x="95.0" y="94" text-anchor="middle" class="dg-t">Projets\</text>
<text x="150.0" y="94" text-anchor="start" class="dg-i">code source, documentation technique</text>
<rect x="50" y="110" width="50" height="26" rx="6" class="dg-box"/>
<text x="75.0" y="128" text-anchor="middle" class="dg-t">RH\</text>
<text x="110.0" y="128" text-anchor="start" class="dg-i">contrats des salariés, bulletins de paie, évaluations</text>
<rect x="50" y="144" width="130" height="26" rx="6" class="dg-box"/>
<text x="115.0" y="162" text-anchor="middle" class="dg-t">Comptabilite\</text>
<text x="190.0" y="162" text-anchor="start" class="dg-i">bilans, factures, relevés bancaires</text>
<rect x="50" y="178" width="106" height="26" rx="6" class="dg-box"/>
<text x="103.0" y="196" text-anchor="middle" class="dg-t">Direction\</text>
<text x="166.0" y="196" text-anchor="start" class="dg-i">procès-verbaux, plans stratégiques, budgets</text>
<rect x="50" y="212" width="50" height="26" rx="6" class="dg-box"/>
<text x="75.0" y="230" text-anchor="middle" class="dg-t">IT\</text>
<text x="110.0" y="230" text-anchor="start" class="dg-i">configurations réseau, scripts, documentation d&#x27;infrastructure</text>
<rect x="50" y="246" width="98" height="26" rx="6" class="dg-box"/>
<text x="99.0" y="264" text-anchor="middle" class="dg-t">Archives\</text>
<text x="158.0" y="264" text-anchor="start" class="dg-i">documents de plus de 5 ans, en lecture seule</text>
</svg>
<figcaption>Sept dossiers de premier niveau, chacun avec ses propres besoins d&#x27;accès.</figcaption>
</figure>

## Les groupes et leurs besoins métier

| Groupe | Effectif | Missions | Besoins d'accès exprimés |
|---|---|---|---|
| `G_Commercial` | 5 | Relation clients, devis, contrats | Clients, Archives |
| `G_Comptable` | 2 | Facturation, paie, bilan | Comptabilité ; Clients (consultation) ; RH (données de paie seulement) |
| `G_DRH` | 1 | Gestion du personnel | RH |
| `G_Dev` | 8 | Développement logiciel | Projets |
| `G_Chef_Projet` | 3 | Pilotage, clients, technique | Clients, Projets, Archives |
| `G_Direction` | 2 | Stratégie, validation globale | Direction ; consultation des autres dossiers de gestion |
| `G_Admin_IT` | 2 | Infrastructure, sécurité, maintenance | IT ; journaux ; **sauvegarde** de l'ensemble |
| `G_Stagiaire` | 2 | Aide au développement | Projets (consultation) |

> [!WARNING]
> Les besoins « exprimés » sont **ceux que les équipes disent avoir**. Le travail d'un administrateur consiste aussi à les **questionner** : est-ce un besoin ou une habitude ?
