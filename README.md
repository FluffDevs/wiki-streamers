# wiki-streamers

Wiki de documentation pour aider les streamers Fluff Radio a configurer OBS et diffuser sur le serveur RTMP.

Le site est bilingue avec une structure i18n complete basee sur Jekyll.

## Architecture actuelle

- `index.md`: redirection de `/` vers `/fr/`
- `fr/`: routes FR (pages legeres: front matter + renderer)
- `en/`: routes EN (pages legeres: front matter + renderer)
- `_includes/render-i18n-page.html`: renderer unique qui charge le contenu selon `lang` + `ref`
- `_includes/lang-switcher.html`: switch FR/EN base sur `lang` + `ref`
- `_includes/t.html`: helper de traduction avec fallback pour textes UI
- `_data/i18n/fr.yml` et `_data/i18n/en.yml`: dictionnaires UI
- `_data/i18n_pages/fr.yml` et `_data/i18n_pages/en.yml`: contenu editorial complet par langue
- `_config.yml`: configuration Jekyll/GitHub Pages

## Parcours utilisateur cible

1. Lire les pre-requis
2. Recuperer les identifiants (serveur RTMP + passphrase unique)
3. Configurer OBS
4. Lancer le stream
5. Resoudre les incidents via le troubleshooting

## Convention i18n

Chaque page localisee contient dans son front matter:

- `lang`: code langue (`fr` ou `en`)
- `ref`: identifiant commun entre traductions d'une meme page

Le switch langue affiche automatiquement les pages partageant le meme `ref`.

Les labels transverses (ex: libelle du switch de langue) sont resolus via les dictionnaires `_data/i18n/*`.

Le contenu editorial des pages est centralise dans `_data/i18n_pages/`.
Les pages markdown servent de points d'entree de route et appellent toutes le meme renderer.

Exemple logique:

- FR: `fr/guides/configurer-obs.md` avec `lang: fr`, `ref: configure-obs`
- EN: `en/guides/configure-obs.md` avec `lang: en`, `ref: configure-obs`

## Contenu volontairement sans valeurs fixes

Les guides detaillent la methode (quoi verifier, dans quel ordre, comment diagnostiquer)
sans imposer de valeurs techniques arbitraires (bitrate exact, presets encodeur, etc.).

Les valeurs operationnelles doivent rester celles validees par l'equipe technique.

## Publier le site

Le deploiement GitHub Pages est gere par le workflow:

- `.github/workflows/jekyll-gh-pages.yml`

Chaque push sur `main` declenche le build et le deploiement.
