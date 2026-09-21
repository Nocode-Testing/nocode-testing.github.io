# Pilotage projet — nocode-testing.com

Dernière mise à jour : 2026-09-21.

## Chantiers en cours

| Chantier | Agent | Modèle | Statut | Dépendances | Sortie attendue |
|---|---|---|---|---|---|
| Maquettes accueil + header expressives | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, choix attendu | Direction laboratoire et logo | `Orbite des cas` recommandée, `Champ de preuves` alternatif |
| Stratégie de test | Mikaya test | Claude Sonnet 4.5, repli GPT-5 | Complétée, validation attendue | Gouvernance GitHub et dossier qualité | Anomalies bloquantes/majeures interdisent production |
| Stratégie de test sécurité | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Complétée | SMTP OVH et rétention | Turnstile validé, SMTP à qualifier en recette |
| Stack, architecture et CI/CD | Soso ArchiOps | Claude Sonnet 4.5, repli GPT-5 | Réévaluée, validation attendue | Plan Vercel et approbateurs | Eleventy et promotion humaine recommandés |
| Gouvernance produit / qualité | Scarce PO | Claude Sonnet 4.5, repli GPT-5 | Complétée, US du lot à revoir | Arbitrages sponsor intégrés, sans issue GitHub ni ressource distante | Dossier `qualite-logicielle/` et référentiel mis à jour |
| Processus projet | Soso ArchiOps | Claude Sonnet 4.5, repli GPT-5 | Complété | Gouvernance validée | Dossier `Processus/` et procédures opératoires créés |
| CAPTCHA | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Décision actée | Turnstile et flux formulaire | Turnstile validé sous réserves |
| Image puis maquette Atelier calibre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Brief UI validé | Direction et maquette « Labo puzzle » |
| Raffinement maquette hybride Atelier calibre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Retours UI détaillés | `assets/mockups/accueil-hybride-atelier-calibre.svg` : palette, logo visible et boutons personnalisés |
| Raffinement panneaux et boutons flat | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Retours UI 7.14 | `assets/mockups/accueil-hybride-atelier-calibre-raffine.svg` et catalogue de formulations |
| Corrections panneaux et maquette sombre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Validé | Retours UI 7.15 | Référence UI MVP : `accueil-puzzle-ateliers-themes.svg` |
| Politique de confidentialité | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Validations sponsor intégrées, revue juridique obligatoire avant publication | Configuration réelle des sous-traitants et test SMTP en recette | `Processus/11-projet-politique-confidentialite.md` |
| Référentiel et US du lot accueil + header + thèmes + footer | Scarce PO | Claude Sonnet 4.5, repli GPT-5 | À revoir après faisabilité | CTA de maquette, URL LinkedIn et périmètre contact | `qualite-logicielle/01-exigences/referentiel-exigences.md` et `qualite-logicielle/02-user-stories/US-001` à `US-004` |
| Référentiel et US du formulaire de contact MVP | Scarce PO | Claude Sonnet 4.5, repli GPT-5 | À revoir après revues spécialisées | Fake local, SMTP OVH recette, Turnstile production, validation serveur, limitation durable et politique RGPD | `qualite-logicielle/01-exigences/referentiel-exigences.md` et `qualite-logicielle/02-user-stories/US-005-formulaire-contact.md` |
| Contrat API Contact | Rindel Dev | GPT-5 | Livrable produit (contrat documentaire ajouté) | Pilotage, Mina, Soso, Camity Front | `Processus/12-contrat-api-contact.md` |

## Tableau de bord

| Indicateur | Valeur | Statut |
|---|---:|---|
| User stories définies | 5 | À revoir, revues spécialisées et arbitrages techniques restants |
| Couverture TU | Non mesurable | Aucune stack ni suite de tests |
| Couverture TI/E2E | Non mesurable | Aucune stack ni suite de tests |
| Anomalies ouvertes | 0 connue | Aucun code applicatif |
| Risques sécurité / CVE ouverts | 0 CVE ; 3 réserves techniques | Configuration des sous-traitants, SMTP et limitation durable |
| Risques capacité / exploitation ouverts | 2 | SMTP et limitation durable à qualifier en recette |
| Tâches en attente de validation | 4 validations ciblées | Revue US-005, essai SMTP OVH en recette, Turnstile production et revue juridique |

## Questions ouvertes

1. Réaligner la maquette avec les libellés CTA validés.
2. Qualifier le transport fake local puis le SMTP OVH en recette avec des donnees fictives.
3. Confirmer les parametres de limitation durable, les seuils de charge et le comportement de secours du transport.
4. Relecture juridique humaine de la politique avant toute publication en production.

## Chantier UX/UI formulaire `/contact/`

- **Agent** : Armindia UI
- **Statut** : Maquette produite, recommandation de transmission à Camity Front
- **Périmètre** : aucun code applicatif, aucune modification distante
- **Sorties** : `assets/mockups/contact-formulaire-labo-puzzle.svg` et `assets/mockups/contact-formulaire-labo-puzzle-handoff.md`
- **Couverture** : desktop/mobile, thèmes clair/sombre, idle, validation/erreur, loading, succès, erreur transport et rate-limit ; champs contractuels, RGPD, honeypot annoté et emplacement Turnstile production uniquement
- **Dépendances restantes** : validation humaine de la maquette, contrat API Rindel Dev et vérifications responsive/accessibilité par Camity Front et Mikaya test