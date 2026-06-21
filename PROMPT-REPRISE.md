# PROMPT DE REPRISE — Site **eFoil Croix-Valmer** (dépôt autonome)

Colle ce prompt en début de nouvelle session. **Lis-le en entier** : la mémoire auto ne suit pas ce dossier.

---

## ⚠️ Nouveau (2026-06-21) — ce dossier est désormais un DÉPÔT GIT AUTONOME

- **Fini les worktrees / la branche `croix-valmer-landings` partagée.** Ce dossier a son **propre `.git`** indépendant.
- **Dossier** : `D:\efoil_sites\croix-valmer`
- **Branche** : `main` · **1er commit** : `init: site La Croix-Valmer autonome` (`da4fd93`)
- **Pas de remote GitHub** pour l'instant (à créer quand on voudra déployer).
- Les anciens liens `raw.githack.com/.../efoilcotedazur/croix-valmer-landings/...` **ne marchent plus** (branche supprimée). Preview = serveur local.
- ⚠️ **Vidéos hors git** : `assets/video/` est dans `.gitignore`. (Croix-Valmer n'a pas encore de vidéo — heros en photo — mais la règle reste pour le futur : hébergement LFS/CDN avant déploiement git.)

### Règles git (simples maintenant)
```
git branch --show-current   # doit afficher : main
git add <fichiers> && git commit -m "..."
# pas de pull/push tant qu'il n'y a pas de remote
```

---

## Le site

**eFoil à La Croix-Valmer**, initiation & location à la **plage de Gigaro** (golfe de Saint-Tropez).

> **Marque = « eFoil Croix-Valmer »** (PAS « Côte d'Azur »). Le domaine `efoilcotedazur.fr` reste l'entité, mais la page se présente sous le nom local.

---

## Fichiers présents (HTML uniquement Croix-Valmer)

| Fichier | Rôle |
|---|---|
| `croix-valmer.html` | **Page principale unique**. DA hybride « cinéma + marque EFCA » : police Inter, **orange `#F4631F` / turquoise `#00A7C7`**, boutons pilule, rating bar, vagues SVG, logo. Namespace `.cvx-`. Hero **photo aérienne** plein écran + ken-burns. **Bascule de thème orange ⇄ bleu** (bouton header → `[data-theme]` + swap hero + `localStorage`). |
| `croix-valmer-como.html` | Variante DA éditoriale teal/Archivo (style COMO). Namespace `.cv-`. |
| `dashboard.html` | Dashboard réservations (démo). |
| `trieur-photos.html` | Outil de tri des photos par slots. |

### Médias
- **Photos 100 % aériennes** : `medias/web/cv/` (`aer-01..37` + `hero-{orange,bleu,como}{,-v}`), générées par `tools/cv_aerial_media.py` depuis la curation `efca-photo-tri.json` (packs `aerien`/`top`/`sunset`/`lieu`, **sans riders classiques**).
- **Pas de vidéos** (pas encore prêtes) → heros en photo. Originaux lourds **gitignorés** ; seul `medias/web/` est destiné au web.

---

## À FAIRE ensuite
1. **Réservation** : brancher le `BOOKING_BLOCK` sur un vrai backend.
2. **Remplir les tokens `{{…}}`** : `{{PRIX}}`, `{{TÉLÉPHONE}}`, avis Google réels, etc.
3. **Vraies photos de Gigaro** quand disponibles ; **vidéos** quand prêtes (heros vidéo possible ensuite).
4. Décider de la variante retenue (`croix-valmer.html` orange⇄bleu vs `croix-valmer-como.html`).

## Preview locale
```
cd D:\efoil_sites\croix-valmer
python -m http.server 8000
# http://localhost:8000/croix-valmer.html
# http://localhost:8000/croix-valmer-como.html
```

## Déploiement (plus tard)
Créer un repo GitHub dédié → `git remote add origin <url>` → push. Si GitHub Pages et qu'on ajoute des vidéos : régler d'abord l'hébergement (LFS/CDN).

## Note
`11+Agents+SEO+_+GEO+-+RosoAI/` = squad d'agents SEO/GEO (copie locale, suivie par git).
