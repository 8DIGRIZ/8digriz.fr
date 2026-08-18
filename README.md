# 8digriz.fr

Site vitrine de la SASU **8DIGRIZ**. Statique : HTML + CSS, aucun JavaScript, aucun build,
aucune dépendance, aucune requête vers un service tiers à l'exécution.

## Contenu

| Fichier | Rôle |
|---|---|
| `index.html` | Accueil : nom, activité, contact — aucune donnée d'immatriculation |
| `mentions-legales.html` | Mentions légales (art. 6-III LCEN) |
| `confidentialite.html` | Politique de confidentialité (RGPD) |
| `404.html` | Page d'erreur |
| `assets/style.css` | Feuille de style unique, `@font-face` inclus |
| `assets/fonts/` | Polices auto-hébergées (subset `latin`, 113 Ko au total) |
| `_headers` | En-têtes de sécurité et cache, lus par Cloudflare Pages |
| `robots.txt`, `sitemap.xml`, `favicon.svg` | Métadonnées |

## Déploiement — Cloudflare Pages

Aucune commande de build. **Build command** : vide. **Build output directory** : `/`.

    npx wrangler pages deploy . --project-name=8digriz

Ou via le dashboard : *Workers & Pages → Create → Pages → Upload assets*, glisser le dossier.

## DNS — le domaine est chez OVH, l'hébergement chez Cloudflare

Le domaine et la messagerie (`contact@8digriz.fr`) restent gérés par OVH. Deux options :

1. **Nameservers Cloudflare** (recommandé) — Cloudflare importe la zone existante ;
   **vérifier que les enregistrements `MX`, `SPF`, `DKIM` et `DMARC` d'OVH ont bien été repris
   avant de basculer les NS chez OVH**, sinon la messagerie tombe. L'apex `8digriz.fr` est alors
   résolu par CNAME flattening vers le projet Pages.
2. **DNS conservé chez OVH** — OVH ne supporte pas de `CNAME` à l'apex : router
   `www.8digriz.fr` en `CNAME` vers `<projet>.pages.dev`, puis créer une redirection
   `8digriz.fr → www.8digriz.fr` dans l'interface OVH.

## Modifier une donnée légale

Les identifiants (SIREN, SIRET, TVA, adresse, capital, nom du président) n'apparaissent **que**
dans `mentions-legales.html` et `confidentialite.html` — volontairement pas sur l'accueil, ni
dans un bloc JSON-LD. Vérifier ces deux fichiers en cas de changement :

    grep -rn '877 773 689\|87777368900030\|FR96\|Pagnol' *.html

Les deux pages légales sont en `noindex, follow` et hors `sitemap.xml` : elles restent publiques
et liées depuis chaque page (exigence LCEN d'accès facile, direct et permanent), mais leur contenu
n'alimente pas les moteurs de recherche. Ne pas les remettre en `index`.
