# 07 - Gestion des acces, secrets et environnements

## Principes

- Le sponsor est administrateur de GitHub, Vercel, OVH/DNS et des secrets.
- Les secrets ne figurent jamais dans Git, les Issues, les logs, les captures ou cette documentation.
- Aucun agent ne demande, recoit ou stocke mot de passe, jeton, cle privee ou identifiant SMTP.

## Environnements

| Environnement | Donnees | Acces | Secrets |
|---|---|---|---|
| Local | Fictives | Developpeurs autorises | Fichier local non versionne si necessaire |
| CI | Fictives | Workflow a droits minimaux | Aucun secret hors action deploiement justifiee |
| Recette | Fictives ou anonymisees | Testeurs autorises, protection active | Valeurs dediees, distinctes de production |
| Production | Reelles minimales | Public pour le site, administration sponsor | Valeurs dediees, jamais exposees au navigateur |

## Procedure d'acces

1. Le demandeur justifie l'acces, son perimetre et sa duree.
2. Le sponsor accorde le droit minimal necessaire et l'inscrit dans son registre d'acces.
3. Pour un secret, le sponsor le saisit directement dans le gestionnaire du fournisseur concerne, sans le transmettre aux agents.
4. Apres le lot ou le depart d'un intervenant, le sponsor retire l'acces et fait tourner le secret s'il a pu etre expose.

## Controle et urgence

Verifier avant chaque mise en production la separation recette/production, l'absence de variable publique sensible et les droits minimaux. En cas de fuite suspectee, revoquer ou faire tourner la valeur dans le fournisseur, stopper les promotions et ouvrir un incident selon [08](08-incident-retour-arriere-et-post-mortem.md).