# Handoff UI — `/contact/`

## Direction retenue

Le formulaire reprend la direction MVP **Labo puzzle** : fond et cadre de la maquette d'accueil, panneaux asymétriques, contraste ardoise/encre et surfaces éditoriales. Le formulaire reste un panneau de lecture et d'écriture, jamais un dashboard ni une carte imbriquée.

Référence visuelle : [contact-formulaire-labo-puzzle.svg](./contact-formulaire-labo-puzzle.svg). La planche montre desktop/mobile, clair/sombre, et les états fonctionnels nécessaires à la recette.

## Composition

- Desktop : panneau éditorial sombre à gauche avec titre, introduction et formulaire ; rail ardoise à droite pour les repères d'états et contraintes.
- Mobile 320/375 : une seule colonne, labels toujours visibles, champs empilés, bouton pleine largeur utile avec cible minimale de 44 px.
- Header : logo couleur `assets/brand/Logo_NCT_vectoriel.svg` en clair, logo blanc `assets/brand/Logo_NCT_vectoriel_blanc.png` en sombre.
- Champs visibles : `nom`, `e-mail`, `societe`, `sujet`, `message`. Les placeholders ne remplacent jamais les labels.
- Pied de formulaire : lien politique de confidentialité et `rgpd@nocode-testing.com`. Aucun consentement inventé avant validation juridique.

## Etats à implémenter

- **Idle** : formulaire utilisable, aucun retour global.
- **Validation** : erreur factuelle au champ concerné, `aria-describedby`, `aria-invalid`, résumé global ; focus sur le premier champ invalide.
- **Loading** : `Envoyer le message` devient `Envoi en cours...`, bouton désactivé seulement pendant la requête, zone de statut annoncée.
- **Succès** : `Votre message a bien ete envoye.` dans `role="status"`, sans echo HTML ni détail personnel.
- **Transport / serveur** : `Envoi impossible pour le moment. Conservez vos informations et reessayez ulterieurement.` dans `role="alert"` ; valeurs conservées.
- **Rate-limit / anti-abus** : même retour neutre que l'erreur de transport ; aucune distinction du mécanisme, aucun retry automatique.

L'endpoint attendu par le contrat est `POST /api/contact` en JSON. Le front ne construit pas d'URL externe et ne connaît aucun secret SMTP ou Turnstile.

## Tokens

| Usage | Clair | Sombre |
|---|---|---|
| Fond | `#E8EDF1` | `#202B34` |
| Surface | `#F8FAF8` | `#293741` |
| Encre | `#25323D` | `#F5F7F3` |
| Ardoise | `#5D648C` | `#465071` |
| Bleu gris / focus | `#CED7E2` | `#CED7E2` |
| Accent contact | `#A8B8AA` | `#A8B8AA` |
| Erreur factuelle | `#9B3D38` | `#FFB5A8` |

Titres et repères courts : `Space Grotesk`. Texte, labels, aides et contrôles : `IBM Plex Sans`. Prévoir les replis documentés par Camity Front.

## Accessibilité et sécurité d'interface

- HTML natif, ordre de lecture et de tabulation naturel, sans dépendance au JavaScript pour naviguer.
- Cibles interactives d'au moins 44 × 44 px ; anneau de focus continu de 3 px, décalé de 3 px, visible sur tous les fonds.
- Erreurs proches du champ et associées programmatiquement ; le statut global existe dans le DOM avant toute mise à jour.
- Honeypot : annotation technique uniquement ; non visible, non focalisable, nom non évident. Il n'est jamais présenté comme une protection client : validation, contrôle anti-abus et rate limit restent côté serveur.
- Turnstile absent en local et en recette. Sa place est réservée en production uniquement si la configuration serveur l'active et après validation RGPD/DPA ; la vérification reste côté serveur.
- Aucun nom, e-mail réel ou message personnel n'est présent dans la maquette.

## Vérifications attendues

Tester `320x568`, `375x667`, `768x1024` et `1280x800`, zoom navigateur et clavier. Vérifier que les messages, labels, bouton et états ne sont ni tronqués ni superposés en clair et en sombre.
