# 09 - Formulaire contact et messagerie

## Statut et prerequis

Cette procedure ne rend pas le formulaire actif. Son implementation exige un lot valide, une duree de conservation chiffree validee juridiquement et la qualification securite/test de Mina, Rindel et Mikaya.

Le formulaire collecte uniquement `nom`, `e-mail`, `societe`, `sujet` et `message`. Il envoie a `contact@nocode-testing.com`. Recette : donnees fictives et `test_recette@nocode-testing.com` uniquement.

## Controles attendus

1. Fonction serveur same-origin : validation stricte, longueurs bornees, encodage et aucun contenu utilisateur interprete comme HTML.
2. Honeypot, limitation de debit durable cote serveur et reponse neutre pour les abus.
3. CAPTCHA desactive en recette. Cloudflare Turnstile est seulement a evaluer ; aucune integration sans avis favorable de Mina sur DPA, localisation, transferts, accessibilite et testabilite.
4. Logs minimises : aucun message, e-mail complet ou secret. Les erreurs retournent un message generique a l'utilisateur.

## SMTP OVH : actions du sponsor lors du lot formulaire

Prerequis : confirmer l'offre, quotas, expéditeur, reception, connectivite TLS depuis Vercel et etat SPF/DKIM/DMARC. Aucun changement DNS n'est presume.

1. Consulter la documentation officielle OVHcloud et confirmer les parametres non secrets : `smtp.mail.ovh.net`, port `587`, `STARTTLS`, authentification requise.
2. Dans Vercel, creer des variables de secret distinctes recette et production. Le sponsor saisit lui-meme identifiant et mot de passe SMTP ; ne les colle ni dans Git ni dans le chat.
3. Configurer l'expediteur controle et le destinataire approprie a l'environnement.
4. Tester en recette avec un message fictif vers `test_recette@nocode-testing.com`, puis verifier reception, TLS, logs minimises et gestion d'erreur.
5. Le sponsor valide le resultat avant toute promotion. La production reste desactivee tant que cette validation manque.

## Rollback

En cas d'echec, de spam ou de doute sur la securite, le sponsor retire ou desactive les variables SMTP/fonction de l'environnement concerne, conserve les preuves non sensibles et applique [08](08-incident-retour-arriere-et-post-mortem.md).