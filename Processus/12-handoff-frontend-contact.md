# Handoff frontend - `/contact/`

## Statut et perimetre

Document de cadrage frontend uniquement. Aucun code applicatif, endpoint ou secret n'est defini ici.

Le formulaire `/contact/` est fonctionnel dans le MVP. Il collecte uniquement `nom`, `e-mail`, `societe`, `sujet` et `message`, puis transmet la demande au service serveur du projet. La cible de production est `contact@nocode-testing.com`. La recette utilise exclusivement des donnees fictives et `test_recette@nocode-testing.com`.

Stack cible : Eleventy, HTML semantique, CSS et JavaScript natif, Node.js 22. Le comportement serveur et le contrat definitif restent sous la responsabilite de Rindel Dev.

## Structure HTML attendue

- Une page avec un `main` portant un titre `h1` explicite, par exemple « Nous ecrire ».
- Un texte d'introduction associe au formulaire, indiquant la finalite du contact et invitant a ne pas transmettre de donnees sensibles.
- Un `form` natif avec `method="post"` et une action same-origin fournie par le contrat Rindel. Le frontend ne doit pas construire une URL externe ni envoyer directement un e-mail.
- Un `fieldset` et un `legend` si plusieurs groupes sont necessaires ; sinon une structure simple de champs avec des `label` explicites.
- Les champs visibles suivants, avec `name` stable et identique au contrat :
  - `nom` : texte, obligatoire.
  - `e-mail` : email, obligatoire, avec `autocomplete="email"`.
  - `societe` : texte, facultatif si le contrat le confirme.
  - `sujet` : texte, obligatoire.
  - `message` : `textarea`, obligatoire.
- Chaque champ possede un `id`, un `label` visible et un message d'erreur associe. Les erreurs utilisent `aria-describedby` et `aria-invalid` uniquement lorsque le champ est invalide.
- Une zone de retour globale `role="status"` pour les informations non bloquantes et `role="alert"` pour les erreurs de soumission. Elle doit etre presente dans le DOM avant toute mise a jour.
- Un bouton submit avec un libelle explicite, par exemple « Envoyer le message ». L'icone eventuelle est decorative et ne remplace pas le texte.
- Un lien vers la politique de confidentialite et l'adresse RGPD `rgpd@nocode-testing.com`, sans case de consentement inventee avant validation juridique du traitement.

Le honeypot, s'il est expose dans le HTML, ne doit pas perturber les technologies d'assistance ni le parcours clavier : nom de champ non evident, non focusable et masque visuellement. Il ne constitue jamais une protection cote client ; le serveur reste l'autorite.

## Accessibilite et ergonomie

- Ordre de lecture et de tabulation naturel, compatible clavier sans JavaScript.
- Focus visible continu, contraste AA, cible interactive d'au moins 44 x 44 px et aucun etat porte par la couleur seule.
- Les erreurs sont placees pres du champ concerne et resumees dans la zone globale. Apres une validation invalide, placer le focus sur le premier champ invalide ; apres une reponse serveur, placer le focus sur le titre de l'etat ou la zone de retour sans deplacer silencieusement la personne.
- Le bouton est desactive pendant une requete uniquement pour eviter les doubles soumissions ; le formulaire doit redevenir utilisable en cas d'echec.
- Les textes d'erreur restent factuels et non humoristiques. Les formulations positives du catalogue peuvent etre utilisees uniquement pour une confirmation reussie.
- Ne pas charger d'analytics, de publicite, de suivi ou de script tiers non justifie par le MVP.

## Etats fonctionnels

### Idle

Le formulaire est utilisable, les champs conservent leurs valeurs, aucune erreur de soumission n'est affichee et le bouton porte son libelle normal.

### Validation client invalide

Le navigateur et le frontend peuvent controler les champs requis, le format e-mail et les longueurs connues. Ils affichent une erreur locale accessible et empechent une requete manifestement invalide.

Cette validation est un confort d'interface uniquement. La validation serveur est obligatoire et doit revalider les types, longueurs, encodages, honeypot, limitation de debit et controles anti-abus.

### Loading

Au depart de la requete `POST`, le bouton indique un etat d'envoi, n'est plus activable et la zone de statut annonce le chargement. Ne pas vider les champs ni afficher une reussite avant la reponse serveur.

### Success

Sur reponse serveur de succes, afficher une confirmation accessible et generique, par exemple « Votre message a bien ete envoye. ». Reinitialiser le formulaire uniquement apres cette confirmation et selon le contrat serveur. Ne jamais afficher de contenu renvoye par l'utilisateur comme HTML.

### Error

Pour une erreur reseau, serveur ou fournisseur e-mail, afficher un message generique, conserver les valeurs saisies et proposer une nouvelle tentative. Ne pas exposer de stack trace, secret, adresse complete, diagnostic SMTP ou contenu du message.

### Rate-limit / abus

Pour une limitation de debit, honeypot declenche ou refus anti-abus, afficher un retour neutre qui ne permet pas de distinguer le mecanisme exact. Le frontend ne doit pas contourner, retenter automatiquement ou modifier la reponse serveur. Le statut HTTP et le format d'erreur seront confirmes avec Rindel Dev.

## Transport et contrat a synchroniser avec Rindel Dev

Aucun contrat Rindel detaille n'est present dans le depot. Le frontend attend la confirmation des points suivants avant implementation :

- endpoint `POST` same-origin et methode de protection CSRF si necessaire ;
- format de requete, encodage et noms definitifs des cinq champs ;
- limites de longueur, champs obligatoires et format des erreurs par champ ;
- statuts HTTP pour succes, validation, rate-limit, indisponibilite anti-abus et erreur fournisseur ;
- schema de reponse sans echo de donnees personnelles ni contenu HTML ;
- comportement de l'honeypot et en-tetes necessaires ;
- nom de la configuration Turnstile publique et regle d'activation par environnement.

Le frontend ne doit connaitre que l'URL same-origin publique et les donnees necessaires au rendu. Les identifiants SMTP, la cle secrete Turnstile, les variables privees et les details du fournisseur restent exclusivement cote serveur.

## Environnements et Turnstile

- **Local** : `CONTACT_TRANSPORT=fake` est choisi par variables d'environnement Windows non commitees, injectees au processus serveur ou au middleware de developpement. Le navigateur ne recoit jamais de secret SMTP ni de variable privee. Le mode fake ne fait aucun appel reseau et ne persiste aucune donnee personnelle.
- **Recette** : POST same-origin deploye, transport SMTP OVH a qualifier avec `test_recette@nocode-testing.com`, donnees fictives uniquement. Turnstile est desactive pour la recette automatisee ; aucun widget ni dependance a une cle de production ne doit apparaitre dans ce parcours.
- **Production** : Turnstile Managed peut etre charge uniquement sur `/contact/` lorsque l'environnement l'active. Le serveur doit verifier chaque jeton via Siteverify, avec refus securise si le jeton est absent, invalide, expire, reutilise, lie au mauvais hote/action ou si le service est indisponible. Le frontend affiche alors l'erreur generique et permet une nouvelle tentative.

Le frontend peut recevoir une configuration publique minimale injectee par le serveur, par exemple un indicateur d'activation et une cle publique Turnstile. Cette configuration ne doit jamais contenir de secret. Toute decision RGPD, DPA, transfert ou information visiteur reste a valider avant activation production.

## CSS et integration de la maquette

- Reprendre la direction validee « Labo puzzle » et la reference `assets/mockups/accueil-puzzle-ateliers-themes.svg` : fond brume teinte, encre `#25323D`, ardoise `#5D648C`, bleu gris `#CED7E2`, surfaces blanc casse et accents menthe/corail utilises comme reperes redondants.
- Le formulaire est un panneau editorial integre a la composition, pas un tableau de bord ni une carte imbriquee dans une autre carte. Conserver une lecture claire sur mobile.
- Utiliser `Space Grotesk` pour les titres et reperes courts, `IBM Plex Sans` pour les champs, aides et controles, avec des replis documentes si le chargement des polices n'est pas retenu.
- Maintenir les themes `light` et `dark` avec la cle existante `nct-theme`. Les surfaces, bordures, textes, erreurs et focus doivent avoir des jetons propres dans chaque theme ; ne pas inverser simplement la page.
- Les champs ont des dimensions stables, des libelles toujours visibles, des aides et erreurs qui ne provoquent pas de chevauchement. Sur petits ecrans, les libelles peuvent rester sur plusieurs lignes sans troncature.
- Verifier les largeurs `320x568`, `375x667`, `768x1024` et `1280x800`, avec Chrome et Firefox. Tester aussi le zoom navigateur et la navigation clavier.

## Testabilite et recette

Ajouter seulement les attributs `data-auto` qui ne disposent pas d'un selecteur accessible stable :

- `contact-form` sur le formulaire si son nom accessible ne suffit pas ;
- `contact-submit` sur le bouton si le role et le libelle ne suffisent pas ;
- `contact-status` sur la zone de retour globale ;
- `contact-turnstile` uniquement si le widget est necessaire a l'automatisation production.

Scenarios frontend minimaux :

1. Idle : labels, aides, ordre clavier, focus et champs requis.
2. Validation client : champ requis, e-mail invalide et longueurs hors limites.
3. Loading : bouton bloque, annonce de statut et prevention de double soumission.
4. Success : confirmation, absence d'echo HTML et comportement de remise a zero.
5. Error : erreur reseau ou serveur, conservation des saisies et nouvelle tentative.
6. Rate-limit : message neutre et absence de retry automatique.
7. Local/recette : simulation ou SMTP recette sans Turnstile ni secret expose au navigateur.
8. Production : Turnstile present seulement lorsque la configuration serveur l'active et parcours d'echec generique.

Preuves attendues : tests unitaires frontend des transitions et du mapping d'erreurs, tests d'integration du `POST` avec mocks representatifs fournis par Rindel, puis E2E Chrome/Firefox en recette. Les donnees de recette restent fictives et les logs de test ne contiennent ni message, ni e-mail complet, ni jeton.

## Points de synchronisation avant implementation

- Rindel Dev doit fournir et versionner le contrat `POST` et ses exemples de reponses.
- Armindia UI doit confirmer la composition specifique de la page contact et les jetons d'etat erreur/succes dans les deux themes.
- Mikaya test doit challenger les scenarios unitaires et definir les parcours E2E de recette.
- Mina Cybersécurité doit confirmer le comportement Turnstile production et le fail closed avant activation.
- Soso ArchiOps doit confirmer l'injection des variables locales et la separation des secrets Vercel.
