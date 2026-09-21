# Processus projet

Ces procedures decrivent le fonctionnement du projet `nocode-testing.com`.

## Regles communes

- Le sponsor est le seul a valider une priorite, une exception et une promotion vers la production.
- Project GitHub `#1` est le registre des anomalies. Project GitHub `#2` est le Kanban des travaux.
- Chaque changement passe par une trace Git, une recette stable et une promotion humaine d'un commit identifie.
- La recette et les previews ne contiennent aucune donnee reelle. La production est publique et sa promotion est exclusivement humaine.
- Les agents preparent les livrables et les tickets ; ils ne realisent aucune action distante ni ne manipulent de secret.

## Procedures

| Procedure | Objet |
|---|---|
| [01](01-cadrage-et-validation-de-lot.md) | Cadrer et valider un increment |
| [02](02-gestion-des-user-stories-et-tickets.md) | Gerer les US, taches et Kanban |
| [03](03-gestion-des-anomalies-et-priorites.md) | Qualifier les anomalies et leurs priorites |
| [04](04-contenu-editorial-et-publication.md) | Publier du contenu Markdown |
| [05](05-livraison-applicative-recette-production.md) | Livrer une evolution applicative |
| [06](06-recette-et-campagnes-de-test.md) | Executer la recette et les campagnes |
| [07](07-gestion-des-acces-secrets-et-environnements.md) | Administrer les acces et secrets |
| [08](08-incident-retour-arriere-et-post-mortem.md) | Gerer un incident et son retour arriere |
| [09](09-formulaire-contact-et-messagerie.md) | Mettre en service le formulaire et SMTP |
| [10](10-rgpd-demandes-et-conservation.md) | Traiter les demandes RGPD et la conservation |
| [11](11-projet-politique-confidentialite.md) | Projet de politique de confidentialité à relire humainement |
| [Contrat API](12-contrat-api-contact.md) | Contrat API du formulaire de contact |
| [Handoff frontend](12-handoff-frontend-contact.md) | Cadrer le frontend du formulaire `/contact/` |

## Questions bloquantes

1. Avant la mise en service de la recette protegee : le sponsor choisit le plan Vercel ou confirme que chaque testeur utilisera un compte Vercel autorise.
2. Avant l'activation du formulaire : le sponsor documente la duree chiffree de conservation legalement validee et sa justification.