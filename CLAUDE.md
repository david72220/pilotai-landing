# Site PilotAI — Landing page produit

Site statique Astro dédié à la présentation de PilotAI, le SaaS de gestion de projet avec IA souveraine.

## Stack
- Astro 6 (statique)
- Tailwind CSS v4 via PostCSS
- Fonts self-host (@fontsource)
- Hébergement : Vercel
- Domaine : `pilotai.alliance-digitale.fr` (sous-domaine)

## Structure
```
src/
├── layouts/Layout.astro     # Layout SEO + JSON-LD + animations
├── components/
│   ├── Header.astro          # Nav PilotAI (identité propre)
│   └── Footer.astro          # Footer PilotAI + lien retour AD
├── pages/
│   └── index.astro           # Landing page complète
└── styles/global.css         # Charte Alliance Digitale adaptée
```

## Développement
```bash
npm install
npm run dev      # localhost:4321
npm run build    # dist/
npm run preview  # preview du build
```

## Déploiement
- Repo GitHub : `david72220/pilotai-landing`
- Vercel : projet séparé, domaine `pilotai.alliance-digitale.fr`
- DNS : sous-domaine Hostinger → Vercel

## Charte graphique
Héritée du site Alliance Digitale :
- Bleu Alliance `#3B97D3`, Rouge accent `#9E2114`
- Fonds sombres `#070d18` / `#0B1120`
- Typo : Playfair Display / Space Grotesk (titres), Inter (corps)

## Sections de la landing page
1. Hero (badge + titre + CTA + mock Kanban)
2. Problème (3 cartes)
3. Solution (3 piliers)
4. Démo (placeholder vidéo + form email)
5. Comparatif (tableau vs Asana/Monday/ClickUp)
6. Témoignages (placeholders)
7. Tarif (essai 14j + sur devis)
8. FAQ (5 questions)
9. CTA final

## TODO
- [ ] Remplacer le placeholder du form email par Brevo API
- [ ] Ajouter la vidéo démo (septembre)
- [ ] Ajouter les vrais témoignages (post test utilisateurs)
- [ ] Configurer le DNS `pilotai.alliance-digitale.fr` → Vercel
- [ ] Créer OG image 1200×630