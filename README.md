# 8digriz.fr

Site vitrine statique : HTML + CSS, aucun JavaScript, aucun build, aucune dépendance,
aucune requête vers un service tiers à l'exécution.

Tout ce qui est publié vit dans `public/` — et rien d'autre n'est publié.

## Conventions

Aucun style ni script inline : la CSP (`public/_headers`) impose `style-src 'self'` et
`script-src 'self'` sans `'unsafe-inline'`. Tout CSS va dans un fichier de `public/assets/`.

Les liens internes et les `<link rel="canonical">` sont écrits sans `.html` : l'hébergeur sert
les pages sans extension et redirige `/page.html` vers `/page`.
