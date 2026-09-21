# nocode-testing.com

Ce depot va accueillir prochainement le site de nocode-testing.com.

Le projet repart de zero: l'ancienne base Docusaurus a ete retiree pour laisser place au futur site, qui sera concu et realise via IA par mes soins.

## Statut

Le repository sert actuellement de point de depart propre avant la mise en ligne du site.

Le site sera une vitrine de `nocode-testing`, avec le blog professionnel "Le testeur du granier", une rubrique d'experimentations IA, des ressources, une page a propos et un contact. La stack detaillee reste a choisir. Les questions et decisions de cadrage sont suivies dans [build-app.md](./build-app.md).

## Organisation du projet

Le projet est pilote par l'agent Dominion Orchestrateur. Les roles specialises couvrent les exigences, la securite, l'architecture et l'exploitation, l'UX/UI, le frontend, le backend et les tests. Aucun chantier n'est lance avant validation explicite du commanditaire.

Les notes de contexte technique et UI sont respectivement maintenues dans [handoff.md](./handoff.md) et [handoff_UI.md](./handoff_UI.md).

## Developpement

Node.js 22 LTS est la version cible du MVP. Eleventy, HTML/CSS/JavaScript natif et les scripts de build, test et developpement seront ajoutes lors du premier incrément technique.

## Publication

Le code sera heberge sur GitHub et deploye sur Vercel. Deux environnements sont prevus : une recette protegee par mot de passe et une production publique, toutes deux en HTTPS. Une CI devra verifier chaque increment avant la recette puis la production.

Les elements de marque (logo et charte graphique) sont conserves dans `assets/brand/`.

## Licence

Ce projet conserve sa licence actuelle. Voir [LICENSE](./LICENSE).