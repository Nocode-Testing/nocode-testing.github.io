# Build App — Journal de pilotage Dominion

Ce fichier est la base de communication entre le commanditaire et Dominion (orchestrateur) pour faire évoluer le projet `nocode-testing.com`. Il consigne : la revue des agents, les LLM recommandés par agent, les questions ouvertes de cadrage et les réponses obtenues.

Dernière mise à jour : 2026-09-20.

---

## 1. Revue des agents existants

### Scarce PO (exigences, US, Gherkin)
- Bien cadré : référentiel d'exigences + US Markdown + Gherkin, collaboration avec Mina Cybersécurité, Soso ArchiOps, Camity Front, Mikaya test et Rindel Dev prévue via `agents:`.
- **Recommandation** : rien de bloquant. Le dossier `qualite-logicielle/02-user-stories/` accueille désormais les futures US une fois le besoin cadré.

### Mina Cybersécurité (revue sécurité, pentest, CVE)
- Couvre la revue obligatoire de chaque nouvelle US, l'audit de code, les tests d'intrusion autorisés en local ou staging et la qualification des CVE applicables.
- **Recommandation** : conserver les tests actifs hors production et sous validation explicite du commanditaire. Les correctifs peuvent être appliqués par Mina uniquement sur demande explicite ; sinon ils sont transmis à Rindel Dev.

### Soso ArchiOps (architecture SI, DevOps, capacité)
- Valide les choix d'infrastructure, l'architecture client/serveur/données, le dimensionnement, Docker, CI/CD, serverless, l'observabilité, les sauvegardes et les coûts.
- Compare les options d'hébergement selon le besoin sans préférence préalable. Il peut produire les fichiers DevOps locaux sur demande, mais ne réalise aucune opération distante : il fournit à l'utilisateur des tutoriels vérifiables, notamment pour Vercel.
- **Recommandation** : le solliciter dès le cadrage lorsque les exigences de charge, disponibilité, données, sécurité, budget ou exploitation influencent la solution.

### Armindia UI (UX/UI, mockups)
- Bon cadrage : mémoire dédiée `handoff_UI.md`, propose 1 à 3 directions, garde la cohérence graphique et transmet la direction validée à Camity Front.
- **Recommandation** : aucune action requise. Armindia consulte `handoff.md` pour tenir compte des contraintes frontend de Camity et des contrats API de Rindel.

### Camity Front (développement frontend, TU)
- Propriétaire des interfaces HTML/CSS/JavaScript, avec JavaScript natif par défaut et React ou Vue uniquement lorsque la stack ou le besoin le justifie.
- Écrit les tests unitaires frontend, utilise `data-auto` pour les éléments importants sans sélecteur accessible stable et travaille avec Armindia UI, Rindel Dev et Mikaya test.
- **Recommandation** : aucune action requise. Mikaya challenge la couverture des TU et prend en charge la stratégie d'intégration/E2E.

### Rindel Dev (backend, API, architecture)
- Propriétaire des services backend, contrats API, accès aux données et décisions d'architecture applicative ; collabore avec Soso pour l'infrastructure et conserve une culture frontend pour synchroniser les contrats avec Camity.
- **Recommandation** : documenter les contrats et changements incompatibles, fournir des mocks représentatifs et déléguer l'implémentation d'interface à Camity Front.

### Mikaya test (stratégie de test, automatisation)
- Bon cadrage général (ISTQB, Playwright/TS, sélecteurs `[data-auto]`).
- **Recommandation** : aucune action requise. Mikaya lit le README et les handoffs, challenge les TU frontend et couvre les tests d'intégration, API et E2E.

### Dominion Orchestrateur (ce fichier)
- Rôle confirmé : coordination uniquement des 7 agents métier, validation systématique avant chaque chantier, suivi KPI dans `pilotage-projet.md` (à créer au premier chantier réel).
- **Recommandation** : aucune, le périmètre est cohérent avec les 7 agents métier existants.

---

## 2. LLM recommandés par agent (ordre 1 → 3)

Ces listes ont été ajoutées dans le frontmatter `model:` de chaque fichier `.agent.md` (utilisées dans cet ordre, la première disponible étant retenue).

| Agent | 1 | 2 | 3 | Justification courte |
|---|---|---|---|---|
| Scarce PO | Claude Sonnet 4.5 | GPT-5 | o4-mini | Rédaction structurée, raisonnement sur les exigences et le Gherkin ; repli rapide/économique si besoin. |
| Mina Cybersécurité | Claude Sonnet 4.5 | GPT-5 | o4-mini | Raisonnement approfondi pour l'analyse de risques, la revue de code, la qualification des CVE et la priorisation des remédiations. |
| Soso ArchiOps | Claude Sonnet 4.5 | GPT-5 | o4-mini | Raisonnement systémique, comparaison des compromis d'infrastructure, capacité et rédaction de procédures opératoires. |
| Armindia UI | GPT-5 | Claude Sonnet 4.5 | Gemini 2.5 Pro | Bon pour générer plusieurs directions créatives argumentées ; alternatives solides en raisonnement visuel. |
| Camity Front | Claude Sonnet 4.5 | GPT-5 | Grok Code Fast 1 | Solide sur JavaScript, CSS, composants React/Vue, accessibilité et tests unitaires frontend. |
| Rindel Dev | Claude Sonnet 4.5 | GPT-5 mini | Grok Code Fast 1 | Adapté à la conception d'API, aux contrats front/back, à l'architecture et au code serveur ciblé. |
| Mikaya test | Claude Sonnet 4.5 | GPT-5 | o4-mini | Rigueur et couverture de cas (ISTQB), bonne génération de code de test structuré (Playwright/TS). |
| Dominion Orchestrateur | Claude Sonnet 4.5 | GPT-5 | o4-mini | Raisonnement de planification/coordination le plus fiable en premier choix, repli économique pour les points de suivi courts. |

Note : la disponibilité réelle de ces modèles dépend de votre souscription Copilot ; si un modèle de la liste n'apparaît pas dans le sélecteur, le suivant de la liste sera utilisé automatiquement.

---

## 3. Interview de cadrage — projet nocode-testing.com

Le projet repart de zéro. Répondez directement sous chaque question, en sélectionnant une option ou en complétant le champ libre. Les réponses permettront de préparer le premier lot de travail dans une prochaine session ; aucun agent ne sera lancé pendant cette interview.

### 3.1 Objectif et périmètre initial
**Question** : quel rôle doit jouer le site au lancement ?

Options :
- [X] Vitrine de présentation de nocode-testing.com.
- [X] Blog ou base de connaissances.
- [ ] Catalogue d'offres/services avec prise de contact.
- [ ] Plateforme interactive (compte utilisateur, données ou fonctionnalités métier).
- [ ] Autre.

**Votre réponse / précisions** :

Il s'agit d'une page de présentation de mon entreprise, nocode-testing, dont le logo existe déjà et que je partagerais avec armindia-ui pour prendre en compte dans la charte graphique.
Et d'un blog professionnel "le testeur du granier", ou je partage, avec humour, mes experimentations sur le test en général !
Il y'aura aussi une section "contact" pour m'envoyer des messages, une page ressources avec des liens utiles, et une rubrique 'experimentation' ou je partagerais les applications que j'aurais réalisé à l'aide de l'IA

**Pages ou sections prioritaires au lancement** (ex. accueil, offre, à propos, contact, blog) :

- Page d'accueil
- Header avec les différentes rubriques
- Page de Blog avec un premier exemple d'article
- Experimentation une page d'accueil pour expliquer la page
- Ressources avec quelques liens (vers la taverne du testeur, le cftl, taia...) 
- A propos
- Footer avec : RGPD, lien linkedin
- Contact

### 3.2 Public et conversion attendue
**Question** : qui est le public prioritaire et quelle action doit-il accomplir ?

Options de public :
- [X] Professionnels du test logiciel.
- [X] Entreprises recherchant une prestation.
- [X] Communauté no-code / low-code.
- [X] Recruteurs ou partenaires.
- [ ] Autre.

Options d'action principale :
- [X] Prendre contact.
- [ ] Demander un devis ou un rendez-vous.
- [X] Consulter un contenu.
- [ ] S'inscrire à une newsletter.
- [ ] Créer un compte.
- [ ] Autre.

**Votre réponse / précisions** :

### 3.3 Contenu disponible
**Question** : quelle matière existe déjà et quelle part doit être produite ?

Options :
- [ ] Je possède les textes, médias et liens ; ils seront fournis dans le dépôt.
- [ ] Le contenu de l'ancien site peut être réutilisé.
- [ ] Seule une partie du contenu existe ; indiquer laquelle ci-dessous.
- [X] Le contenu initial doit être cadré et rédigé avec Scarce PO.

**Emplacement des sources existantes / précisions** :

### 3.4 Identité visuelle et accessibilité
**Question** : quelles contraintes visuelles doivent guider Armindia UI ?

Options :
- [ ] Charte existante (logo, couleurs, typographies) à fournir.
- [X] Logo existant, charte à concevoir.
- [ ] Identité complète à concevoir depuis zéro.
- [ ] Inspirations ou sites de référence à fournir.

**Contraintes d'accessibilité attendues** :
- [X] Bonnes pratiques usuelles (clavier, contrastes, HTML sémantique).
- [ ] Objectif WCAG 2.2 niveau AA.
- [ ] Autre niveau ou contrainte.

**Votre réponse / liens / précisions** :

Il faudrait une accessibilité entre le minimum et le niveau AA.
Je ne veux pas d'un site full accessible, mais respectant un minimum les lecteurs d'écran (aria-label et description partout), la navigation clavier, les contrastes...

**Complément du 2026-09-20** : la charte graphique existante est une base à respecter et à compléter si nécessaire. Le commanditaire est ouvert aux propositions d'Armindia UI.

### 3.5 Fonctionnalités, données et intégrations
**Question** : le site a-t-il besoin d'un backend ou de données dynamiques ?

Options :
- [ ] Site statique sans formulaire ni donnée dynamique.
- [ ] Site statique avec formulaire de contact via un service tiers.
- [X] Contenu éditorial géré dans des fichiers du dépôt.
- [X] CMS ou base de données.
- [ ] Comptes utilisateurs, authentification ou espace privé.
- [ ] API, paiement, calendrier, analytics ou autre intégration.

**Votre réponse / intégrations envisagées / données traitées** :

Le site nécessitera une base de donnée pour les articles.
Tout le code sera cependant assez statique dans l'ensemble, sauf la création de microapp en javascript qui pourront rajouter du dynamisme.
On peut envisager un backoffice avec connexion pour modifier et mettre à jour les articles par la suite.
Le projet sera dans Github puis utilisé par Vercel.
Certains asset seront crées par la suite, comme des modules de quizz et autre... un mini forum, des commentaires ... mais pas dans le MVP (mais à garder en tête)
On n'utilise pas de CMS externe, on crée tout de zéro.
Et tout doit être en https.
Le site aura une recette et une production (les 2 disponibles sur Vercel) afin de pouvoir réaliser des tests
Une pipeline devra être mise en place sous Github CI ou Vercel (selon tes recommandations) afin de pouvoir déployer les 2 plateforme efficacement et rapidement.
La recette ne pourra être accessible que via un mot de passe.

### 3.6 Stack, hébergement et budget
**Question** : quelles contraintes techniques et financières s'appliquent ?

Options de stack :
- [X] HTML/CSS/JavaScript natif, sans phase de build.
- [ ] Générateur de site statique léger (ex. Eleventy, Astro).
- [ ] Framework frontend (React, Vue ou autre), à justifier par le besoin.
- [X] À recommander par Soso ArchiOps et Camity Front.

Options d'hébergement :
- [ ] GitHub Pages.
- [X] Vercel.
- [ ] Autre hébergeur : à préciser.
- [X] À recommander selon les besoins.

**Budget mensuel cible et contraintes d'hébergement** :

Pas vraiment de limite, mais on reste sur un petit site.
J'ai déjà le nom de domaine https://www.nocode-testing.com/

**Complément du 2026-09-20** : le trafic attendu est celui d'un petit site institutionnel ; aucune charge importante n'est anticipée au MVP. Les navigateurs cibles prioritaires sont Chrome et Firefox.

### 3.7 Mesure, sécurité et conformité
**Question** : quels services et obligations doivent être anticipés ?

Options :
- [ ] Aucun suivi d'audience au lancement.
- [X] Analytics respectueux de la vie privée.
- [ ] Google Analytics ou outil équivalent.
- [ ] Formulaire collectant des données personnelles.
- [X] Bandeau cookies, politique de confidentialité ou mentions légales nécessaires.
- [X] Exigences spécifiques (RGPD, hébergement, sécurité) : à préciser.

**Votre réponse / précisions** :
Penser et mettre en place les règles de respect du RGPD, avec une page indiquant les règles mise en place.

**Complément du 2026-09-20** : les données de contact seront conservées pendant la durée minimale légalement applicable. Le service d'e-mail transactionnel reste à choisir ; la compatibilité avec l'envoi SMTP OVH est une piste à étudier, sans engager de secret dans le dépôt.

### 3.8 Qualité, tests et échéance
**Question** : quel niveau de qualité visez-vous pour la première version et pour quand ?

Options de tests :
- [X] Vérifications manuelles avant publication.
- [ ] Tests unitaires des comportements interactifs.
- [ ] Tests E2E de fumée sur les parcours critiques.
- [X] Tests unitaires et E2E avec seuil de couverture à définir.

**Échéance ou jalon de première mise en ligne** :

Quand on sera pret, nous partirons sur un fonctionnement agile, avec une version de recette et une version de production.
A chaque nouvelle mise à jour, on pousse sur la recette, on valide et on pousse en prod (et on valide)

**Complément du 2026-09-20** : Mikaya test doit proposer un niveau de couverture proportionné, sans surqualité. La promotion en production intervient uniquement après validation explicite de la plateforme de recette par le commanditaire.

**Niveau de priorité** :
- [X] Publier très vite une version minimale.
- [ ] Privilégier une base solide avant publication.
- [ ] Équilibrer délai et qualité.

### 3.9 Gouvernance et validation
**Question** : qui valide les décisions de contenu, design et technique, et quel rythme de validation préférez-vous ?

Options :
- [ ] Je valide chaque lot de travail avant son lancement.
- [X] Je valide les grandes étapes, Dominion peut enchaîner les sous-tâches explicitement approuvées.
- [ ] Autre processus : à préciser.

**Votre réponse / personnes impliquées / disponibilité** :

Chaque mise en place part d'un premier besoin partagé avec Dominion.
Mais on part en incrémentale, avec chaque étape réfléchie et validée ensemble.
Je ne demanderais jamais : "fais moi un site complet" mais plutôt "faisons la page d'accueil avec le header..."
Et le site va se construire petit à petit. Il est donc important que nous respections ce process (merci de remettre au propre ce process)

## 4. Réponses du commanditaire
- Réponses intégrées dans les sections 3.1 à 3.9 le 2026-09-13.

## 5. Décisions actées
- MVP : vitrine `nocode-testing` avec accueil, header, blog "Le testeur du granier" (un premier article), experimentations IA, ressources, a propos, contact, footer RGPD et lien LinkedIn.
- Public : professionnels du test, entreprises, communaute no-code/low-code, recruteurs et partenaires. Objectifs prioritaires : consulter les contenus et prendre contact.
- Contenu initial : a cadrer et rediger avec Scarce PO. Logo existant a transmettre a Armindia UI ; charte graphique a concevoir.
- Identite visuelle : elements de marque disponibles dans `assets/brand/` : logo couleur, noir et blanc, blanc et charte graphique PDF. Le SVG couleur est la variante de reference par defaut.
- Donnees : le MVP publie un premier article Markdown. Une base de donnees et un backoffice authentifie sont reportes apres le MVP ; commentaires, forum, quiz et autres micro-applications restent egalement hors MVP mais a anticiper dans les choix structurants.
- Hebergement : code sur GitHub, deploiement Vercel en HTTPS, avec recette protegee par mot de passe et production publique.
- Domaine : le commanditaire controle le DNS de `nocode-testing.com` et peut le configurer pour Vercel.
- Contact : formulaire avec `nom`, `e-mail`, `societe`, `sujet` et `message`, a envoyer a `michael@nocode-testing.com`. Le ton des libelles doit etre convivial et moins formel. Un prestataire transactionnel compatible Vercel, si possible gratuit, sera recommande lors du lot technique.
- Antispam : honeypot, limitation de debit et validation serveur recommandes au MVP, sans CAPTCHA visible. Un CAPTCHA sera reconsidere seulement si des abus sont observes.
- Recette : protection native Vercel, accessible au commanditaire, a Mikaya test et aux testeurs designes.
- Qualite : verifications manuelles, tests unitaires et E2E pour les parcours critiques. La CI est bloquante lorsqu'un lint, un test ou le build echoue.
- Conformite : entreprise francaise, page RGPD et mentions legales requises. Informations connues : NOCODE TESTING, SAS, SIREN 943 002 451, SIRET 943 002 451 00012, 8 ter rue de la penissiere, 85610 Cugand. L'adresse e-mail de confidentialite reste a fournir et les informations legales devront etre verifiees humainement avant publication.
- Analytics : module maison leger envisage apres le MVP ; aucun analytics n'est integre au MVP.
- Gouvernance : construction incrementale. Chaque besoin est cadre et valide avec Dominion ; les sous-taches approuvees peuvent etre enchainees, puis chaque increment est valide en recette avant sa promotion en production.

## 5.1 Processus incremental de reference
1. Le commanditaire partage un besoin limite (ex. "accueil et header").
2. Dominion reformule le besoin, consulte les documents de contexte et propose un lot : perimetre, agents, LLM, dependances, risques et criteres de sortie.
3. Le commanditaire valide explicitement le lot avant tout lancement d'agent.
4. Les agents produisent uniquement les livrables du lot et transmettent leurs decisions, risques et validations a Dominion.
5. Dominion consolide les resultats et demande la validation du commanditaire avant les actions suivantes.
6. Le code du lot passe les controles CI puis est deploye en recette.
7. Le commanditaire valide la recette ; la production ne suit qu'apres cette validation explicite.
8. Dominion met a jour les handoffs, le suivi de projet, les KPI et les decisions avant l'increment suivant.

## 5.2 Analytics — decision actee

**Recommandation : Plausible Cloud en premier choix.** Il est leger, sans cookie par defaut, respectueux de la vie privee et simple a integrer. Il convient au besoin initial de mesurer les pages et sources de trafic, sans construire ni maintenir un systeme de collecte personnel.

Alternatives :
- **Matomo Cloud** : bon choix lorsque des rapports plus complets ou davantage de controle sur les donnees sont necessaires, au prix d'une configuration et d'un cout potentiellement superieurs.
- **Module maison** : non recommande pour le MVP. Il implique un endpoint, une base de donnees, de la securite, de la retention, de la transparence RGPD et de la maintenance ; le gain de performance par rapport a un script Plausible est trop faible pour justifier ce cout maintenant.

Decision :
- [X] Construire un module maison apres une etude dediee (hors MVP).
- [X] Aucun analytics pendant le MVP.

## 5.3 Questions restantes avant le premier increment
1. **Adresse de confidentialite** : quelle adresse e-mail doit figurer dans les mentions legales et la politique de confidentialite pour les demandes RGPD ?
2. **Duree de conservation** : la duree minimale legalement applicable doit etre precisee par une validation juridique humaine avant publication ; elle ne peut pas etre deduite du projet seul.
3. **E-mail transactionnel** : Soso ArchiOps et Mina Cybersécurité instruisent la compatibilite SMTP OVH, ainsi que les alternatives Vercel compatibles, leurs limites, la protection des secrets et les implications RGPD.

## 5.4 Réponses du commanditaire — 2026-09-20
- La charte graphique existante est une base ; Armindia UI peut proposer des compléments à valider.
- La charge cible est celle d'un petit site institutionnel, sans besoin de dimensionnement important au MVP.
- La conservation des données personnelles doit respecter la durée minimale légalement applicable ; une validation juridique humaine demeure nécessaire.
- L'utilisation du SMTP OVH est une piste pour l'envoi des e-mails de contact, à comparer aux services transactionnels compatibles Vercel.
- Mikaya test doit recommander une couverture pragmatique, sans surqualité.
- La production ne peut être promue qu'après validation explicite de la recette par le commanditaire.
- Les navigateurs cibles prioritaires sont Chrome et Firefox.

## 5.5 Lot de cadrage validé — 2026-09-20
Le commanditaire a autorisé le lancement des chantiers suivants. Ils ne comprennent aucune implémentation applicative ni aucune opération distante.

| Chantier | Agent | Livrable attendu | Modèle retenu | Statut |
|---|---|---|---|---|
| UX/UI | Armindia UI | Première maquette exploratoire de l'accueil et du header | GPT-5 (repli Claude Sonnet 4.5) | Lancé |
| Qualité | Mikaya test | Stratégie de test proportionnée au MVP | Claude Sonnet 4.5 (repli GPT-5) | Lancé |
| Sécurité | Mina Cybersécurité | Stratégie de tests de sécurité et exigences RGPD techniques | Claude Sonnet 4.5 (repli GPT-5) | Lancé |
| Architecture / CI | Soso ArchiOps | Stack, architecture Vercel et workflow CI/CD recette vers production | Claude Sonnet 4.5 (repli GPT-5) | En attente des avis sécurité et test |

Les résultats de ces chantiers seront consolidés dans de nouvelles sous-parties de ce document. Les questions ouvertes des experts seront remontées au commanditaire avant toute décision structurante ou implémentation.

---

## 6. Audit de préparation — 2026-09-13

### État des agents
- **Prêt** : les huit rôles sont présents et leurs périmètres sont désormais complémentaires : pilotage, exigences, sécurité, architecture/exploitation, UX/UI, frontend, backend et tests.
- **Corrigé lors de cet audit** : Scarce PO consulte maintenant le README, les handoffs et le suivi `build-app.md` avant toute évolution d'exigence. La séparation entre rôle et vérifications de contexte de Dominion a aussi été rétablie.
- **À confirmer** : les noms des modèles configurés dans les frontmatters doivent apparaître dans le sélecteur Copilot de l'organisation. L'ordre de repli est correct, mais il dépend des licences et de la disponibilité effective des modèles.

### État de la documentation
- **README** : mis à jour avec le statut de cadrage, l'organisation multi-agent, les documents de référence et l'absence actuelle de scripts de développement.
- **handoff.md** : mis à jour avec les faits techniques confirmés, la structure, les responsabilités, les blocages et les prochaines étapes.
- **handoff_UI.md** : mis à jour avec le contexte de reconstruction et les contraintes connues ; les éléments de design restent intentionnellement ouverts.
- **build-app.md** : demeure la source de vérité pour les réponses du commanditaire et les décisions de cadrage.

### Conditions avant le premier chantier
1. Répondre aux sept questions de la section 3, au minimum : nature du site, stack, hébergement, contenu et identité visuelle.
2. Choisir et faire valider le premier lot : cadrage produit (Scarce PO), architecture (Soso ArchiOps) et/ou UX exploratoire (Armindia UI).
3. Ne lancer les agents choisis qu'après validation explicite de ce lot par le commanditaire.

### KPI de départ
| Indicateur | Valeur | Statut |
|---|---:|---|
| User stories définies | 0 | Non démarré |
| Couverture TU | Non mesurable | Aucune stack ni suite de tests |
| Couverture TI/E2E | Non mesurable | Aucune stack ni suite de tests |
| Anomalies ouvertes | 0 connue | Aucun code applicatif à auditer |
| Risques de sécurité/CVE ouverts | Non mesurable | Aucune dépendance installée |
| Décisions de cadrage validées | 0 | En attente du commanditaire |

---

## 7. Livrables du lot de cadrage — 2026-09-20

Ces livrables sont des recommandations d'experts. Les éléments signalés « à valider » ne deviennent pas des décisions de projet avant accord explicite du commanditaire.

### 7.1 Première maquette — Armindia UI

**Livrable :** wireframe exploratoire de l'accueil et du header, sans code. Le logo couleur est la référence. Les actifs de marque confirment notamment le bleu ardoise `#5D648C` et le bleu gris clair `#CED7E2`.

**Direction recommandée : « Atelier de test ».** Cette direction articule expertise professionnelle, contenus éditoriaux et expérimentations IA sans apparence de produit SaaS générique.

```text
[Liens d'évitement]
[Header : logo] Accueil | Blog | Expérimentations IA | Ressources | À propos [Contact]

[Hero sur fond clair bleuté]
[NOCODE TESTING]
[H1 : Tester mieux. Explorer autrement.]
[Expertise test logiciel, retours de terrain et expérimentations IA.]
[Découvrir le blog] [Prendre contact]                  [Détail du logo]

[Repères : Test logiciel] [Veille et ressources] [Expérimentations IA]
[Accès éditoriaux : Le testeur du granier | Expérimentations IA | Ressources]
```

- Header desktop : logo à gauche, navigation à six entrées, seul `Contact` est un bouton. L'entrée active est identifiable autrement que par la couleur.
- Header mobile : bouton de menu et panneau vertical pleine largeur ; focus contenu dans le panneau, restauré sur le bouton à la fermeture.
- CTA : principal `Découvrir le blog`, secondaire `Prendre contact`.
- Style : bleu de marque pour l'ancrage, bleu gris clair pour les surfaces, fond neutre de lecture. Une police sans sérif humaniste est recommandée pour le texte, avec une police de titre éditoriale sobre, à choisir selon licence, performance et support du français. Un accent chaud désaturé est possible après validation.
- Accessibilité : lien d'évitement, HTML sémantique, navigation clavier, focus visible, contraste de texte d'au moins 4.5:1, zone tactile de 24 x 24 px minimum, zoom 200 %, respect de `prefers-reduced-motion`. Le logo porte une alternative de marque seulement lorsqu'il est cliquable ; il est décoratif sinon.

**Alternatives explorées :**
- « Carnet de terrain » : plus éditorial, centré sur le blog ; l'activité de l'entreprise est moins immédiatement lisible.
- « Signal de confiance » : plus institutionnel et orienté prestation ; réduit la singularité du blog et de l'expérimentation.

**Décisions à valider :** direction « Atelier de test », hiérarchie des CTA, navigation sans sous-menu au MVP, emploi du logo couleur sur fond clair et éventuel accent de palette.

### 7.2 Stratégie de test — Mikaya test

**Principe :** stratégie proportionnée au MVP. Les pages Markdown et le CSS ne justifient ni TU exhaustifs ni snapshots massifs ; le build, les parcours E2E et la recette manuelle sont les contrôles principaux.

| Niveau | Objet | Responsable | Attendu MVP |
|---|---|---|---|
| TU | Comportements JavaScript et validations client | Camity Front, revus par Mikaya | Ciblés sur l'interactif |
| Intégration/API | Fonction contact, validation serveur, antispam, fournisseur e-mail | Rindel Dev et Mikaya | Obligatoire avec le formulaire |
| E2E | Parcours utilisateur sur recette | Mikaya test | Smoke et régression critique |
| Manuel | Rendu, contenu, liens, responsive et expérience éditoriale | Mikaya, commanditaire, testeurs désignés | Avant chaque promotion |
| Accessibilité | Socle WCAG 2.2 AA applicable | Camity Front et Mikaya | Automatisation ciblée et contrôles manuels |

**Outillage recommandé, dépendant de la stack :** Playwright avec TypeScript et projets Chrome/Firefox ; `@axe-core/playwright` sur les pages et états importants ; Vitest pour une stack JavaScript avec build, ou `node:test` pour du JavaScript natif minimaliste. Les tests privilégient rôles et noms accessibles, puis `[data-auto]` uniquement en dernier recours.

**Seuils initiaux proposés :** 80 % lignes/fonctions pour le code serveur du contact et les utilitaires métier ; 70 % pour le JavaScript frontend interactif ; 100 % des scénarios E2E critiques listés. Aucun seuil de couverture globale pour les pages statiques et Markdown. Une baseline est établie au premier incrément ; les seuils ne sont bloquants que lorsque les surfaces concernées existent.

**CI et critères de sortie :** installation reproductible, lint, TU/intégration applicables, build, déploiement recette protégé, smoke Playwright Chrome et Firefox. Avant production : E2E critiques verts, aucune anomalie bloquante ou majeure, contrôle clavier/focus/libellés, aucune violation axe critique ou sérieuse non justifiée, puis validation explicite de recette par le commanditaire. La production reçoit ensuite un smoke sans donnée personnelle.

**Scénarios critiques initiaux :** navigation et logo, article Markdown, liens de ressources, parcours clavier et focus, structure et alternatives, validation client/serveur du contact, succès/erreur du fournisseur e-mail, honeypot et limitation de débit, protection de recette, absence d'analytics au MVP.

**KPI :** réussite CI, scénarios E2E verts/total, défauts par sévérité, délai recette-validation, violations axe critiques/sérieuses et couverture ciblée des modules interactifs/serveur.

### 7.3 Stratégie de test sécurité — Mina Cybersécurité

**Avis : Conforme sous réserves.** Le MVP statique réduit l'exposition. Les priorités sont le futur formulaire, les secrets, le Markdown, les dépendances et la CI.

| Actif / flux | Menaces prioritaires | Mesures attendues |
|---|---|---|
| GitHub et CI | Secret commité, dépendance compromise, workflow trop privilégié | Secrets hors dépôt, droits minimaux, revue PR, audit et détection de secrets |
| Recette Vercel | Accès non autorisé ou indexation | Protection Vercel vérifiée, accès restreint, aucune donnée réelle |
| Formulaire | Spam, injection, abus, fuite | Endpoint serveur, allowlist, validation, encodage, limite de débit et honeypot |
| Service e-mail | Fuite de clé ou conservation non maîtrisée | Secrets Vercel, TLS, expéditeur contrôlé, revue contrat/logs |
| Markdown et liens | XSS et liens malveillants | HTML brut désactivé, assainissement exceptionnel, revue des liens |

**Exigences vérifiables :**
- Seule une fonction serveur envoie l'e-mail ; elle valide strictement les cinq champs, leurs longueurs et le format de l'adresse.
- Aucun contenu utilisateur n'est interprété comme HTML. Le honeypot donne une réponse neutre et la limite de débit est appliquée côté serveur avec un comportement documenté.
- Secrets séparés recette/production, stockés hors dépôt et inaccessibles au navigateur ; procédure de rotation avant la mise en production.
- HTTPS et en-têtes de sécurité adaptés : CSP, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy` et protection contre l'encadrement non voulu.
- Le Markdown interdit le HTML brut ; les liens ouverts dans un nouvel onglet portent `rel="noopener noreferrer"`.
- La CI exécute lockfile, lint, tests, build, audit qualifié des dépendances et détection de secrets. Les actions sont épinglées à une révision immuable et les permissions minimisées.

**Test actif futur en recette :** uniquement après autorisation explicite du commanditaire, sur recette protégée, avec données fictives et scénario non destructif. Il couvrira accès recette/prévisualisations, HTTPS et en-têtes, soumissions contrôlées, faible test de limitation, exposition de secrets et rendu Markdown. Un risque confirmé élevé ou critique bloque toute promotion.

**RGPD technique :** la collecte est limitée aux cinq champs annoncés. Les journaux ne contiennent ni message, ni adresse complète, ni secret. La durée de conservation, la suppression, la base légale, l'adresse de confidentialité et les sous-traitants exigent une validation humaine compétente ; cette recommandation ne vaut pas avis juridique.

### 7.4 Étude de stack et architecture — Soso ArchiOps

**Recommandation à valider : Eleventy, HTML/CSS/JavaScript natif et Node.js 22 LTS.** Eleventy apporte les gabarits, collections Markdown et métadonnées utiles au blog tout en livrant du HTML statique servi par le CDN Vercel. Node 22 LTS remplace Node 18, désormais obsolète, sous réserve de compatibilité des outils retenus.

| Option | Verdict | Justification |
|---|---|---|
| HTML/CSS/JS sans build | Acceptable | Peu de dépendances mais duplication et gestion éditoriale manuelle |
| Eleventy | **Recommandé** | Markdown natif, gabarits réutilisables, sortie HTML simple |
| Astro | Alternative | À réévaluer si les micro-apps deviennent importantes |
| VitePress | Non retenu | Moins naturel pour une vitrine éditoriale |
| React/Vue/Next/Nuxt | Non retenu MVP | Complexité injustifiée |

**Architecture cible :** contenus Markdown versionnés dans GitHub, générés statiquement par Eleventy et distribués par Vercel. La future fonction Vercel de contact est la seule à posséder le secret SMTP/API et à appeler le fournisseur e-mail. Base, backoffice, forum et commentaires restent hors MVP et devront être instruits comme sous-systèmes distincts.

**Règles Markdown :** front matter avec identifiant, titre, date, résumé, tags, statut et slug ; validation au build des champs, slugs, dates et liens internes ; HTML brut, scripts et iframes interdits ; texte alternatif requis pour les images informatives ; prévisualisation recette obligatoire.

**Contact :** `POST` same-origin vers fonction Vercel, validation serveur, honeypot, limite de débit durable hors mémoire serverless, expéditeur contrôlé et logs minimisés. SMTP OVH est à comparer à un prestataire API sur connectivité serverless, authentification, quotas, SPF/DKIM/DMARC, délivrabilité, DPA, localisation et réversibilité.

### 7.5 Workflow CI/CD recette puis production — Soso ArchiOps

**Décision à valider : GitHub Actions contrôle la CI/CD ; Vercel est la cible de déploiement.** Aucun déploiement production n'est un effet de bord d'un merge seul.

1. Les branches `feature/*` portent les incréments ; `recette` et `main` sont protégées. Une revue humaine et les statuts requis précèdent chaque fusion.
2. Toute pull request exécute installation depuis lockfile, lint, TU pertinents, build, E2E Playwright Chrome/Firefox, axe ciblé, audit des dépendances et détection de secrets.
3. Une fusion vers `recette` déclenche les contrôles sur le commit fusionné, puis son déploiement sur Vercel Recette protégé et un smoke HTTPS/routes essentielles.
4. Mikaya, les testeurs désignés et le commanditaire réalisent la recette manuelle. La validation explicite du commanditaire est consignée dans le suivi.
5. Une pull request `recette` vers `main` est revue. Le déploiement utilise l'environnement GitHub `production`, soumis à approbation humaine, puis déploie le même commit validé vers Vercel Production.
6. Un smoke public sans donnée personnelle est exécuté après déploiement. La version, l'URL et la décision de promotion sont consignées.
7. En cas d'incident, un déploiement Vercel validé est redéployé après approbation, suivi d'un smoke et d'une analyse documentée. Aucune restauration de base n'est concernée au MVP.

**Environnements :** local avec données fictives ; CI sans secret hors déploiement ; recette avec secrets dédiés et données fictives/anonymisées ; production avec secrets distincts. Les previews Vercel doivent être protégées. GitHub Environments et Vercel séparent les secrets ; aucune variable publique ne contient de donnée sensible.

**Capacité et coûts :** le CDN Vercel suffit au trafic attendu. Les coûts à surveiller sont l'offre Vercel nécessaire à la protection de recette, les minutes GitHub Actions, l'e-mail transactionnel/SMTP et les futurs besoins de stockage. Réévaluer lors de l'arrivée de plusieurs éditeurs, d'un volume éditorial important, de spam/incidents e-mail, de comptes/commentaires/forum ou d'objectifs de disponibilité chiffrés.

### 7.6 Questions consolidées à trancher

1. Validez-vous la direction UI « Atelier de test », le CTA principal vers le blog et un éventuel accent chaud désaturé ?
- J'aime bien la direction "atelier de test", "laboratoire...", avoir un ptit coté "experimental" me plait. 
- Serais t'il possible de générer quelques maquette graphiques ? 
2. Quelle formulation décrit le mieux l'activité dans le hero : « test logiciel », « qualité logicielle », « accompagnement QA » ou une autre ? Le ton humoristique du blog doit-il être perceptible dès l'accueil ?
- Qualité Logicielle 
- On peut voir le ton humoristique dès le début (sans être trop lourd)
3. Avez-vous des photos/captures d'expérimentations à intégrer ou faut-il lancer sans média externe ? Le libellé `Expérimentations IA` est-il définitif ?
- Plutôt que "experimentation IA", j'aurais mis "Labo Test & IA"
- Je n'ai pas de photos, si tu as moyen de me générer des images adaptées ou alors trouver des images dans des banques d'images gratuites, je suis preneur.

4. Une violation axe critique ou sérieuse doit-elle bloquer la recette dès le premier incrément ? Faut-il une vérification mobile manuelle systématique ?
- Cela doit bloquer la recette avant toute mise en production > Une anomalie majeure ou bloquante ne permet pas de mettre en production dès le premier incrément
- A noter, j'ai crée un bug tracker dans Github https://github.com/orgs/Nocode-Testing/projects/1/views/1 > A voir si on peut l'utiliser pour loguer des anomalies detectées. > Mikaya pourrait avoir les moyens de créer des anomalies directement dans l'outil ?
- A rajouter au process, les anomalies remontées doivent faire l'effet d'une validation de priorité par l'utilisateur humain (mais une proposition de priorité peut déjà être réalisée)
5. Où tracer la validation de recette : GitHub, `pilotage-projet.md`, ou les deux ? Les liens externes doivent-ils être contrôlés à chaque CI malgré les faux échecs réseau possibles ?
- Prévoir la création d'un dossier "Qualité logicielle" ou on retrouvera exigences > US > Tests Case > campagnes de tests > statut des exécution de tests et de campagnes le tout en format MD (j'ai prévu d'experimenter la création d'un outil permettant de rendre visible les campagnes de tests)
- A noter que j'ai aussi créé un Kanban dans Github https://github.com/orgs/Nocode-Testing/projects/2/views/1?system_template=kanban qu'il serait intéressant d'utiliser > Scarce pourrais avoir les moyens de créer des tickets dans ce dernier ?
6. Quelle boîte de réception distincte peut recevoir les e-mails de recette ? Quel niveau de détail de diagnostic est acceptable sans conserver de données personnelles ?
- test_recette@nocode-testing.com (Si tu as un tuto pour créer un alias supplémentaire dans microsoft je suis preneur)
7. Quelle adresse publiera les demandes de confidentialité/RGPD, quelle durée exacte de conservation sera validée juridiquement, et qui est habilité à accéder à GitHub, Vercel, DNS et secrets ?
- rgpd@nocode-testing.com (Si tu as un tuto pour créer un alias supplémentaire dans microsoft je suis preneur)
8. Confirmez-vous que le futur test actif de sécurité se limitera à la recette protégée avec données fictives, et préférez-vous une indisponibilité temporaire du formulaire au risque de spam en cas de limite atteinte ?
- Oui, il faut un blocage en cas de spam. Il faudrait peut être rajouter un captcha en production, qu'on ne mettra pas en recette (pour les tests automatisés) > Prendre un captcha sympa et pas trop invasif pour les utilisateurs.
9. Validez-vous Eleventy + JavaScript natif + Node.js 22 LTS, GitHub Actions et la stratégie de branches `feature/*` / `recette` / `main` ?
- A voir pour Eleventy, cela voudrait dire qu'on n'utilise pas de base de donnée c'est cela? le choix vous parait cohérent? 
-- Si oui, on part sur cette solution, mais il faudra vraiment pouvoir avoir l'affichage html que l'on souhaite à partir du markdown.
-- A noter aussi, que j'aimerais pouvoir mettre certains contenu directement en production > Donc soit on a une base de prod qu'on peut mettre en recette, soit on a la possibilité de livrer des contenus éditoriaux directement en production.
- Merci de réfléchir à cette question avec ces nouvelles informations avant de prendre Eleventy comme dernière solution.
10. Quel niveau Vercel est disponible ou acceptable pour protéger recette et previews ? Qui approuve les déploiements de production ? Souhaitez-vous un sous-domaine stable tel que `recette.nocode-testing.com` ?
- Je souhaite un sous domaine stable oui.
- Je ne sais pas si Vercel gère bien tout cela, si tu as moyen de récupérer les informations ce sera un plus (et la doc pour bien faire attention)
- Déploiement de production validé par un utilisateur humain uniquement (mettre en place le process clairement)
- A NOTER (demande supplémentaire) : tout les process du projet doivent être documenté séparement dans un dossier "Processus" avec les différentes actions à réaliser.
11. Pour l'e-mail, faut-il privilégier traitement UE, budget mensuel nul ou délivrabilité/observabilité ? Le commanditaire autorisera-t-il la mise à jour DNS OVH dans le lot de déploiement dédié ?
- Rien à changer coté OVH, juste utiliser le smtp ovh en m'indiquant quelles informations tu aurais besoin.
- Mail de contact : contact@nocode-testing.com

### 7.6 Réponse Armindia UI aux retours sponsor — 2026-09-20

**Confirmation et affinage.** La direction devient **« Atelier de test / laboratoire »** : une vitrine professionnelle ancrée dans la qualite logicielle, rendue singuliere par des reperes de protocole (fiches, statuts, observations, grille de carnet) plutot que par un imaginaire scientifique caricatural. Le bleu ardoise de la marque reste l'ancrage ; le bleu gris organise les surfaces ; un accent cuivre desature reserve aux statuts, annotations et appels ponctuels apporte le cote experimental sans concurrencer les CTA. Le ton humoristique apparait des l'accueil dans une courte note contextuelle, jamais dans un libelle de navigation, un CTA ou une information critique.

**Maquettes statiques reutilisables.** Deux planches SVG, chacune avec une vue desktop et une vue mobile, ont ete ajoutees :
- `assets/mockups/accueil-atelier-calibre.svg` : direction recommandee. Structure claire, hero « Qualite logicielle », tableau de protocole et humour sobre. Le CTA principal reste le blog ; `Labo Test & IA` remplace `Experimentations IA` dans la navigation et les contenus.
- `assets/mockups/accueil-carnet-laboratoire.svg` : alternative plus editoriale. Le blog devient le geste principal, avec une grille de carnet et une fiche d'experience plus presente.

**Recommandation.** Retenir **Atelier calibre** comme base de l'accueil et du header. Il equilibre le positionnement entreprise, le blog et le futur Labo Test & IA sans faire passer le site pour un outil SaaS ni un blog uniquement. Reprendre le principe de la fiche de laboratoire de la seconde piste dans les cartes de contenu, pas dans toute la page.

**Strategie d'assets.** Aucun visuel decoratif generique (fioles stock, personnes en blouse, ecrans abstraits) ne sera utilise. Les medias prioritaires sont : captures reelles et annotees des futures experimentations, schemas de protocole et donnees fictives explicitement etiquetees, extraits d'interface recrees pour expliquer une methode, puis portraits ou photos de situations de travail seulement lorsqu'ils apportent du contexte editorial. Pour les visuels externes, selectionner uniquement des photos documentaires pertinentes sous licence CC0 ou Unsplash License, conserver URL, auteur, date de telechargement et licence dans un registre d'assets, et verifier que la licence couvre le contexte commercial. Pour les images generees, documenter l'outil, le prompt, la date et la licence applicable ; ne pas representer une personne reelle sans autorisation. Chaque image informative recevra un texte alternatif qui explique l'information utile ; une image decorative aura `alt=""`. Optimiser les fichiers et fournir des dimensions reservees au rendu pour limiter le decalage visuel.

**Questions encore bloquantes pour Dominion.**
1. Validez-vous la maquette `accueil-atelier-calibre.svg` comme direction de reference et l'accent cuivre desature propose ?
- Cette page manque clairement de fantasy et reste trop dans les standard de ce qui se fait actuellement, généré par IA.
-- Essai de me proposer quelques choses moins "communs" plus "graphiques" avec quelques image un peu laboratoire !
-- A noter que mon logo se rapproche un peu du jeu Portal de Valve, donc n'hésites pas à prendre quelques inspiration dans la direction artistique.
-- Soit plus "foufou" :D  
- Le code couleur correspondant au logo me parait parfait
- J'aimerais que tu y incorpore mon logo dans le header

2. Quel niveau d'humour est accepte dans les contenus d'accueil : uniquement une note courte de laboratoire, ou aussi des titres et descriptions de cartes ?
- Titre et description des cartes (ce que tu propose est sympa)
- Rester dans la qualité logicielle et le nocode cependant.
3. Autorisez-vous la constitution d'un registre d'assets dans le futur lot contenu afin de tracer licences, credits et alternatives textuelles ?

**Réponses du commanditaire :** la proposition actuelle est rejetée car trop standardisée. Armindia UI doit proposer des maquettes plus graphiques, expressives et expérimentales, avec des visuels de laboratoire, une inspiration libre de l'univers visuel de Portal sans reprendre d'élément protégé, le logo dans le header et les couleurs existantes. L'humour léger est autorisé dans les titres et descriptions de cartes tant qu'il reste lié à la qualité logicielle et au no-code. La création d'un registre d'assets est autorisée.
- oui pour le registrer d'asset

### 7.7 Réponses spécialisées aux compléments du commanditaire — 2026-09-20

**Qualité et anomalies — Mikaya test.** Le Project GitHub `#1` doit être le tableau de bord des anomalies, chaque anomalie restant une GitHub Issue afin de conserver description, preuves et échanges. L'agent propose sévérité et priorité ; un humain valide la priorité avant traitement. Les anomalies bloquantes ou majeures, les violations axe critiques ou sérieuses non justifiées, les E2E critiques ou une CI en échec interdisent toute promotion. Les liens externes doivent être contrôlés de manière non bloquante afin d'éviter les faux échecs réseau. La recette utilise exclusivement `test_recette@nocode-testing.com` avec des données fictives.

Le dossier `qualite-logicielle/` est organisé par workflow : `01-exigences/`, `02-user-stories/`, `03-cas-de-test/`, `04-campagnes/`, `05-executions/`, `06-anomalies/` et un `README.md` de traçabilité. La chaîne est `REQ -> US -> CT -> CAMP -> EXEC`, complétée par les liens vers les Issues. GitHub Project sert à piloter l'exécution ; Markdown contient les critères et preuves. La création distante d'issues par agent requiert ultérieurement une identité technique dédiée, des droits minimaux, une autorisation explicite et une revue humaine ; l'agent peut sinon préparer les tickets.

**Sécurité — Mina Cybersécurité.** Le CAPTCHA production seulement est acceptable s'il complète la validation serveur, le honeypot et la limitation de débit. Cloudflare Turnstile est proposé à évaluer après revue de son DPA, de sa localisation et des transferts ; la recette garde le CAPTCHA désactivé par variable d'environnement. En production, le jeton doit être vérifié côté serveur et refusé s'il est absent, invalide, expiré ou lié au mauvais hôte. La présence du CAPTCHA ajoute un traitement de données techniques à déclarer dans la politique de confidentialité.

SMTP OVH n'est pas encore validé : avant intégration, il faut confirmer la connectivité TLS depuis Vercel, l'hôte et les ports officiels, l'offre OVH, les quotas, l'expéditeur existant, la réception par `contact@nocode-testing.com` et `test_recette@nocode-testing.com`, ainsi que l'état SPF/DKIM/DMARC. Aucun identifiant SMTP ne doit être communiqué dans le chat ou inscrit dans le dépôt. L'absence de changement DNS est compatible avec l'usage SMTP, mais peut dégrader la délivrabilité si les enregistrements existants sont insuffisants.

**Architecture, contenu et Vercel — Soso ArchiOps.** Eleventy reste cohérent pour le MVP : il transforme des Markdown versionnés en HTML entièrement maîtrisé par les gabarits, CSS et JavaScript, sans imposer de base de données. La base est à introduire seulement lorsqu'un besoin de multi-édition, droits ou backoffice est confirmé. La publication directe doit être comprise comme une promotion éditoriale accélérée, mais toujours tracée : PR `content/*`, validation Markdown/build, recette stable, approbation humaine et promotion d'un commit identifié. Les changements applicatifs suivent le même circuit avec une CI complète.

Vercel couvre le besoin sous réserve du plan retenu : la branche `recette` peut porter `recette.nocode-testing.com` en Preview ; ce sous-domaine nécessite un CNAME web OVH mais ne modifie pas les enregistrements e-mail. Les previews doivent être protégées. La protection par mot de passe est annoncée sur Vercel Pro ; l'authentification Vercel est l'alternative lorsque chaque testeur dispose d'un compte autorisé. La production doit être stagee puis promue manuellement par le commanditaire. Références officielles : [domaines par branche](https://vercel.com/docs/domains/working-with-domains/assign-domain-to-a-git-branch), [Deployment Protection](https://vercel.com/docs/deployment-protection), [promotion de déploiement](https://vercel.com/docs/deployments/promoting-a-deployment).

**Produit et tickets — Scarce PO.** Project `#2` est recommandé comme Kanban des travaux (US, dette, tâches qualité), tandis que Project `#1` reste le registre des anomalies. Les deux Projects sont reliés par les références Markdown et les liens d'issues, sans duplication des statuts. Scarce peut créer des tickets uniquement lorsqu'une intégration GitHub autorisée existe ; dans l'état actuel, il peut produire un ticket prêt à créer. Les agents ne renseignent jamais la priorité validée, ne ferment pas une anomalie critique et ne valident pas une recette à la place d'un humain.

**Questions résiduelles avant les prochains lots :**
1. Validez-vous la maquette `accueil-atelier-calibre.svg`, l'accent cuivre désaturé, le niveau d'humour et le futur registre d'assets ?
- Non, mes retours ont été fait plus haut et peuvent être transmis à Armindia
2. Qui valide les priorités d'anomalies, les exceptions et les promotions production ? Confirmez-vous Project `#1` pour les anomalies et Project `#2` pour le Kanban ?
- Je confirme les projets pour anomalies et kanban
- Je reste seul maître sur les validations de priorité / exception et de promotion en production
3. Autorisez-vous un lot documentaire créant `Processus/` et `qualite-logicielle/` ?
- Oui
4. Quel plan Vercel acceptez-vous : Pro avec mot de passe, ou comptes Vercel individuels pour les testeurs ? Qui administre Vercel, GitHub, DNS OVH et les secrets ?
- Je reste administrateur sur ces outils. Merci de m'indiquer quand tu auras besoin des accès Vercel.
- J'aurais besoin cependant de tes documentations pas à pas pour pouvoir réaliser les actions.
5. Quelle durée de conservation est validée juridiquement pour les demandes de contact, et qui réalise leur suppression ?
- Le minimum légal, je me charge de ces suppressions
6. Pouvez-vous confirmer les informations non secrètes de l'offre SMTP OVH (hôte, ports TLS, quotas, expéditeur, réception et SPF/DKIM/DMARC) et accepter un essai contrôlé en recette ?
serveur SMTP : smtp.mail.ovh.net
port : 587
sécurité : STARTTLS
authentification : oui
- Merci de m'indiquer quels informations supplémentaires tu aurais besoin.
7. Quel fournisseur CAPTCHA acceptez-vous après revue de son DPA et de sa localisation ?
- Si cloudflare Turnstile convient, nous pouvons tester?

### 7.8 Décisions et lots autorisés — 2026-09-20

**Gouvernance validée :** Project GitHub `#1` reste le registre des anomalies et Project `#2` le Kanban. Le commanditaire est l'unique personne habilitée à valider les priorités, exceptions et promotions de production. Il reste administrateur de Vercel, GitHub, OVH/DNS et secrets ; les agents fournissent les procédures pas à pas et ne reçoivent aucun accès ni secret.

**Lot documentaire autorisé :** créer les dossiers `Processus/` et `qualite-logicielle/`, avec leur structure Markdown de gouvernance et de traçabilité. Il ne comprend ni création d'issue GitHub, ni configuration distante, ni US d'interface non validée.

**Lot UX/UI autorisé :** créer de nouvelles maquettes accueil/header, plus graphiques et expérimentales, avec logo dans le header. Les références doivent rester originales : aucune reproduction d'élément, personnage, symbole, interface ou autre contenu protégé de Portal/Valve.

**SMTP OVH confirmé, sous réserve d'essai de recette :** serveur `smtp.mail.ovh.net`, port `587`, sécurité `STARTTLS`, authentification requise. Les identifiants restent secrets et seront saisis uniquement par le commanditaire dans Vercel lorsque le lot formulaire sera validé.

**Rétention :** le commanditaire applique la durée minimale légalement applicable et réalise lui-même les suppressions. La durée chiffrée et sa justification juridique doivent être documentées avant activation du formulaire.

**CAPTCHA :** évaluation de Cloudflare Turnstile autorisée. Son éventuelle intégration reste conditionnée à l'avis de Mina sur DPA, localisation, transferts, accessibilité et stratégie de test.

### 7.9 Avis Turnstile — Mina Cybersécurité (2026-09-20)

**Avis : Conforme sous réserves.** Cloudflare Turnstile convient au besoin d'un contrôle peu intrusif s'il est limité à la production et complète, sans les remplacer, la validation serveur, le honeypot et la limitation de débit.

- Retenir le mode `Managed` avec apparition `interaction-only`, une action `contact` et des restrictions de domaines aux hôtes de production.
- La fonction serveur doit appeler `Siteverify` pour chaque soumission et refuser tout jeton absent, invalide, expiré, réutilisé ou lié au mauvais hôte/action. Aucun e-mail SMTP ne peut partir sans validation serveur réussie.
- En cas d'indisponibilité du widget ou de `Siteverify`, le comportement est `fail closed` : aucun envoi, un message générique et une nouvelle tentative proposée. La recette reste sans widget afin de conserver les E2E automatisés ; les clés de test officielles servent seulement aux environnements non productifs dédiés.
- Turnstile traite notamment l'IP, l'empreinte TLS et le `User-Agent`; son DPA prévoit des transferts potentiels hors EEE. Le fournisseur, la finalité anti-abus et les transferts éventuels doivent être documentés dans la politique de confidentialité et validés juridiquement avant activation.
- Les logs conservent seulement des codes techniques agrégés et excluent jetons Turnstile, contenu du formulaire, adresses e-mail complètes et identifiants SMTP.

**Décision restant à prendre :** le commanditaire doit valider Cloudflare comme sous-traitant après revue juridique du DPA et de l'information visiteurs. Références officielles : [validation serveur](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/), [clés de test](https://developers.cloudflare.com/turnstile/troubleshooting/testing/), [accessibilité et modes](https://developers.cloudflare.com/turnstile/concepts/appearance-modes/), [politique Turnstile](https://www.cloudflare.com/turnstile-privacy-policy/) et [DPA Cloudflare](https://www.cloudflare.com/cloudflare-customer-dpa/).

**Informations SMTP OVH restantes, non secrètes :** offre exacte, format attendu de l'identifiant SMTP, expéditeur autorisé, quotas/taille maximale, exigences d'enveloppe et état SPF/DKIM/DMARC. Le serveur, le port et STARTTLS sont confirmés ; les secrets ne doivent jamais être consignés dans le projet.
- Pour cette partie nous referons des tests après déploiement sur Vercel pour être dans les meilleurs conditions. Il faut tout mettre en place avec l'hypothèse que cela fonctionne correctement.

**Décision du commanditaire :** l'intégration du formulaire peut être conçue avec l'hypothèse que SMTP OVH fonctionne depuis Vercel. La connectivité réelle, les quotas et la délivrabilité seront qualifiés par un essai contrôlé en recette après le déploiement ; un échec déclenchera l'étude d'une alternative API HTTPS.

### 7.10 Décisions complémentaires du commanditaire — 2026-09-20

- **Turnstile :** Cloudflare Turnstile est validé sous les réserves documentées en section 7.9. Son intégration future utilisera le mode `Managed` avec vérification serveur obligatoire, uniquement en production. L'information RGPD sera revue avant activation.
- **UI :** le sponsor préfère la base « Atelier calibre » pour sa palette. Il demande une refonte plus ludique et expressive : police moderne et technique, fond légèrement coloré, suppression du tableau de bord, logo `assets/brand/Logo_NCT_vectoriel.svg` dans le header, bouton Contact conservé et navigation dans un cadre distinct à droite. Une future proposition doit explorer une ambiance de laboratoire/puzzle originale, sans reproduire de contenu protégé de Portal/Valve.

### 7.11 Validations du commanditaire — 2026-09-20

- **RGPD :** les demandes de contact sont conservées au maximum trois ans à compter du dernier contact actif, ou supprimées plus tôt selon la demande de la personne ou lorsque la finalité est atteinte. Le commanditaire réalise les suppressions. Une politique de confidentialité destinée au site est à rédiger, puis à relire humainement avant publication.
- **Vercel :** le commanditaire prévoit de souscrire une offre Pro afin d'utiliser la protection par mot de passe de la recette et des previews. Une procédure pas à pas sera fournie avant toute configuration distante.
- **UI :** le lot « image de direction puis maquette Atelier calibre » est explicitement autorisé. L'image sert de direction artistique ; la maquette structurée reste la source pour l'implémentation accessible et responsive.

### 7.12 Livrables du lot image/maquette et RGPD — 2026-09-20

**Direction UI « Labo puzzle ».** Armindia UI propose une évolution expressive d'Atelier calibre : fond brume teinté, panneaux asymétriques, géométrie de parcours et navigation dans un module indépendant à droite. La maquette utilise explicitement `assets/brand/Logo_NCT_vectoriel.svg` dans le header, retire toute référence à un tableau de bord et conserve le bouton Contact. Les fichiers sont :

- `assets/mockups/direction-labo-puzzle.svg` : planche de direction artistique vectorielle originale ; elle remplit le rôle de référence graphique, sans reprendre de contenu protégé tiers.
- `assets/mockups/accueil-labo-puzzle.svg` : maquette structurée desktop et mobile, destinée au futur handoff frontend.

La planche de direction est un SVG plutôt qu'un bitmap généré. Ce choix garde les formes, contrastes et textes inspectables ; une image bitmap peut être utile comme moodboard, mais ne doit pas être convertie automatiquement en interface, car elle ne garantit ni responsive, ni états, ni accessibilité. Les familles proposées sont `Space Grotesk` pour titres/reperes et `IBM Plex Sans` pour lecture/contrôles ; leur chargement ne sera décidé qu'au lot frontend.

**Projet de politique de confidentialité.** Mina a rédigé [le projet](Processus/11-projet-politique-confidentialite.md) destiné au site. Il couvre le responsable du traitement, les données du formulaire, finalités, bases légales à confirmer, sous-traitants, transferts, conservation, droits, CNIL, sécurité, cookies/analytics et Turnstile. Il rappelle la conservation maximale de trois ans après le dernier contact actif et la suppression anticipée si nécessaire. La revue juridique humaine avant publication reste obligatoire, notamment pour les bases légales, sous-traitants effectifs, transferts et durées des journaux/sauvegardes.

**Décisions attendues :** valider ou ajuster « Labo puzzle », le niveau d'humour et les familles typographiques. La politique de confidentialité doit être relue par une personne compétente avant sa publication.

### 7.13 Retours UI complémentaires du commanditaire — 2026-09-20

- Le sponsor préfère finalement conserver la base chromatique d'« Atelier calibre », en particulier pour le panneau de navigation à droite.
- L'accent jaune citron est rejeté et doit être remplacé par une couleur plus cohérente avec cette palette.
- La proposition typographique est appréciée.
- Le futur langage de boutons doit être plus personnel et moins conventionnel, tout en restant clairement identifiable comme un contrôle et accessible.
- La prochaine maquette doit hybrider le panneau actif à droite avec les cartes de contenu à gauche, en conservant une composition légèrement déstructurée.
- Le logo est référencé dans la maquette actuelle par un lien SVG externe, mais il n'apparaît pas dans certains aperçus. La prochaine maquette doit incorporer le logo de manière autoportante afin qu'il soit visible dans tous les outils d'aperçu ; le fichier source de référence reste `assets/brand/Logo_NCT_vectoriel.svg`.

### 7.14 Raffinement de la direction hybride — 2026-09-20

- Conserver le fond coloré, le cadre général et le header de la maquette hybride.
- Adopter des boutons en flat design : forme rectangulaire sans contour, pictogramme représentatif et libellé explicite. Le pictogramme ne remplace pas le texte ni les états accessibles.
- Conserver le panneau de menu à droite, sa couleur et son style ; le rapprocher du cadre général.
- Remplacer les cartes de gauche actuelles par les panneaux graphiques de `assets/mockups/direction-labo-puzzle.svg`, en préservant l'aspect légèrement déstructuré et l'ordre de lecture clair.
- Préparer un catalogue séparé de petites formulations humoristiques adaptées à la qualité logicielle et au no-code, afin que le commanditaire les sélectionne avant implémentation.

### 7.15 Corrections visuelles et variante sombre autorisées — 2026-09-20

- Le cuivre est rejeté. Les accents reprennent le bleu gris `#CED7E2` des boutons « Voir le labo » et les couleurs de la palette Atelier calibre ; aucun jaune citron ni cuivre n'est retenu.
- Le bouton Contact doit garantir la lisibilité du pictogramme de messagerie, par contraste et par une zone d'icone suffisamment distincte. Le bouton « Nous écrire » du panneau droit doit être centré horizontalement.
- Les CTA sont renommés : `Découvrez l'univers du Testeur du Granier` et `Découvrez nos expérimentations`.
- Les panneaux de gauche doivent reprendre fidèlement la composition graphique de `assets/mockups/direction-labo-puzzle.svg` : panneau sombre vertical à gauche, panneau bleu horizontal en haut à droite, panneau blanc en bas à gauche et panneau coloré en bas à droite, avec leurs proportions et leur décalage. Les précédentes cartes « Question / Essai / Retour terrain » ne sont pas la direction attendue.
- Une variante sombre est explicitement demandée. Elle doit être activable depuis le header par un contrôle de thème accessible, et montrer les états clair, sombre et le comportement mobile sans apposer de données factices.

### 7.16 Validation de la première direction MVP — 2026-09-20

Le commanditaire confirme que la première version proposée convient pour lancer le MVP. La référence de handoff UI est `assets/mockups/accueil-puzzle-ateliers-themes.svg`, avec ses thèmes clair et sombre, ses quatre panneaux, son header et sa navigation rattachée. Toute évolution ultérieure devra partir de cette référence validée.

**Prochain incrément proposé :** cadrage produit de l'accueil et du header, puis création des exigences et tickets associés. Le développement ne débute qu'après validation de ce cadrage et de la stack.

### 7.17 Six éléments de cadrage à relire avant les tickets accueil/header

Ces six points regroupent les décisions demandées à Scarce avant la création de `REQ-001` et des premières US. Ils ne sont pas encore transformés en exigences détaillées.

1. **Hero et positionnement** : afficher « Qualité logicielle » avec le ton léger validé, sans contenu humoristique dans les informations critiques.
- Niveau "titre", dans le header à droite du logo, je serais plus pour mettre une phrase amusante en titre, qui changerait à chaque chargement de la page.
- Avant de mettre la feature en place, la phrase à mettre c'est "La Qualité logicielle est l'affaire de tou•te•s"
2. **Panneaux graphiques** : reprendre les quatre panneaux de `assets/mockups/direction-labo-puzzle.svg` dans la composition validée `assets/mockups/accueil-puzzle-ateliers-themes.svg`.
- Oui pour la reprise :
3. **CTA et destinations** : utiliser `Découvrez l'univers du Testeur du Granier` et `Découvrez nos expérimentations`, puis confirmer les pages ou ancres cibles disponibles au premier incrément.
- On enlève le découvrez pour un "L'univers du testeur du granier" et "Nos experimentations"
4. **Header et navigation** : logo, bouton Contact, navigation rattachée au header à droite, menu responsive et pictogrammes avec libellés explicites.
- OK
5. **Thème clair/sombre** : contrôle accessible dans le header, préférence système initiale, choix utilisateur persistant, contrastes et états clavier ; confirmer si ce comportement appartient au premier incrément.
- Yes, juste le logo sombre / clair sans le texte
- A terme, je prévoir aussi de faire un module permettant de changer le thème complet du site pour permettre à chacun d'avoir le site de son choix (brandé avec les sponsors, outils ou autre) > Après MVP (mais à garder en tête)
6. **Périmètre de livraison** : confirmer l'inclusion du footer dans le lot accueil/header ou son traitement séparé ; les pages secondaires, le formulaire et le contenu éditorial détaillé restent à découper.
- Inclure le footer, avec toutes les informations classique comme les informations légales & RGPD

**Stack validée pour le MVP :** Eleventy, HTML/CSS/JavaScript natif et Node.js 22 LTS. Cette décision permet de créer les exigences et tickets sur une base technique stabilisée.

### 7.18 Décisions complémentaires pour le lot produit — 2026-09-21

- Le texte initial du hero/header est : `La Qualité logicielle est l'affaire de tou•te•s`.
- À terme, le titre du header pourra varier à chaque chargement ; cette variation n'est pas une exigence du premier incrément et devra préserver la lisibilité, la stabilité des tests et l'accessibilité.
- Les CTA deviennent `L'univers du Testeur du Granier` et `Nos expérimentations`.
- Le thème clair/sombre appartient au MVP. Le contrôle de thème affiche uniquement l'icône adaptée (soleil/lune), sans texte permanent ; son nom accessible et son état restent obligatoires pour les technologies d'assistance.
- Le logo devra utiliser la variante adaptée au thème : logo clair sur fond sombre et logo sombre/couleur sur fond clair, sans afficher le mot-symbole textuel en complément dans le contrôle de thème.
- La personnalisation ultérieure de thèmes complets, brandés par sponsors, outils ou partenaires, est une évolution post-MVP à conserver comme piste d'architecture.
- Le footer est inclus dans le premier lot et doit contenir les informations légales, RGPD et les liens attendus ; son contenu précis sera contrôlé avec la politique de confidentialité et les mentions légales.

### 7.19 Revues Mina et Mikaya des US — 2026-09-21

Le découpage en `REQ-001` à `REQ-004` et `US-001` à `US-004` est adapté à un cycle court, mais les US restent `brouillon` / `a_revoir` et ne peuvent pas passer `pret` avant corrections documentaires.

**Mina Cybersécurité :** avis global `À corriger avant développement`. Les réserves portent sur les destinations non définies des CTA et du header, le contrôle du stockage local du thème, la protection de la politique RGPD non relue et l'absence de contrôle explicite des scripts, requêtes et traceurs. Aucune vulnérabilité de code ni CVE n'est confirmée, car aucun code n'existe encore.

**Mikaya test :** avis `À revoir` pour les quatre US. Les critères doivent préciser les routes, les quatre panneaux et leur ordre, les viewports `320x568`, `375x667`, `768x1024`, `1280x800`, le comportement du menu mobile (Échap, retour de focus, absence de piège clavier), les noms et états accessibles, ainsi que la clé et les valeurs autorisées du stockage local.

**Réserves à trancher :**
1. Routes exactes des deux CTA et des cinq rubriques du header.
2. Choix de la clé et des valeurs `localStorage` du thème, avec repli sur la préférence système.
3. Identité de la personne compétente qui relira juridiquement la politique et les mentions légales avant publication.
4. Confirmation du niveau cible : principes WCAG 2.2 AA applicables ou objectif plus limité.
5. Confirmation que le MVP ne charge aucun analytics, publicité, suivi ou script tiers non justifié.
6. Harmonisation définitive des adresses : `contact@nocode-testing.com` pour le contact et `rgpd@nocode-testing.com` pour les droits RGPD.

**Décision analytics clarifiée :** la case historique « Analytics respectueux de la vie privée » est remplacée par la décision ultérieure « aucun analytics ni traceur non essentiel au MVP ». Toute évolution analytics fera l'objet d'un lot et d'une validation séparés.

### 7.20 Arbitrages du commanditaire sur les US — 2026-09-21

- Les routes proposées sont validées : `/blog/`, `/labo-test-ia/`, `/ressources/`, `/a-propos/`, `/contact/`, `/mentions-legales/` et `/confidentialite/`.
- Le thème utilise la clé `nct-theme`, avec les valeurs `light` et `dark`. Priorité : choix enregistré, puis préférence système, puis thème clair par défaut.
- La personne qui réalisera la revue juridique finale sera désignée après le MVP ; le lot produit actuel peut continuer, mais aucune publication légale ne doit intervenir avant cette revue.
- Les principes WCAG 2.2 AA applicables sont confirmés comme objectif du projet.
- Le MVP ne charge aucun analytics, publicité, suivi ni script tiers non justifié.
- Les adresses sont confirmées : `contact@nocode-testing.com` pour le formulaire et `rgpd@nocode-testing.com` pour les droits RGPD.
- Pour le thème sombre, utiliser `assets/brand/Logo_NCT_vectoriel_blanc.png`. Le logo clair/couleur reste utilisé sur fond clair ; le contrôle de thème reste une icône seule visuellement.

### 7.21 Avis de faisabilité avant développement — 2026-09-21

- **Camity Front :** le lot est faisable avec Eleventy, HTML/CSS/JavaScript natif et Node.js 22. Le layout partagé fournira header, contenu et footer ; le menu mobile et le thème restent en JavaScript natif. Les tests responsive viseront `320x568`, `375x667`, `768x1024` et `1280x800`.
- **Soso ArchiOps :** aucune base de données, fonction serveur, SMTP, Turnstile ou secret n'est nécessaire pour ce lot. Le formulaire et son infrastructure seront traités dans un incrément séparé. Le build Eleventy, le lockfile, la CI et les previews Vercel restent à initialiser dans le chantier technique.
- **Rindel Dev :** aucun contrat API n'est nécessaire pour l'accueil, le header, le thème et le footer statiques. Le futur formulaire aura un contrat `POST` same-origin distinct, avec validation serveur, honeypot, limitation durable, Turnstile en production et SMTP OVH en recette.

**Écart à corriger avant implémentation :** la planche `assets/mockups/accueil-puzzle-ateliers-themes.svg` conserve visuellement d'anciens libellés CTA (`Decouvrez...`), alors que les US validées imposent `L'univers du Testeur du Granier` et `Nos experimentations`. L'implémentation doit suivre les US ; la maquette doit être réalignée avant le handoff final.

**Questions restantes :** URL LinkedIn définitive du footer ; confirmation que `/contact/` est une page statique informative dans ce lot, sans envoi, le formulaire fonctionnel étant reporté à un lot séparé.

### 7.22 Extension validée du lot contact et du footer — 2026-09-21

- Footer LinkedIn personnel : `https://www.linkedin.com/in/michael-granier/`.
- Footer LinkedIn entreprise : `https://www.linkedin.com/company/nocode-testing`.
- `/contact/` devient une page formulaire fonctionnelle du MVP, et n'est plus un simple placeholder.
- Le développement local doit pouvoir envoyer ou simuler l'envoi sans dépendre immédiatement du SMTP OVH distant. Le mode local utilisera des variables d'environnement Windows, jamais commitées, pour sélectionner un transport de développement et ses paramètres.
- Le mode local retenu est `CONTACT_TRANSPORT=fake` : aucun appel réseau, aucun secret SMTP et aucune écriture du payload personnel sur disque. Les variables Windows ne contiennent que la configuration de développement non sensible.
- Le SMTP local est autorisé comme mode de test explicite avec `CONTACT_TRANSPORT=smtp`. Les variables SMTP sont fournies par le commanditaire dans la session Windows et ne sont jamais commitées ; `fake` reste le mode par défaut recommandé.
- Le contrat fonctionnel du formulaire reste : `nom`, `e-mail`, `societe`, `sujet`, `message`, validation serveur, honeypot et limitation de débit. La cible réelle de production reste `contact@nocode-testing.com`.
- Le SMTP OVH (`smtp.mail.ovh.net:587`, STARTTLS, authentification) sera branché et testé en recette après déploiement, avec les secrets saisis par le commanditaire dans Vercel. Le mode local ne doit jamais nécessiter ni stocker ces secrets.
- Turnstile reste désactivé en local et en recette automatisée ; il sera activé et vérifié uniquement en production selon les décisions Mina déjà documentées.
