# Projet de politique de confidentialite

**Projet a afficher sur nocode-testing.com - ne pas publier sans revue juridique humaine competente.**

Derniere mise a jour du projet : 21 septembre 2026.

## Responsable du traitement

Le responsable du traitement des donnees personnelles est :

Michael Granier - Président
`contact@nocode-testing.com`
NOCODE TESTING, SAS  
SIREN : 943 002 451  
SIRET : 943 002 451 00012  
8 ter rue de la penissiere  
85610 Cugand, France

Pour toute question relative a vos donnees personnelles ou pour exercer vos droits, vous pouvez ecrire a : `rgpd@nocode-testing.com`.

## Donnees collectees et finalites

Lorsque vous utilisez le formulaire de contact, nous collectons les donnees que vous choisissez de nous communiquer :

- nom ;
- adresse e-mail ;
- societe ;
- sujet de votre demande ;
- contenu de votre message.

Ces donnees sont utilisees uniquement pour recevoir, traiter et repondre a votre demande de contact, ainsi que, lorsque cela est necessaire, pour assurer le suivi de nos echanges. Nous vous invitons a ne pas transmettre de donnees sensibles ou confidentielles dans votre message, sauf si cela est indispensable et approprie.

Le formulaire et ses journaux techniques sont concus pour limiter les donnees traitees. Les journaux ne doivent pas contenir le contenu des messages, les adresses e-mail completes ni des secrets.

## Base legale

Le traitement de vos donnees de contact repose sur une base legale appropriee au contexte de votre demande. Selon la nature de l'echange, il pourra s'agir de mesures precontractuelles prises a votre demande, de l'execution d'un contrat ou de l'interet legitime de NOCODE TESTING a repondre aux sollicitations professionnelles et a assurer le suivi de ses contacts.

Cette presentation ne vaut pas avis juridique. La presente politique fera l'objet d'une revue juridique humaine avant sa mise en ligne.

## Destinataires et sous-traitants

Les donnees sont accessibles uniquement aux personnes habilitees de NOCODE TESTING qui doivent traiter votre demande.

Pour fournir le site et le formulaire, des prestataires techniques peuvent intervenir en qualite de sous-traitants, dans la limite de leurs roles respectifs :

- hebergement et deploiement du site : Vercel ;
- protection contre les soumissions automatisees en production : Cloudflare Turnstile ;
- acheminement des e-mails du formulaire : OVH, via le service SMTP retenu pour le formulaire.

Ces prestataires ne recoivent que les donnees necessaires a leur mission. Leurs conditions contractuelles, mesures de securite et roles sont pris en compte dans la configuration du service.

## Transferts hors de l'Union europeenne

L'hebergement, les services anti-abus et l'acheminement des e-mails peuvent impliquer des traitements ou des acces depuis des pays situes hors de l'Espace economique europeen. Les localisations et garanties applicables dependent des offres et configurations definitivement retenues.

Lorsque ces traitements ou acces existent, ils sont encadres par la garantie appropriee au regard de la reglementation applicable, par exemple une decision d'adequation ou des clauses contractuelles types accompagnees, si necessaire, de mesures supplementaires.

## Durees de conservation

Les demandes de contact sont conservees au maximum trois ans apres le dernier contact actif avec la personne concernee. Elles sont supprimees plus tot lorsque la finalite de la demande est atteinte ou lorsque la personne exerce valablement son droit a l'effacement, sous reserve des obligations legales applicables.

Le responsable du traitement realise les suppressions. Les journaux techniques et les sauvegardes sont conserves pendant la duree necessaire a leurs finalites de securite et de fonctionnement, selon les durees definies par le projet. Les e-mails lies au traitement d'une demande suivent la duree de conservation de cette demande et ne sont pas conserves au-dela de ce qui est necessaire.

## Vos droits

Dans les conditions prevues par la reglementation applicable, vous pouvez demander l'acces a vos donnees, leur rectification, leur effacement, la limitation de leur traitement, vous opposer a certains traitements et demander la portabilite de vos donnees lorsque ce droit s'applique.

Pour exercer ces droits, contactez-nous a `rgpd@nocode-testing.com`. Afin de proteger vos donnees, nous pourrons demander les informations strictement necessaires pour verifier votre identite avant de repondre. Nous repondrons dans les delais applicables par la reglementation.

Vous pouvez egalement introduire une reclamation aupres de la Commission nationale de l'informatique et des libertes (CNIL) : [www.cnil.fr](https://www.cnil.fr/).

## Securite

NOCODE TESTING met en oeuvre des mesures techniques et organisationnelles adaptees pour proteger les donnees traitees, notamment la limitation des donnees collectees, le chiffrement des communications en HTTPS, la restriction des acces et la minimisation des journaux.

Malgre ces mesures, aucune transmission ou conservation de donnees sur internet ne peut etre garantie comme totalement securisee. En cas d'incident affectant des donnees personnelles, NOCODE TESTING appliquera les obligations d'analyse, de notification et d'information prevues par la reglementation applicable.

## Cookies et mesure d'audience

Aucun outil d'analytics ou de mesure d'audience n'est integre au site. Aucun traceur non essentiel ne doit etre depose ou lu sans votre consentement prealable.

Le site peut utiliser des technologies strictement necessaires a son fonctionnement et a sa securite. En production uniquement, Cloudflare Turnstile est charge lors de l'utilisation du formulaire afin de proteger celui-ci contre les soumissions automatisees. Turnstile n'est pas charge sur l'environnement de recette.

Si des cookies ou traceurs non essentiels sont ajoutes ulterieurement, une information et, lorsque requis, un mecanisme de consentement seront mis en place avant leur activation.

## Modifications de cette politique

Cette politique peut etre mise a jour pour tenir compte d'une evolution des traitements, des prestataires ou de la reglementation. La date de derniere mise a jour sera modifiee lors de toute evolution significative.

## Suivi de validation interne - ne pas publier

Les arbitrages du commanditaire sont les suivants :

1. le responsable du traitement et les coordonnees indiquees sont valides ;
2. la base legale et sa formulation sont correctes ;
3. Vercel, Cloudflare Turnstile et OVH sont les sous-traitants retenus dans le texte ;
4. aucune information supplementaire n'est requise a ce stade sur les transferts ;
5. les durees de conservation sont coherentes avec le projet ;
6. Cloudflare Turnstile est valide pour la production ;
7. aucun analytics n'est utilise a ce jour ;
8. la coherence generale avec le formulaire et les procedures est validee.

Avant activation, seuls les points techniques suivants restent a confirmer :

- la configuration reelle des sous-traitants dans les environnements deployes ;
> On mettra à jour après le MVP
- le test SMTP OVH en recette avec `smtp.mail.ovh.net:587`, STARTTLS et authentification.
> On testera après premier déploiement.

La revue juridique humaine reste obligatoire avant toute publication. Le present document est un projet d'information et ne constitue pas une garantie de conformite RGPD.