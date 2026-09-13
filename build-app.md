# Build App — Journal de pilotage Dominion

Ce fichier est la base de communication entre le commanditaire et Dominion (orchestrateur) pour faire évoluer le projet `nocode-testing.com`. Il consigne : la revue des agents, les LLM recommandés par agent, les questions ouvertes de cadrage et les réponses obtenues.

Dernière mise à jour : 2026-09-13.

---

## 1. Revue des agents existants

### Scarce PO (exigences, US, Gherkin)
- Bien cadré : référentiel d'exigences + US Markdown + Gherkin, collaboration avec Mina Cybersécurité, Soso ArchiOps, Camity Front, Mikaya test et Rindel Dev prévue via `agents:`.
- **Recommandation** : rien de bloquant. À surveiller : le dossier `user-stories/` n'existe pas encore — ce sera la première tâche concrète une fois le besoin cadré (voir section Questions).

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

## 3. Questions de cadrage — projet nocode-testing.com

Le projet repart de zéro (README + `package.json` vides de tout choix technique). Avant de lancer le premier chantier avec les agents, j'ai besoin de vos réponses sur les points suivants :

1. **Nature du site** : vitrine simple, blog, plateforme avec contenu dynamique, ou autre ? Combien de pages/sections envisagées au démarrage ?
2. **Stack technique cible** : confirmez-vous du HTML/CSS/JS vanilla pur (sans framework), ou un générateur de site statique léger (ex: Eleventy) est-il envisageable pour la maintenabilité ?
3. **Hébergement/déploiement** : le README mentionne GitHub Pages non reconfiguré — c'est bien la cible de publication définitive ?
4. **Contenu** : le contenu (textes, offres nocode-testing) existe-t-il déjà quelque part (ancien Docusaurus, doc externe), ou faut-il le produire avec Scarce PO ?
5. **Identité visuelle** : existe-t-il déjà une charte graphique (logo, couleurs, typographie) à respecter, ou Armindia UI doit-elle proposer des directions from scratch ?
6. **Tests** : quel niveau de couverture visez-vous au démarrage (fumée/E2E basique vs couverture complète) ? Cela dimensionnera le travail de Mikaya test.
7. **Échéance** : y a-t-il une date ou un jalon cible pour une première mise en ligne, afin de prioriser le découpage des US ?

## 4. Réponses du commanditaire
- *(à compléter au fur et à mesure des réponses)*

## 5. Décisions actées
- *(à compléter une fois les réponses obtenues et le premier plan de tâches validé)*

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
