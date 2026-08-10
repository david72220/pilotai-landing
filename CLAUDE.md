# CLAUDE.md — Site PilotAI (Landing page produit)

Fichier d'instructions projet pour le site de présentation de PilotAI. Source de vérité pour l'architecture, les conventions, le déploiement et l'avancement.

---

## 0. Contexte

**Produit :** PilotAI — SaaS multi-tenant de gestion de projet avec IA hybride souveraine (Ollama local par défaut, ingestion réunions Notta, pilotage vocal PWA + Telegram, souveraineté RGPD Supabase UE).

**Ce site :** Landing page produit autonome, indépendante du site Alliance Digitale (`www.alliance-digitale.fr`). Un lien depuis le site Alliance Digitale sera fait quand David sera prêt.

**Plan marketing complet :** `../Appli gestion de projets/CLAUDE-LANCEMENT.md` et `../Appli gestion de projets/.hermes/plans/2026-07-27_lancement-marketing-pilotai.md`

**Script vidéo démo :** `../Appli gestion de projets/docs/marketing/script-video-demo.md`

---

## 1. Stack technique

| Couche | Techno | Notes |
|--------|--------|-------|
| Framework | **Astro 6** (statique) | `output: 'static'`, `trailingSlash: 'always'` |
| Styling | **Tailwind CSS v4** via PostCSS | `@tailwindcss/postcss` |
| Fonts | **@fontsource** (self-host) | Inter, Playfair Display, Space Grotesk |
| SEO | `@astrojs/sitemap` | `sitemap-index.xml` auto-généré |
| Hébergement | **Vercel** | Projet séparé du site Alliance Digitale |
| Repo GitHub | `david72220/pilotai-landing` | Branche `main` |
| Domaine cible | `pilotai.alliance-digitale.fr` | Sous-domaine Hostinger → Vercel (DNS à configurer) |
| Domaine actuel | `pilotai-landing.vercel.app` | URL Vercel par défaut, active |

---

## 2. Structure du projet

```
/Users/davidollivier/Documents/Antigravity/Site PilotAI/
├── astro.config.mjs              # config Astro statique + sitemap
├── postcss.config.mjs            # Tailwind v4 via PostCSS
├── tailwind.config.mjs           # tokens couleurs Alliance Digitale
├── tsconfig.json                 # TypeScript strict (Astro)
├── package.json                  # scripts + dépendances
├── CLAUDE.md                     # ce fichier
├── .gitignore
├── public/
│   └── robots.txt                # Allow + sitemap reference
└── src/
    ├── layouts/
    │   └── Layout.astro          # Layout SEO + JSON-LD + animations reveal
    ├── components/
    │   ├── Header.astro          # Nav PilotAI (identité propre, logo texte gradient)
    │   └── Footer.astro          # Footer PilotAI + lien retour alliance-digitale.fr
    ├── pages/
    │   └── index.astro           # Landing page complète (9 sections)
    └── styles/
        └── global.css            # Charte Alliance Digitale adaptée (boutons, panels, gradient)
```

---

## 3. Charte graphique

Héritée du site Alliance Digitale pour cohérence de marque :

| Élément | Valeur |
|---------|--------|
| Bleu Alliance | `#3B97D3` |
| Rouge accent | `#9E2114` |
| Fond sombre | `#070d18` / `#0B1120` |
| Typographie titres | Playfair Display / Space Grotesk |
| Typographie corps | Inter |
| Effets visuels | `relief-panel` (gradient border + blur), `gradient-text`, `fiber-pulse` |

Fonts en **self-host** via `@fontsource` (pas de Google Fonts CDN).

---

## 4. Sections de la landing page

| # | Section | ID ancre | Contenu |
|---|---------|----------|---------|
| 1 | Hero | — | Badge "Lancement octobre 2026" + titre "Gérez vos projets avec une IA qui reste chez vous" + CTA + mock Kanban visuel (3 colonnes, cartes, barre progression 62%) |
| 2 | Problème | `#probleme` | 3 cartes : Fuite de données / IA boîte noire / Pas faits pour l'oral |
| 3 | Solution | `#solution` | 3 piliers : IA souveraine (Ollama) / Ingestion réunions (Notta) / Pilotage vocal (PWA + Telegram) |
| 4 | Démo | `#demo` | Placeholder vidéo + form de capture email (placeholder Formspree, à remplacer par Brevo) |
| 5 | Comparatif | `#comparatif` | Tableau PilotAI vs Asana/Monday/ClickUp (7 critères) |
| 6 | Témoignages | — | 3 placeholders (remplir post tests utilisateurs septembre) |
| 7 | Tarif | — | 4 offres en cartes : Essai gratuit (14j, fonctions restreintes sans installation) / Base (IA souveraine + Notta + Gmail + vocal + routine + notifications) / Pro recommandé (Base + priorité, sous-tâches, suivi temps, progression, charge, récurrences, rapport IA) / Sur-mesure (Pro + modules à la carte : dépendances, budget, Eisenhower, auto-planif, relances, sentiment, Scrum Master). Note explicative sous les cartes : installation manuelle pour versions payantes. |
| 8 | FAQ | `#faq` | 5 questions : données extérieures / offline / quitter Asana / IA souveraine / prix |
| 9 | CTA final | — | "Prêt à gérer vos projets avec une IA souveraine ?" + bouton démo |

---

## 5. SEO

- `sitemap-index.xml` + `sitemap-0.xml` auto-générés via `@astrojs/sitemap`
- `robots.txt` autorise tous les crawlers, référence le sitemap
- Canonical pointe vers `https://pilotai.alliance-digitale.fr/` (configuré dans `astro.config.mjs` `site:`)
- JSON-LD `SoftwareApplication` sur la page (nom, catégorie, description, offre, éditeur)
- OG image : placeholder `og-image.png` (à créer en 1200×630)
- Self-host fonts (zéro 3rd-party DNS)

---

## 6. Développement

```bash
npm install
npm run dev        # serveur local sur localhost:4321
npm run build      # build statique dans dist/
npm run preview    # preview du dist/
```

---

## 7. Déploiement

```bash
# Git : commit + push
git add -A && git commit -m "feat: description" && git push origin main

# Vercel : déployer en production
npx vercel@latest --prod --yes --name pilotai-landing
```

Le projet Vercel est détecté automatiquement comme Astro (Build Command: `astro build`, Output Directory: `dist`).

### DNS (à configurer)
- Ajouter un enregistrement CNAME `pilotai` → `cname.vercel-dns.com` dans le DNS Hostinger du domaine `alliance-digitale.fr`
- Ajouter le domaine `pilotai.alliance-digitale.fr` dans les Vercel Project Settings → Domains

---

## 8. Décisions arrêtées

| # | Question | Décision | Date |
|---|----------|----------|------|
| Q1 | Nom commercial | PilotAI | 27/07/2026 |
| Q2 | Support présentation | Landing page indépendante (projet séparé) | 27/07/2026 |
| Q5 | Techno landing | Astro 6 dédié (pas Framer) — validé à l'exécution | 27/07/2026 |
| Q7 | Domaine | `pilotai.alliance-digitale.fr` (sous-domaine, `pilotai.fr` pris) | 27/07/2026 |
| Q9 | Tarif affiché | 4 offres : Essai gratuit (14j, fonctions restreintes) / Base / Pro (recommandé) / Sur-mesure. Versions payantes sur devis (installation manuelle) | 27/07/2026 |

---

## 9. Avancement

### ✅ Fait (27/07/2026)

- Vérification domaine `pilotai.fr` → déjà pris (OVH, 30/09/2025). Fallback sous-domaine.
- Projet Astro 6 créé avec charte graphique Alliance Digitale (couleurs, typos, effects)
- Header.astro : nav propre PilotAI (logo texte gradient, menu ancré, responsive mobile)
- Footer.astro : footer PilotAI + lien retour alliance-digitale.fr + contact
- Layout.astro : SEO complet (canonical, OG, Twitter Card, JSON-LD SoftwareApplication) + animations reveal
- index.astro : landing page complète 9 sections (hero + mock Kanban, problème, solution, démo + form, comparatif, témoignages, tarif, FAQ, CTA)
- global.css : charte adaptée (btn-primary/secondary, relief-panel, gradient-text, fonts)
- robots.txt + sitemap auto-généré
- Repo GitHub créé : `david72220/pilotai-landing` — https://github.com/david72220/pilotai-landing
- Premier commit poussé sur `main`
- Déploiement Vercel réussi : **https://pilotai-landing.vercel.app** (200 OK, build en 16s)
- Script vidéo démo rédigé : `../Appli gestion de projets/docs/marketing/script-video-demo.md`

### ⬜ À faire

| Tâche | Délai | Notes |
|-------|-------|-------|
| Configurer DNS `pilotai.alliance-digitale.fr` → Vercel | Août | CNAME Hostinger + ajout domaine Vercel |
| Remplacer placeholder form email par Brevo API | Août S34 | `action="https://formspree.io/f/placeholder"` → endpoint Brevo |
| Configurer email auto de confirmation (Brevo) | Août S34 | Sender `accueil@kmc.ci`, template avec lien Cal.eu |
| Configurer Cal.eu pour démos personnalisées | Août S34 | Lien Cal dans l'email auto |
| Créer OG image 1200×630 | Août | `public/og-image.png` |
| Enregistrer + ajouter la vidéo démo | Septembre | Teaser 90s + démo 2-3min (voir script) |
| Ajouter les vrais témoignages | Septembre | Post tests utilisateurs (5-10 sessions) |
| Intégrer lien depuis site Alliance Digitale | Quand David prêt | Section sur `index.astro` + liens Header/Footer |

---

## 10. Points de vigilance

- Ne jamais commiter le `.env` réel (le projet n'en a pas besoin pour l'instant, mais Brevo API key sera nécessaire)
- Le canonical pointe vers `pilotai.alliance-digitale.fr` qui n'existe pas encore — le SEO sera correct une fois le DNS branché
- Le form email est un placeholder visuel non fonctionnel — ne pas laisser en production sans le brancher
- Les témoignages sont des placeholders — à remplacer par de vrais témoignages post tests
- La vidéo démo est un placeholder — à remplacer par la vraie vidéo en septembre
- `pilotai.fr` est pris par un tiers — ne pas tenter de l'acheter, utiliser le sous-domaine

---

## 11. Journal d'avancement

### Session 1 — 27/07/2026 — Création et déploiement

**Fait :**
- Projet Astro 6 créé de zéro dans `/Users/davidollivier/Documents/Antigravity/Site PilotAI/`
- Charte graphique Alliance Digitale adaptée (couleurs, typos, relief-panels, gradient-text, fonts self-host)
- Header.astro : nav propre PilotAI avec logo texte gradient, menu ancré (#probleme, #solution, #demo, #comparatif, #faq), responsive mobile avec burger
- Footer.astro : 3 colonnes (description + lien AD, navigation, contact), lien retour alliance-digitale.fr
- Layout.astro : head SEO complet (canonical, OG, Twitter Card, JSON-LD SoftwareApplication), animations reveal IntersectionObserver + hero animations staggered
- index.astro : 9 sections complètes
  - Hero : badge animé, titre gradient, CTA, mock Kanban visuel (3 colonnes À faire/En cours/En retard, cartes avec assignee/dates, barre progression 62%)
  - Problème : 3 cartes (Fuite de données, IA boîte noire, Pas faits pour l'oral)
  - Solution : 3 piliers détaillés (IA souveraine/Ollama, Ingestion réunions/Notta, Pilotage vocal/PWA+Telegram) avec listes de features
  - Démo : placeholder vidéo + form email (placeholder Formspree)
  - Comparatif : tableau 7 critères PilotAI vs Asana/Monday/ClickUp
  - Témoignages : 3 placeholders
  - Tarif : essai 14j gratuit + sur devis
  - FAQ : 5 questions en accordéon
  - CTA final
- global.css : adaptation de la charte AD (btn-primary/secondary, relief-panel/relief-1/relief-2, gradient-text, prefers-reduced-motion)
- robots.txt + sitemap via @astrojs/sitemap
- Build local réussi : 1 page en 1.44s
- Repo GitHub créé et poussé : `david72220/pilotai-landing`
- Déploiement Vercel réussi : `pilotai-landing.vercel.app` (200 OK, 16s)

**Décisions :**
- Q5 amendée : Astro dédié au lieu de Framer (David a préféré utiliser son processus GitHub+Vercel existant)
- Q7 confirmée : sous-domaine `pilotai.alliance-digitale.fr` (`pilotai.fr` pris chez OVH)

**Prochaine étape :** Brancher DNS, form email Brevo, vidéo démo.