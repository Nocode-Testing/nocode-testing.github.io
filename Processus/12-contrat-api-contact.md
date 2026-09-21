---
id: CONTRAT-API-CONTACT
statut: brouillon
---

# Contrat API — Formulaire Contact

Version : 2026-09-21
Propriétaire : Rindel Dev
Emplacement : Processus/12-contrat-api-contact.md

Résumé
- Endpoint same-origin exposé par le site : POST `/api/contact`
- Transport des messages : local en développement Windows (sans SMTP obligatoire), SMTP OVH en recette/production via secrets Vercel
- Antispam : honeypot + validation serveur + rate limit durable; Turnstile uniquement en production avec vérification serveur (siteverify)
- Aucun stockage métier durable des messages (pas de DB). Logs minimisés.

1. Endpoint

- Méthode : `POST`
- URL : `/api/contact` (même origine que le site)
- Content-Type : `application/json`

2. Payload attendu (JSON)

- `nom`: string, 1..100 caractères, trim, HTML interdit
- `email`: string, RFC 5322 compatible validation raisonnable, 5..254 caractères, lowercase, trim
- `societe`: string | null, 0..100 caractères, trim, HTML interdit
- `sujet`: string, 1..150 caractères, trim, HTML interdit
- `message`: string, 1..4000 caractères, trim, HTML interdit
- `honeypot`: string, MUST be empty; field invisible côté client pour bots

Exemple minimal de payload :

```json
{
  "nom": "Jean Dupont",
  "email": "jean@example.com",
  "societe": "Acme",
  "sujet": "Question sur vos prestations",
  "message": "Bonjour, je souhaite...",
  "honeypot": ""
}
```

3. Validation serveur

- Tous les champs texte : `trim()` puis validation de longueur et du type.
- Refuser toute entrée contenant balises HTML ou entités interprétables : neutraliser (`escape`) si affichage requis ailleurs, mais refuser l'envoi si HTML détecté dans `sujet`/`message`.
- `email` : vérification syntaxique (regex raisonnable) et ajout d'un test simple pour domaines invalides (ex : adresse locale sans domaine).
- `honeypot` : doit être vide — sinon répondre comme si l'appel avait réussi (réponse neutre) mais sans transport d'email.
- Vérifier présence et source Origin/Referer (voir section CSRF/CORS).

4. Responses JSON et codes HTTP

- 200 OK — succès

  ```json
  { "status": "ok", "message": "Votre message a été transmis." }
  ```

- 400 Bad Request — validation échouée

  ```json
  { "status": "error", "code": "validation_error", "errors": { "email": "Adresse invalide" } }
  ```

- 429 Too Many Requests — quota/rate limit dépassé

  ```json
  { "status": "error", "code": "rate_limited", "retry_after_seconds": 3600 }
  ```

- 500 Internal Server Error — erreur interne

  ```json
  { "status": "error", "code": "server_error", "message": "Une erreur est survenue, veuillez réessayer plus tard." }
  ```

Remarques :
- Les messages d'erreur présents dans les réponses exposent un libellé générique ; ne pas renvoyer de PII ni de stack traces.

5. Transport des messages

- Environnement local (Windows) — comportement par défaut : `CONTACT_TRANSPORT=fake`.
  - Le transport fake ne fait aucun appel réseau, ne charge aucun secret SMTP et n'ecrit jamais le payload personnel sur disque.
  - Un test SMTP local est autorise uniquement si `CONTACT_TRANSPORT=smtp` est choisi explicitement et si les variables SMTP sont definies dans la session Windows. Les secrets ne sont jamais commites ni affiches.
  - Le transport fake retourne un resultat simule stable ou l'injecte dans un mock en memoire pour les tests. Les logs locaux n'incluent aucune donnee du formulaire.

- Recette et Production — `CONTACT_TRANSPORT=smtp` et configuration SMTP OVH via secrets Vercel :
  - Hôte recommandé : `smtp.mail.ovh.net`, port `587`, STARTTLS, authentification requise.
  - Variables secrets attendues (voir section Variables d'environnement).
  - Expéditeur : `SMTP_FROM` contrôlé par l'environnement ; destinataire : `CONTACT_RECEIVER` (ex. `test_recette@nocode-testing.com` en recette, `contact@nocode-testing.com` en prod).

- En cas d'échec d'envoi SMTP : gérer les erreurs selon politique d'exploitation — pour le MVP refuser l'appel côté serveur en retournant `500` et logs minimisés ; possibilité d'ajouter file d'attente/relai plus tard.

6. Turnstile (CAPTCHA)

- Activation : production seulement (ne pas activer en recette ni en local).
- Flow : le client inclut le token Turnstile côté navigateur ; le serveur appelle l'endpoint Siteverify (Cloudflare) avec la `TURNSTILE_SECRET` et vérifie le succès.
- En cas d'indisponibilité du service Turnstile : refuser l'envoi (sécurité prioritaire) ou, si décision validée, appliquer un fallback progressif documenté.

7. CSRF / CORS / Sécurité applicative

- CORS : endpoint conçu `same-origin` — lister les origines autorisées strictement (par défaut `Origin` doit être égal à la base du site). Si nécessaire, autoriser une liste blanche via `CONTACT_ALLOWED_ORIGINS`.
- CSRF : vérifier `Origin` et `Referer` ; refuser si manquant ou non matching. Pour protections supplémentaires, utiliser `SameSite=strict` cookies et double-submit cookie si un cookie d'authentification/existence est présent.
- Headers attendus : vérifier `Content-Type: application/json`, `Origin` et `Referer` ; accepter `X-Idempotency-Key` facultatif.
- Injection : ne jamais interpréter le contenu des champs comme HTML ; envoyer en texte brut et échapper à l'affichage.

8. Rate limit durable

- Objectif : limiter abus et assurer résilience.
- Recommandation initiale (ajustable après observation) :
  - 30 requêtes par adresse IP / 1 heure
  - 5 requêtes par adresse IP / 1 minute
  - 10 messages par adresse e-mail / 24 heures
- Durabilité : utiliser un store court-terme partagé (Redis, Cloud provider Redis ou équivalent) pour pouvoir répartir la limite entre instances. En l'absence de Redis, un compteur en mémoire est acceptable en développement mais non durable.
- En cas de rate limit dépassé : retourner 429 avec `Retry-After` ou `retry_after_seconds` dans le JSON.

9. Idempotence / Anti-rejeu

- Option A (léger) : permettre l'en-tête `X-Idempotency-Key` fourni par le client ; le serveur conserve la clé dans un cache durable (TTL court, ex. 24h) et refuse la ré-exécution si la clé existe.
- Option B (alternatif) : calculer un hachage immuable du payload (par ex. SHA256 de `nom|email|sujet|message` normalisé) et garder les hachages récents en cache pour déduplication pendant une fenêtre (ex. 24h).
- Recommandation MVP : implémenter Option A si un store durable existe (Redis) ; en local, l'idempotence peut être désactivée ou simulée.

10. Observabilité et logging

- Logs minimisés : enregistrer uniquement événements opérationnels (success/failure code, transport type, erreur codée), sans stocker de PII (email complet, message intégral) dans les logs.
- Exemple de log autorisé : `contact.sent env=production transport=smtp status=sent time_ms=123`.
- En cas d'erreur : loguer `contact.error env=production code=smtp_auth_failed` et un identifiant de corrélation non sensible (`correlation_id`) pour debugging, sans inclure le payload.

11. Aucune persistance métier

- Par conception : ne pas écrire le contenu des messages dans une base de données métier ni dans une outbox locale. Le mode fake utilise un mock en mémoire ou un résultat simulé ; seuls des événements anonymisés peuvent être journalisés.

12. Variables d'environnement (noms uniquement)

- `NODE_ENV`
- `APP_ENV` (`local`|`recette`|`production`)
- `VERCEL_ENV`
- `CONTACT_TRANSPORT` (values: `fake`|`smtp`)
- `CONTACT_RECEIVER` (adresse destinataire par défaut)
- `SMTP_HOST` (ex: smtp.mail.ovh.net)
- `SMTP_PORT` (ex: 587)
- `SMTP_SECURITY` (expected value: `STARTTLS`)
- `SMTP_USER` (secret)
- `SMTP_PASS` (secret)
- `SMTP_FROM` (expéditeur affiché)
- `TURNSTILE_SECRET` (secret)
- `TURNSTILE_SITEKEY` (public key, non secret)
- `TURNSTILE_ENABLED` (`false` local/recette, `true` production)
- `CONTACT_ALLOWED_ORIGINS` (optionnel, liste séparée par des virgules)
- `RATE_LIMIT_WINDOW_SECONDS` (optionnel)
- `RATE_LIMIT_MAX_REQUESTS` (optionnel)

13. Règles CORS / CSRF (récapitulatif)

- CORS : par défaut `same-origin` uniquement ; si cross-origin requis, limiter strictement à `CONTACT_ALLOWED_ORIGINS`.
- CSRF : vérifier `Origin` et `Referer` ; refuser si absents ou mismatch. N'accepter aucune requête mutative sans vérification d'origine.

14. Questions ouvertes (à valider avec le commanditaire / Soso ArchiOps)

- Adresse destinataire en production exacte (ex : `contact@nocode-testing.com`) et en recette (`test_recette@nocode-testing.com`).
- Politique de retry SMTP souhaitée (requeue, alerting, abandon définitif après N tentatives).
- Seuils de rate-limit souhaités en production définitive.
- Décision sur l'usage d'un store durable (Redis) pour rate limit et idempotence en production.
- Politique de conservation des fichiers locaux de debug et procédure de purge.

15. Scénarios d'acceptation (extraits)

- Envoi valide (local) : `CONTACT_TRANSPORT=fake`, POST valide → 200 et resultat simule, sans appel reseau ni fichier personnel.
- Envoi valide (recette) : `CONTACT_TRANSPORT=smtp`, secrets fournis pour recette, message fictif → 200 et mail reçu `test_recette@...`.
- Honeypot rempli → réponse 200 (ne pas révéler le rejet), aucun transport effectué.
- Payload invalide (email manquant) → 400 et indication `validation_error`.
- Rate limit dépassé → 429 et `retry_after_seconds`.

16. Annexes

- Référence SMTP OVH (non sensible) : `smtp.mail.ovh.net`, port `587`, STARTTLS.
- Turnstile : vérifier DPA et réglages d'accessibilité avant activation en production. Siteverify côté serveur obligatoire.

Fin du contrat.
