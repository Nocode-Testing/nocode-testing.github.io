# 04 - Contenu editorial et publication

## Cadre

Le Markdown versionne est la solution recommandee avec Eleventy, mais Eleventy n'est pas encore valide definitivement. Les regles ci-dessous restent applicables a toute solution Markdown retenue.

## Preparation

1. Creer une branche `content/*` et une PR avec un contenu cible et ses metadonnees : identifiant, titre, date, resume, tags, statut et slug.
2. Ecrire un contenu relu : liens internes valides, sources et droits d'assets traces dans le registre d'assets.
3. Interdire HTML brut, scripts et iframes dans Markdown. Les images informatives ont un texte alternatif ; les images decoratives utilisent `alt=""`.
4. Verifier le ton, les mentions legales eventuelles, l'accessibilite et les liens ouverts dans un nouvel onglet (`rel="noopener noreferrer"`).

## Publication normale et acceleree

1. Executer les controles applicables : validation Markdown, build et controle de liens non bloquant en cas d'erreur reseau externe.
2. Deployer le commit en recette stable et verifier le rendu cible, mobile et desktop.
3. Le sponsor valide la recette puis promeut humainement le commit identifie.
4. Pour un contenu urgent, le circuit est accelere mais identique : PR, build, recette, validation sponsor et promotion humaine. Aucune edition manuelle non tracee en production.

## Retour arriere

Le sponsor promeut ou redeploie la derniere version validee. Une correction editoriale passe ensuite par une nouvelle PR ; consigner l'incident si le contenu a porte atteinte a un utilisateur ou a la conformite.