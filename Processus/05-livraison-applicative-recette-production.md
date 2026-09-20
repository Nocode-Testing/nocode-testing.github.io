# 05 - Livraison applicative recette-production

## Prerequis

- Lot valide par le sponsor et criteres de sortie testables.
- Commit identifie, revue de code et controles applicables verts.
- Recette stable, protegee et sans donnee reelle.

## Flux

1. Developper sur `feature/*`, ouvrir une PR et lier l'US et les anomalies concernees.
2. Executer les controles disponibles : installation reproductible, lint, tests pertinents, build, analyse de dependances et detection de secrets.
3. Fusionner vers `recette` apres revue ; deployer le commit sur l'URL de recette stable protegee.
4. Executer smoke et campagne de recette. Les anomalies bloquantes ou majeures interdisent la suite.
5. Le sponsor consigne sa validation de recette et autorise la promotion.
6. Creer ou valider la PR `recette` vers `main`. Le sponsor promeut humainement le meme commit vers la production.
7. Executer un smoke public sans donnee personnelle, puis consigner version, URL et resultat.

## Vercel : actions du sponsor

Plan, prerogatives et protections sont a confirmer avant configuration. Le sponsor, administrateur Vercel, realise les actions suivantes dans un lot de deploiement valide :

1. Associer le depot et verifier les reglages de build de la stack retenue.
2. Assigner `recette.nocode-testing.com` a la branche `recette` selon la [documentation Vercel](https://vercel.com/docs/domains/working-with-domains/assign-domain-to-a-git-branch).
3. Configurer dans OVH le seul CNAME web demande par Vercel, apres avoir verifie qu'il ne modifie aucun enregistrement e-mail.
4. Activer la protection adaptee aux testeurs selon [Deployment Protection](https://vercel.com/docs/deployment-protection), sans presumer du plan souscrit.
5. Verifier HTTPS, protection, branche servie et absence de donnees reelles ; noter le resultat dans la recette.

## Retour arriere

Le sponsor redeploie une version Vercel precedemment validee, conformement a la [procedure de promotion Vercel](https://vercel.com/docs/deployments/promoting-a-deployment), puis execute un smoke. Ouvrir une anomalie et appliquer [08](08-incident-retour-arriere-et-post-mortem.md).