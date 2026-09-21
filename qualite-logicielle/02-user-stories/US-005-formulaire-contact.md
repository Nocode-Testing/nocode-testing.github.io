---
id: US-005
statut: a_revoir
liens:
  requirements:
    - REQ-005
  github_issue: null
  github_project: null
---

# US-005 - Formulaire de contact fonctionnel

En tant que visiteur de nocode-testing.com,
Je veux envoyer une demande depuis `/contact/`,
Afin d'obtenir une reponse de NOCODE TESTING.

## Contexte

La route `/contact/` est fonctionnelle dans le MVP. Le formulaire collecte uniquement `nom`, `e-mail`, `societe`, `sujet` et `message`, puis transmet la demande au destinataire de l'environnement. Le transport et les parametres sont choisis par variables d'environnement Windows locales non commitees ; aucun secret SMTP n'est requis ni stocke en local.

## Modes d'execution

- **Local** : le transport fake est selectionne par variables d'environnement Windows non commitees. Il simule l'envoi sans appel reseau, sans SMTP et sans persistance du payload personnel ; il ne contient aucun secret SMTP de recette ou de production.
- **Recette** : l'essai utilise le SMTP OVH `smtp.mail.ovh.net:587`, STARTTLS et authentification avec des secrets saisis par le commanditaire dans Vercel. Les donnees sont fictives, le destinataire est `test_recette@nocode-testing.com` et Turnstile est desactive pour les E2E automatisees.
- **Production** : l'envoi utilise le SMTP OVH qualifie, les secrets Vercel de production et le destinataire `contact@nocode-testing.com`. Turnstile est active, limite a la production et verifie cote serveur via Siteverify.

## Regles metier

- Les champs du formulaire sont `nom`, `e-mail`, `societe`, `sujet` et `message`. Les bornes de longueur, le format de l'e-mail et l'encodage sont controles cote serveur.
- Aucun contenu utilisateur n'est interprete comme HTML ou injecte dans les journaux.
- Un champ honeypot est present pour les soumissions automatisees ; une soumission identifiee comme abusive recoit une reponse neutre.
- Une limitation de debit durable cote serveur protege l'envoi. Elle s'applique avant le transport et ne divulgue pas le fonctionnement interne du dispositif.
- Une erreur de validation, d'anti-spam ou de transport n'expose ni secret, ni detail SMTP, ni contenu de message ; le message affiche est generique et actionnable.
- Un succes confirme uniquement que la demande a ete prise en compte. Le contenu du message, l'adresse e-mail complete et les secrets sont exclus des logs ; seuls les elements techniques strictement necessaires peuvent etre traces.
- En recette, aucune donnee reelle ou sensible ne doit etre utilisee et aucune demande ne doit etre adressee a `contact@nocode-testing.com`.
- Les donnees sont traitees pour recevoir, traiter et suivre la demande. La personne est invitee a ne pas transmettre de donnees sensibles ; les droits RGPD sont accessibles via `rgpd@nocode-testing.com`.
- La promotion en production est bloquee tant que la recette SMTP n'a pas verifie la reception, TLS, les quotas ou limites utiles, les logs minimises et la gestion d'erreur, et tant que les reserves critiques ou elevees de securite ne sont pas acceptees ou corrigees.

## Criteres d'acceptation

```gherkin
Scenario: Afficher le formulaire fonctionnel
  Given un visiteur ouvre `/contact/`
  When la page est rendue
  Then les champs nom, e-mail, societe, sujet et message sont visibles
  And chaque champ a un libelle accessible
  And le formulaire indique comment obtenir l'information RGPD

Scenario: Refuser une saisie invalide cote serveur
  Given une personne soumet un formulaire avec un champ obligatoire manquant, une longueur depassee ou un e-mail invalide
  When le serveur traite la demande
  Then aucune demande n'est transmise
  And une erreur generique indique qu'une correction est necessaire
  And aucun contenu utilisateur n'est interprete comme HTML

Scenario: Envoyer une demande en mode local
  Given le mode local est configure par des variables d'environnement Windows non commitees
  And aucun secret SMTP OVH de recette ou de production n'est present
  When une personne soumet des donnees de test valides
  Then le transport fake retourne un resultat simule
  And aucun appel reseau SMTP ni aucune ecriture du payload personnel n'est effectuee

Scenario: Envoyer une demande fictive en recette
  Given l'application s'execute en recette
  And les donnees saisies sont fictives
  When une demande valide est soumise sans Turnstile
  Then elle est envoyee via SMTP OVH avec STARTTLS vers `test_recette@nocode-testing.com`
  And elle n'est jamais envoyee vers `contact@nocode-testing.com`
  And la reponse confirme generiquement la prise en compte

Scenario: Envoyer une demande en production
  Given l'application s'execute en production
  And Turnstile est valide par Siteverify
  When une demande valide est soumise
  Then elle est envoyee via SMTP OVH avec STARTTLS vers `contact@nocode-testing.com`
  And la reponse confirme generiquement la prise en compte

Scenario: Bloquer un abus anti-spam
  Given une soumission contient une valeur dans le honeypot ou depasse la limitation de debit durable
  When le serveur traite la demande
  Then aucune demande n'est transmise
  And la reponse reste neutre et ne revele pas le controle declenche
  And le contenu du message et l'adresse e-mail complete ne sont pas inscrits dans les logs

Scenario: Refuser Turnstile indisponible en production
  Given l'application s'execute en production
  And la verification serveur Siteverify est indisponible ou invalide
  When une demande est soumise
  Then aucune demande n'est transmise
  And une erreur generique est affichee
  And aucun secret ni detail du fournisseur n'est expose

Scenario: Gerer une erreur de transport
  Given le transport configure echoue ou ne repond pas
  When une personne soumet une demande valide
  Then aucune confirmation de livraison n'est affichee
  And une erreur generique invite a reessayer ulterieurement
  And les logs ne contiennent ni message, ni e-mail complet, ni secret SMTP

Scenario: Utiliser le formulaire au clavier et sur mobile
  Given une personne utilise le clavier ou un viewport de `320x568`, `375x667`, `768x1024` ou `1280x800`
  When elle parcourt et soumet le formulaire
  Then l'ordre de lecture et de focus est coherent
  And le focus, les erreurs et le succes sont visibles et accessibles
  And aucun champ, message ou bouton n'est tronque ni superpose
  And les criteres WCAG 2.2 AA applicables sont respectes
```

## Exigences non fonctionnelles

- Securite : fonction serveur same-origin, validation stricte, encodage, honeypot, limitation de debit durable, Turnstile production avec Siteverify, refus securise, secrets uniquement dans Vercel pour recette/production.
- Confidentialite : minimisation des donnees et des logs, HTTPS, information RGPD, absence de donnees sensibles en recette, conservation conforme a la politique soumise a revue juridique humaine.
- Accessibilite : HTML semantique, libelles associes, erreurs et succes annonces de facon accessible, clavier, focus visible, contrastes et responsive selon WCAG 2.2 AA applicable.
- Performance et charge : temps de reponse et capacite du transport, de la limitation de debit et de SMTP a qualifier en recette ; un envoi ne doit pas bloquer indefiniment la page.
- Livraison : CI bloquante sur build/tests, recette avant promotion humaine, production interdite avant validation du test SMTP OVH et des reserves de securite.

## Avis et decisions

- Taille : OK pour un cycle court si le contrat d'envoi et la qualification d'infrastructure restent dans cette US ; les travaux d'implementation du transport, de l'infrastructure et de la CI sont des dependances techniques, pas des exigences supplementaires.
- Revues Mina Cybersecurite, Mikaya test, Camity Front, Rindel Dev et Soso ArchiOps attendues avant `pret`.
- Le statut reste `a_revoir` jusqu'a ces revues et a la resolution ou l'acceptation explicite des reserves critiques ou elevees de securite.

## Liens

- Exigence parente : [REQ-005](../01-exigences/referentiel-exigences.md#req-005---formulaire-de-contact-fonctionnel)
- Procedure contact : `Processus/09-formulaire-contact-et-messagerie.md`
- Projet de politique de confidentialite : `Processus/11-projet-politique-confidentialite.md`
- GitHub Issue : `null`