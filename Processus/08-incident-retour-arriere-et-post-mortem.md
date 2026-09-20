# 08 - Incident, retour arriere et post-mortem

## Declenchement

Declencher cette procedure pour indisponibilite, regression en production, fuite suspectee, erreur de contenu sensible, envoi e-mail anormal ou degradation de securite.

## Reponse immediate

1. Creer une Issue d'incident dans Project `#1` sans donnee personnelle ni secret ; noter heure, impact, version et actions.
2. Le sponsor decide l'arret d'une promotion, la desactivation fonctionnelle ou le retour arriere.
3. Pour une regression de site, le sponsor redeploie la derniere version Vercel validee et lance un smoke public.
4. Pour une fuite de secret, le sponsor revoque ou fait tourner le secret directement chez le fournisseur et verifie les acces.
5. Informer les personnes utiles avec des faits confirmes, sans exposer de donnees personnelles.

## Stabilisation et reprise

1. Identifier la cause probable, le perimetre affecte et les utilisateurs concernes.
2. Corriger dans une branche, tester sur recette avec donnees fictives et suivre [05](05-livraison-applicative-recette-production.md).
3. Le sponsor valide la reprise et la promotion humaine.

## Post-mortem

Sous cinq jours ouvrables, consigner : chronologie, impact, cause racine, detection, decision de retour arriere, actions preventives, responsable et echeance. Le post-mortem ne cherche pas de responsabilite individuelle et ne contient ni secret ni donnee personnelle.