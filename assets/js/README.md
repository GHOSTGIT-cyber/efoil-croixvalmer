# `assets/js/` — NON CHARGÉ par le site actuel

> ⚠️ **Aucune page de ce site ne charge ces fichiers.** Vérifié : aucun `<script src="assets/js/...">`
> dans `index.html`, `initiation-efoil-debutant.html`, `efoil-golfe-saint-tropez.html` ni `reservation.html`.
> **Modifier ces fichiers n'a aucun effet sur le site en ligne.**

## Pourquoi ils sont là

Ce sont les briques d'un **tunnel réservation → paiement prévu pour WordPress**, écrites en amont
d'une éventuelle migration. Ils attendent un backend WP (`/wp-json/efca/v1/...`) qui **n'existe pas
aujourd'hui** — le site est un **site statique**.

| Fichier | Rôle prévu |
|---|---|
| `efca-config.js` | Config front (`window.EFCA_CONFIG`) : mode de paiement, prix unitaire, base API. Fallback pour preview statique. |
| `efca-reservation.js` | Tunnel réservation → paiement → succès. POST vers l'API REST WP. Contient un **stub Stripe** (non actif). |
| `efca-dashboard.js` | Dashboard réservations (démo). |
| `efca.js` | Utilitaires front. |

Ils sont **conservés volontairement** : c'est du travail préparé pour une version WordPress/paiement,
pas du code oublié. Ne pas les supprimer sans valider que la migration WP est abandonnée.

## Où est la vraie logique de réservation ?

**En inline, dans `reservation.html`** (bas de page, dans le `<script>`). C'est **elle** qu'il faut
modifier. Elle :

- poste vers le dashboard mutualisé `https://resa.efoil-beauvallon.fr/api/reservations?site=croixvalmer`
  (⚠️ le domaine `beauvallon` est **voulu** — un seul dashboard pour les 2 bases ; ne pas retirer `?site=croixvalmer`) ;
- utilise les identifiants préfixés **`rv-`** (`#rv-form`, `#rv-date`, `#rv-slot`, `#rv-name`, honeypot `#rv-hp`) —
  **et non** les identifiants `efca-*` attendus par `efca-reservation.js` ;
- applique le **délai minimum de réservation J+3** (constante `BOOKING_LEAD_DAYS`, fuseau Europe/Paris).

## En cas de migration WordPress

Ces fichiers redeviendront pertinents, mais il faudra **réaligner les identifiants** : le HTML actuel
utilise `rv-*`, alors que `efca-reservation.js` cible `#efca-reservation-form`, `#efca-form-error`,
`#efca-submit`, etc. Les deux mondes ne sont pas branchés l'un sur l'autre en l'état.
