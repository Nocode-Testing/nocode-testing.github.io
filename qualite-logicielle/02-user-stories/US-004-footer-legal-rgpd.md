---
id: US-004
statut: a_revoir
liens:
  requirements:
    - REQ-004
  github_issue: null
  github_project: null
---

# US-004 - Footer legal et RGPD

En tant que visiteur,
Je veux trouver les informations legales et RGPD depuis le footer,
Afin de comprendre le responsable du site et l'usage de mes donnees.

## Contexte

Le footer appartient au premier lot et expose les liens legaux et RGPD sans analytics, publicite, suivi ni script tiers non justifie dans le MVP. La publication des pages legales est interdite avant une revue humaine finale.

## Regles metier

- Le footer contient un acces aux mentions legales et a la politique de confidentialite.
- Les routes legales sont `/mentions-legales/` et `/confidentialite/`.
- Le footer est present sur toutes les pages du lot MVP et contient le lien LinkedIn lorsque ce perimetre est publie.
- Le footer contient le lien LinkedIn personnel `https://www.linkedin.com/in/michael-granier/` et le lien LinkedIn entreprise `https://www.linkedin.com/company/nocode-testing`.
- Les adresses de contact sont `contact@nocode-testing.com` et `rgpd@nocode-testing.com`.
- Les informations legales connues sont verifiees humainement avant publication ; aucune page legale n'est publiee avant la revue juridique finale.
- L'adresse de confidentialite et les informations juridiques inconnues ne sont pas inventees.
- Aucun consentement a des traceurs non essentiels n'est requis si aucun traceur n'est charge.

## Criteres d'acceptation

```gherkin
Scenario: Afficher le footer sur toutes les pages du lot
  Given un visiteur consulte une page du lot MVP
  When la page est rendue
  Then le footer est visible en fin de contenu
  And les liens `/mentions-legales/` et `/confidentialite/` sont accessibles
  And le lien LinkedIn est accessible si le perimetre LinkedIn est publie

Scenario: Consulter les informations au clavier
  Given un visiteur navigue au clavier
  When il atteint le footer
  Then chaque lien a un nom accessible et un focus visible
  And chaque lien peut etre active avec Entree

Scenario: Ne charger aucun service tiers non justifie
  Given le visiteur ouvre le site dans le MVP
  When la page est chargee
  Then aucun analytics, publicite, suivi ni script tiers non justifie n'est charge
  And aucune donnee personnelle n'est collectee par le footer

```

## Precondition de sortie

Avant toute publication en production, une revue humaine finale des mentions legales et de la politique de confidentialite doit etre tracee. En l'absence de cette revue, la publication legale et la promotion du lot sont bloquees.

## Exigences non fonctionnelles

- Informations lisibles, accessibles au clavier, utilisables sur mobile et verifiees sous Chrome et Firefox.
- HTTPS requis en recette et en production.
- Relecture humaine de la politique de confidentialite avant publication.
- La CI bloque le build ou les tests en echec ; la recette precede toute promotion manuelle.

## Avis et decisions

- Taille : OK pour un cycle court, limitee au footer et aux liens legaux/RGPD.
- Revues Mina Cybersecurite, Mikaya test et Soso ArchiOps si le deploiement ou le consentement evoluent, avant `pret`.
- Statut de revue : `a_revoir`.

## Liens

- Exigence parente : [REQ-004](../01-exigences/referentiel-exigences.md#req-004---footer-legal-et-rgpd)
- GitHub Issue : `null`
