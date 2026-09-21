# Handoff UI

Ce document sert de memoire de contexte UX/UI pour un LLM intervenant sur le design du projet.
Il centralise les decisions de design, les pistes retenues, la charte graphique validee et les informations utiles pour garder une coherence visuelle dans le temps.

## Type de site ou produit
- Futur site `nocode-testing.com`, en reconstruction apres le retrait de l'ancienne base Docusaurus.
- Vitrine de l'entreprise `nocode-testing` avec le blog professionnel "Le testeur du granier", une rubrique d'experimentations IA, des ressources, une page a propos et un contact.

## Objectif de l'interface
- Presenter l'entreprise et ses contenus, encourager la prise de contact et permettre l'exploration du blog, des ressources et des experimentations.

## Public cible
- Professionnels du test logiciel, entreprises recherchant une prestation, communaute no-code/low-code, recruteurs et partenaires.

## Parcours et ecrans importants
- Accueil avec header de navigation, blog avec un premier article, experimentations, ressources, a propos, contact et footer avec informations RGPD et lien LinkedIn.

## Charte graphique validee
- Logo PNG/SVG et document de charte graphique disponibles dans `assets/brand/`.
- Variantes disponibles : logo couleur, logo noir et blanc et logo blanc. Utiliser le SVG couleur comme variante de reference par defaut ; le noir et blanc et le blanc sont reserves aux contextes ou le contraste ou la charte le justifient.
- Armindia UI devra exploiter ces elements et ne proposer que les decisions graphiques non couvertes par la charte.

## Inspirations et references
- A completer.

## Composants ou patterns retenus
- A completer.

## Directions explorees
- 2026-09-20 : « Atelier de test / laboratoire » confirme par le sponsor. La direction associe qualite logicielle, protocole de test et experimentation professionnelle, sans imagerie scientifique generique.
- Maquette recommandee : `assets/mockups/accueil-atelier-calibre.svg`, avec vues desktop et mobile. Alternative editoriale : `assets/mockups/accueil-carnet-laboratoire.svg`.
- Le libelle de navigation devient `Labo Test & IA` en remplacement de `Experimentations IA`.
- 2026-09-20 : le sponsor juge les directions « Atelier calibre » et « Carnet de laboratoire » trop standard. Deux pistes plus expressives les remplacent pour arbitrage : `assets/mockups/accueil-orbite-des-cas.svg` et `assets/mockups/accueil-champ-de-preuves.svg`. Elles montrent chacune un accueil et un header en vues desktop et mobile.
- « Orbite des cas » : une carte orbitale abstraite de parcours et de points de verification. Recommendation Armindia UI : plus memorable, plus souple pour decliner blog, ressources et experimentation, tout en restant lisible.
- « Champ de preuves » : une matrice de tuiles et de flux. Direction plus graphique, editoriale et dense ; a privilegier si la marque assume une expression visuelle plus vive.
- 2026-09-20 : « Labo puzzle » est la nouvelle recommandation. Elle reprend la palette de base Atelier calibre, mais remplace son registre conventionnel par des panneaux asymetriques, des pieces abstraites et un parcours editorial visible. Livrables : `assets/mockups/direction-labo-puzzle.svg` et `assets/mockups/accueil-labo-puzzle.svg`.
- La maquette place la navigation dans un module autonome a droite sur desktop. Sur mobile, ce module devient un panneau distinct sous le header ; le header conserve le logo et le controle Menu/Contact.
- 2026-09-20 : le sponsor conserve les principes de composition de Labo puzzle, mais prefere revenir aux couleurs d'Atelier calibre, en particulier pour le panneau de navigation droit. L'accent citron est rejete. La prochaine version melangera panneau droit actif et cartes de contenu a gauche, dans une composition legerement destructuree.
- 2026-09-20 : maquette hybride produite : `assets/mockups/accueil-hybride-atelier-calibre.svg`. Elle reprend le panneau de navigation ardoise actif a droite et des cartes editoriales qui se decalent legerement a gauche, sans perturber l'ordre de lecture. Le logo est incorpore comme symbole vectoriel interne afin de rester visible dans les apercus SVG.
- 2026-09-20 : raffinement demande : conserver fond, cadre et header hybrides ; rapprocher le panneau droit du cadre ; remplacer les cartes de gauche par les panneaux graphiques de `direction-labo-puzzle.svg`. Les boutons passent en flat design rectangulaire sans contour, avec pictogramme representatif et libelle explicite.
- 2026-09-20 : raffinement produit : `assets/mockups/accueil-hybride-atelier-calibre-raffine.svg`, planche autonome desktop + mobile. Le fond colore, le cadre et le header hybride sont conserves. Le panneau ardoise est rapproche du bord droit du cadre ; les contenus de gauche deviennent les panneaux asymetriques « Question », « Essai » et « Retour terrain ». Le logo est un symbole vectoriel interne, sans ressource SVG externe.
- 2026-09-20 : le sponsor rejette la traduction simplifiee des panneaux. La prochaine version doit reprendre fidelement la composition de `direction-labo-puzzle.svg` a gauche du panneau droit : bloc sombre vertical, bloc bleu horizontal, bloc blanc et bloc colore, avec les proportions et decalages de la planche source. Une variante sombre est autorisee et doit etre pilotable par un controle dans le header.
- 2026-09-20 : planche de correction produite : `assets/mockups/accueil-puzzle-ateliers-themes.svg`. Elle presente les vues claire et sombre en desktop et mobile. Le groupe gauche reprend les quatre masses Labo puzzle et leurs rapports de composition : grand sombre vertical, bleu horizontal, blanc bas gauche, colore bas droite. La navigation ardoise est physiquement rattachee au header, en haut a droite et proche du cadre.
- 2026-09-20 : le sponsor valide cette direction comme premiere version du MVP. `assets/mockups/accueil-puzzle-ateliers-themes.svg` devient la reference de handoff UI pour l'accueil et le header.
- 2026-09-21 : le lot produit inclut le footer et le theme clair/sombre. Le hero commence par « La Qualite logicielle est l'affaire de tou•te•s ». Les CTA sont « L'univers du Testeur du Granier » et « Nos experimentations ». Le controle de theme est visuel avec une icone seule, mais conserve un nom accessible et un etat expose. La variante de logo est adaptee au theme ; la personnalisation de themes brandes est post-MVP.
- 2026-09-21 : les routes du lot sont validees. Le theme persiste sous la cle `nct-theme` avec les valeurs `light` et `dark`. Le logo du theme sombre est `assets/brand/Logo_NCT_vectoriel_blanc.png`; le logo de reference clair/couleur reste utilise sur fond clair.
- 2026-09-21 : maquette du formulaire `/contact/` validee pour transmission a Camity Front : `assets/mockups/contact-formulaire-labo-puzzle.svg` et `assets/mockups/contact-formulaire-labo-puzzle-handoff.md`. La composition reprend le panneau editorial Labo puzzle, avec vues desktop/mobile, themes clair/sombre et etats idle, validation, loading, succes, erreur de transport et rate-limit.

## Decisions validees
- Le hero doit faire figurer « Qualite logicielle ».
- Le ton humoristique est perceptible des l'accueil, de maniere legere et contextuelle.
- Le bleu ardoise `#5D648C` et le bleu gris clair `#CED7E2` restent les couleurs structurantes. La maquette hybride recommande le cuivre doux `#A85E44` pour les annotations et reperes secondaires, jamais comme seul indicateur d'etat : il est associe a un libelle, une forme ou une position. Son contraste est preserve par l'usage en texte fonce sur fond clair ou texte blanc sur aplat cuivre, et non pour du petit texte cuivre sur fond colore.
- Le cuivre doux est rejete. Les accents de reference reprennent le bleu gris `#CED7E2` et les couleurs Atelier calibre. Aucun jaune citron ni cuivre n'est retenu pour la direction cible.
- Les nouvelles maquettes conservent les couleurs de marque et ajoutent des accents menthe/corail ou cyan/jaune/rouge uniquement comme reperes redondants avec texte et formes. Elles n'emploient aucun personnage, symbole, slogan, asset ou interface tiers proteges.
- Chaque header presente une signature logo de marque et la navigation cible : Blog, Labo Test & IA, Ressources, A propos et Contact. Les maquettes indiquent des tailles de texte lisibles, des contrastes forts et des controles qui pourront conserver un focus visible lors de l'implementation.
- Le logo couleur `assets/brand/Logo_NCT_vectoriel.svg` doit etre utilise comme fichier source dans le header, et non recompose, simplifie ou remplace par un monogramme. Les maquettes Labo puzzle le referencent explicitement.
- En theme sombre, utiliser `assets/brand/Logo_NCT_vectoriel_blanc.png` pour garantir le contraste ; ne pas afficher le mot-symbole textuel dans le controle de theme.
- Palette Labo puzzle a valider pour implementation : fond brume teinte `#E5E9E4` ou surface proche, blanc casse `#F5F7F3`, encre `#25323D`, bleu ardoise de marque `#5D648C`, bleu gris `#CED7E2`, citron `#D6E65E` et corail `#DF765D`. Citron et corail sont des accents de parcours, jamais le seul porteur d'une information ou d'un etat.
- Typographies proposees, sans installation dans ce depot : `Space Grotesk` (titres, numerotation et micro-libelles) et `IBM Plex Sans` (lecture et controles). Les deux familles sont open source et prennent en charge les contenus francais ; leur mode de chargement et les repli systeme relevent du lot frontend.
- Regle de transposition image vers UI : les panneaux, trajectoires et pieces sont des repères de composition, pas des widgets, donnees, statistiques ni animations imposees. Camity Front doit les realiser avec HTML/CSS semantique, conserver l'ordre de lecture naturel et proposer un focus visible ; aucune forme decorative ne doit concurrencer un lien, un bouton ou une information.
- Les influences autorisees restent abstraites : modularite, contraste de panneaux, indices de parcours et geometrie experimentale. Aucun symbole, personnage, slogan, asset, interface ou vocabulaire identifiable d'une oeuvre tierce ne doit etre utilise.
- Les boutons doivent avoir une patte plus personnelle que des rectangles arrondis standard, tout en conservant une apparence de controle, un libelle explicite, un contraste suffisant et des etats clavier visibles.
- Les maquettes doivent incorporer le logo de reference de maniere autoportante. Un lien SVG externe peut etre masque par certains apercus et ne suffit donc pas a valider le rendu du logo.
- Boutons et controles de la direction hybride : silhouette de cartouche a encoche droite, avec un minimum de 44 x 44 px pour toute cible interactive. Le libelle reste entier et explicite ; la forme ne remplace jamais le texte. Au survol, eclaircir la surface de fond ou renforcer le contour sans deplacer la mise en page. Au focus clavier, afficher un anneau continu de 3 px en bleu gris clair `#CED7E2`, decale d'au moins 3 px et visible sur tous les fonds ; ne jamais supprimer `:focus-visible`. L'activation clavier `Enter` et `Espace` reste native selon l'element semantique employe. Les differents etats ne reposent jamais sur la couleur seule.
- Boutons attendus dans le raffinement : flat design rectangulaire sans contour. Chaque bouton associe une icone semantiquement decorative a un libelle entier ; la taille de cible reste au moins 44 x 44 px. Le focus visible, les etats hover/actif et l'activation clavier native restent obligatoires ; l'icone n'est jamais l'unique moyen de comprendre l'action.
- Le bouton Contact et le bouton « Nous ecrire » doivent garantir un pictogramme de messagerie visible par contraste. Le bouton du panneau droit est centre horizontalement. Les CTA d'accueil sont « Decouvrez l'univers du Testeur du Granier » et « Decouvrez nos experimentations ».
- Le mode sombre est une exigence de la direction cible. Le header fournit un bouton de bascule accessible avec libelle explicite, etat expose aux technologies d'assistance, focus visible et preference systeme respectee au premier chargement. La variante sombre conserve les contrastes, le logo, les boutons et la distinction du panneau de navigation ; elle ne repose pas sur une inversion automatique des couleurs.
- La planche de correction retient le vert grise `#A8B8AA` comme quatrieme aplat discret. Il est utilise pour le panneau « Partage » et les actions de contact : sa valeur feutree est compatible avec l'ardoise `#5D648C`, le bleu gris `#CED7E2`, le fond teinte et l'encre `#25323D`, sans reprendre le citron ni le cuivre rejetes. Il ne porte jamais seul une information d'etat.
- Controle de theme valide pour transmission : « Passer au mode sombre » en clair et « Passer au mode clair » en sombre, accompagne respectivement d'une icone lune/soleil et d'un etat programmatique. A la future implementation, appliquer `prefers-color-scheme` au premier chargement uniquement en l'absence de choix enregistre ; persister ensuite le choix explicite de la personne (stockage local a documenter dans la politique de confidentialite si necessaire). Les deux themes disposent de jetons propres et ne resultent pas d'une inversion CSS.
- Regle CTA responsive validee : les libelles « Decouvrez l'univers du Testeur du Granier » et « Decouvrez nos experimentations » restent entiers, peuvent passer sur deux lignes (trois au maximum si un format plus etroit l'impose), conservent une cible d'au moins 44 px de haut et un espacement horizontal interne stable. Aucune troncature ni reduction sous une taille de lecture confortable.
- Catalogue de ton disponible : `assets/mockups/catalogue-formulations-humour-qualite-nocode.md`. Ses formulations sont uniquement contextuelles ou positives ; elles sont interdites dans les erreurs, informations critiques, avis legaux et instructions de securite. Les elements marques « Recommandee accueil » sont les candidats privilegies pour le hero et les panneaux.

## Decisions rejetees a memoriser
- 2026-09-20 : « Atelier calibre » et « Carnet de laboratoire » ne doivent plus etre proposes comme direction principale ; le sponsor les considere trop standard/IA.
- 2026-09-20 : conserver la palette Atelier calibre ne signifie pas reutiliser son traitement visuel standard. Le libelle « tableau de bord » et toute representation de donnees non reelles sont exclus de l'accueil.
- 2026-09-20 : l'accent citron `#D6E65E` est rejete pour la direction de reference.

## Contraintes produit ou techniques impactant l'UI
- Aucune stack frontend n'est encore retenue. JavaScript natif est privilegie si le besoin le permet ; React ou Vue demandent une justification explicite.
- Les contraintes techniques, contrats API et decisions d'architecture sont maintenus dans `handoff.md`.
- Viser les principes WCAG 2.2 AA applicables : clavier, focus visible, contrastes, HTML semantique, libelles de formulaire et alternatives utiles. ARIA ne remplace pas le HTML semantique.
- Le MVP ne charge aucun analytics, publicite, suivi ni script tiers non justifie. Toute evolution de mesure d'audience fera l'objet d'un lot RGPD distinct.

## Questions ouvertes
- Niveau exact d'humour acceptable hors de la note contextuelle du hero.
- Autorisation du futur registre de tracabilite des assets (licences, credits, texte alternatif).
- Choix de chargement des familles Space Grotesk et IBM Plex Sans et de leurs repli apres validation du lot frontend.

## Prochaines etapes design
- Faire valider la maquette hybride Atelier calibre, puis transmettre a Camity Front : `assets/mockups/accueil-hybride-atelier-calibre.svg`, palette et specification des boutons.
- Faire valider le raffinement comme direction de transmission : `assets/mockups/accueil-hybride-atelier-calibre-raffine.svg`, ses panneaux graphiques et le catalogue de formulations. Camity Front traduit ces repères en HTML semantique, CSS responsive et controles natifs sans reproduire les formes decoratives comme des widgets.
- Produire une maquette claire corrigee et sa variante sombre avec les panneaux de `direction-labo-puzzle.svg`, puis les faire valider avant transmission a Camity Front.
- Transmettre a Camity Front la planche de reference, la composition des panneaux, les jetons clair/sombre, le comportement de preference/persistance et les regles de retour a la ligne des CTA apres cadrage produit et validation de stack.
- Transmettre a Camity Front la maquette `/contact/`, ses tokens d'etat, les associations d'erreur, les cibles de 44 px, l'annotation honeypot non focalisable et la regle Turnstile production uniquement.