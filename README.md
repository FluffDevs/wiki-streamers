# wiki-streamers

Wiki de documentation pour aider les streamers Fluff Radio a passer en direct (SRT/RTMP, panel, OBS), et guide complet du panel d'administration `programmation.fluffradio.com` pour le staff.

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

### Streamers / animateurs

1. Lire les pre-requis (mode SRT ou RTMP du compte)
2. Recuperer son lien de connexion depuis le panel (automatique 10 min avant en SRT, manuel en RTMP)
3. Configurer OBS
4. Lancer le stream
5. Resoudre les incidents via le troubleshooting

### Staff (admins, programmateurs, uploadeurs...)

Guide complet du panel `programmation.fluffradio.com` : `fr/panel-admin/` (ref `admin-guide`), `en/panel-admin/`. Couvre l'authentification, chaque page du tableau de bord (mediatheque, fichiers audio, playlists, programmations, habillage d'antenne, validation musiques, streamers, debug API, cache), un glossaire et une FAQ.

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
- FR: `fr/panel-admin/index.md` avec `lang: fr`, `ref: admin-guide`
- EN: `en/panel-admin/index.md` avec `lang: en`, `ref: admin-guide`

Note: la page `admin-guide` n'est pas enregistree dans `_includes/page-nav.html` (qui ne gere que le parcours streamer classique) — elle affiche donc un fil d'ariane simple (Accueil > titre) sans navigation precedent/suivant, ce qui est attendu vu sa taille (page de reference unique, pas une etape d'un parcours lineaire).

## Contenu volontairement sans valeurs fixes

Les guides detaillent la methode (quoi verifier, dans quel ordre, comment diagnostiquer)
sans imposer de valeurs techniques arbitraires (bitrate exact, presets encodeur, etc.).

Les valeurs operationnelles doivent rester celles validees par l'equipe technique.

## Publier le site

Le deploiement GitHub Pages est gere par le workflow:

- `.github/workflows/jekyll-gh-pages.yml`

Chaque push sur `main` declenche le build et le deploiement.
