# 06 - Recette et campagnes de test

## Perimetre

Les campagnes couvrent au minimum navigation, contenus Markdown, liens, responsive, clavier/focus, accessibilite cible, parcours contact lorsqu'il existe et protection de recette.

## Preparation

1. Mikaya prepare les cas de test et la campagne dans `qualite-logicielle/` ; l'execution reference le commit et l'URL de recette.
2. Utiliser exclusivement des donnees fictives. Pour le formulaire, utiliser uniquement `test_recette@nocode-testing.com` comme destinataire de test.
3. Verifier que la recette est protegee, stable et correspond au commit teste.

## Execution

1. Executer les smoke Chrome et Firefox et les E2E critiques disponibles.
2. Effectuer les controles manuels : rendu, liens, mobile, clavier, focus, libelles, contrastes et zoom utile.
3. Consigner les resultats, preuves non sensibles, executions bloquees et anomalies dans Project `#1`.
4. Les liens externes sont controles mais leurs erreurs reseau ne bloquent pas seuls la CI ; ils sont qualifies manuellement si besoin.

## Decision

Mikaya fournit le bilan. Le sponsor seul accepte la recette, une exception ou le report. Aucune production n'est autorisee avec une anomalie bloquante/majeure, une CI en echec, un E2E critique en echec ou une violation axe critique/serieuse non justifiee.

## Retour arriere

En cas d'echec de recette, conserver les preuves, creer ou lier les anomalies, revenir au ticket de correction et relancer la campagne sur un nouveau commit.