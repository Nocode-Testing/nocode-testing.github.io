# Qualite logicielle

Ce dossier constitue le referentiel documentaire de qualite exploitable par un futur outil. Il ne remplace pas GitHub Issues ni les GitHub Projects : il apporte la tracabilite entre le besoin, les tests et leurs resultats.

## Arborescence

- `01-exigences/referentiel-exigences.md` : exigences validees et liens vers leurs US.
- `02-user-stories/` : une US Markdown par fichier, avec criteres Gherkin.
- `03-cas-de-test/` : cas de test reutilisables.
- `04-campagnes/` : campagnes preparant un ensemble de cas pour une version ou une recette.
- `05-executions/` : resultats d'execution des campagnes.
- `06-anomalies/` : index documentaire des anomalies GitHub.
- `traceabilite.md` : matrice REQ -> US -> CT -> CAMP -> EXEC.

## Identifiants

| Type | Format | Exemple |
|---|---|---|
| Exigence | `REQ-<numero>` | `REQ-001` |
| User story | `US-<numero>` | `US-001` |
| Cas de test | `CT-<numero>` | `CT-001` |
| Campagne | `CAMP-<numero>` | `CAMP-001` |
| Execution | `EXEC-<numero>` | `EXEC-001` |
| Anomalie | `ANOM-<numero>` | `ANOM-001` |

Les numeros sont sequentiels et ne sont pas reutilises. Les fichiers concrets commencent par leur identifiant, par exemple `US-001-slug-court.md`.

## Front matter minimal

Chaque element concret utilise un front matter YAML minimal :

```yaml
id: US-001
statut: brouillon
liens:
  requirements:
    - REQ-001
```

Le champ `id` et le champ `statut` sont obligatoires. Le champ `liens` contient les identifiants amont ou aval applicables. Aucun exemple ci-dessus ne represente un element cree.

## Gouvernance

Le commanditaire est le seul a valider une priorite, une exception et une promotion vers la production. Les agents peuvent uniquement proposer ces decisions et les documenter comme telles.

Aucune US d'interface ne peut etre creee ou declaree prete tant que le lot UI concerne n'a pas ete valide explicitement par le commanditaire. Les US nouvelles suivent la revue securite de Mina Cybersecurite, puis les avis de faisabilite et de test requis avant tout statut pret.

Les anomalies sont gerees dans [GitHub Project #1](https://github.com/orgs/Nocode-Testing/projects/1/views/1). Le pilotage de travail est gere dans [GitHub Project #2](https://github.com/orgs/Nocode-Testing/projects/2/views/1?system_template=kanban). Les liens GitHub Issues sont renseignes lorsqu'une issue existe ; ce dossier ne cree aucune issue ni aucune ressource distante.

## Statuts communs

| Statut | Signification |
|---|---|
| `brouillon` | Element en preparation, non valide. |
| `a_revoir` | Avis ou decision attendue. |
| `pret` | Element complet et valide pour son usage. |
| `en_cours` | Travail ou execution en cours. |
| `bloque` | Avancement empeche par une dependance ou une decision. |
| `reussi` | Execution terminee sans echec. |
| `echoue` | Execution terminee avec echec. |
| `annule` | Element abandonne avec justification. |
| `archive` | Element conserve mais non actif. |

Les statuts `pret`, `reussi` et `echoue` s'appliquent seulement lorsqu'ils sont pertinents pour le type d'element.