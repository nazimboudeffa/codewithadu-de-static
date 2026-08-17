# Code with a Dude — Analyse du design et plan d'amélioration

> Note : les images (`hero.png`, `substack-logo.png`) n'ont pas pu être analysées (le modèle ne gère pas les entrées visuelles). Cette analyse porte sur la structure et le code HTML/CSS de `index.html`.

## 1. Analyse du design actuel

### Structure

Landing page mono-fichier (`index.html`, 346 lignes) en Tailwind CDN + Inter. Six blocs plein écran :

| # | Section | Contenu |
|---|---------|---------|
| 1 | Hero | Image plein écran (`hero.png`) + titre « You want a cool web site? » + CTA « BOOK A CALL » |
| 2 | Intro | « About My Approach » — encart à bordure verte, 6 phrases |
| 3 | Pricing | « How It Works » — 3 colonnes (Learn and Code / Landing Pages / SaaS) + encart « Donate Instead » |
| 4 | FAQ | 5 questions en accordéon |
| 5 | Contact | « KEEP IN TOUCH » + logo Substack + vidéo YouTube |
| 6 | Footer | Liens vers les autres expérimentations |

### Système visuel

- **Couleur** : accent vert/émeraude dominant, mais chaque section change de dégradé (lime, teal, cyan, sky…), le sélecteur de langue est violet, les liens footer sont bleus et les FAQ utilisent un arc-en-ciel de dégradés. C'est un site « une palette par section ».
- **Typographie** : Inter partout, titres en `font-extrabold` + texte en dégradé (`bg-clip-text`). Pas de hiérarchie display/body, pas de mono.
- **Icônes** : émojis fonctionnels (🌱🚀🏆💬💡⏱🎁🌿👈). Pas de système d'icônes.
- **Interactions** : hover scale+shadow sur presque tout, deux CTA solides pour le même calendrier, dégradé ombre verte au survol.
- **Personnalité** : copy décontractée et honnête (« Take it easy », don au lieu de prix fixe) — un vrai caractère, mais anglais bancal (« how much costs your project ») et un message contradictoire (300€ annoncé, puis « donnez ce que vous voulez »).

## 2. Plan d'amélioration

### P0 — Fondations (cohérence, santé)

1. **Palette unique + tokens** : un seul accent vert, décliné en OKLCH (`--bg`, `--surface`, `--fg`, `--muted`, `--border`, `--accent`). Purger le violet du sélecteur de langue, le bleu des liens footer, les dégradés multicolores des FAQ. Un dégradé par écran maximum.
2. **Typographie appariée** : garder Inter en corps, ajouter une serif ou un display distinct pour les titres + une mono pour les données/eyebrows (le site est centré Next.js/dev, une mono évoque le code).
3. **Système d'icônes** : remplacer les émojis par des SVG dessinés, une seule épaisseur de trait, couleur accent.
4. **Corriger les bugs** : favicon cassé (`../src/app/favicon.ico`), `hero.png` à 1,3 Mo (compresser/webp), couverture i18n incomplète (le titre FAQ et le footer « Explore more » ne sont pas traduits).

### P1 — Hiérarchie & clarté

5. **Rythme de page** : abandonner `min-h-screen` sur chaque section pour un vrai flux éditorial ; la page perd sa continuité en « diapos » déconnectées.
6. **Économie de CTA** : un seul bouton primaire (le calendrier) ; le second devient un lien secondaire. Revoir le badge « Interesting » et le titre « How It Works » (c'est un bloc services).
7. **Copy** : réécrire les phrases bancales en gardant le ton décontracté (c'est la marque de fabrique), et lever la contradiction 300€ vs « don libre » — soit un prix clair, soit un encart « donation » assumé.
8. **Appel intro** : le motif « barre verte verticale + carte arrondie » est un cliché ; le remplacer par un traitement plus typographique.

### P2 — Accessibilité, SEO, performance

9. `:focus-visible` sur tous les éléments interactifs, contraste des textes en dégradé (souvent faibles sur fond clair), `aria-expanded` sur le menu langue.
10. Balises OG/Twitter + données structurées, `alt` descriptifs.
11. Retirer le CDN Tailwind en prod (purger/compiler) — le Play CDN est pour le développement.