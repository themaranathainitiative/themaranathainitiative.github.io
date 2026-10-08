# Maranatha Initiative

A personal publication by Benjamin Perkins: **Scripture, culture, and everything in between.**

Built with Jekyll and the gem-based [Chirpy theme](https://github.com/cotes2020/jekyll-theme-chirpy), served by GitHub Pages at <https://maranathainitiative.org>. The Gemfile targets Chirpy `~> 7.6`; the initial design was checked against 7.6.0. The theme remains a gem dependency; only the documented local overrides live in this repository.

## Preview and verify

Use Ruby **3.4**, as the existing GitHub Actions workflow does. Chirpy 7.6 requires Ruby 3.x; Ruby 4 is incompatible.

```sh
bundle install
bundle exec jekyll serve
```

Open <http://127.0.0.1:4000>. Restart Jekyll after changing `_config.yml`.

To run the production build and internal HTML/link checks used in deployment:

```sh
bash tools/test.sh
```

The existing `.github/workflows/pages-deploy.yml` builds, tests, and deploys pushes to `main` or `master`. `CNAME` and `_config.yml` both specify `maranathainitiative.org`. Keep the custom domain configured in GitHub Pages and its DNS records; these repository settings do not change DNS.

## Publish an article

1. Copy [docs/post-template.md](docs/post-template.md) to `_posts/YYYY-MM-DD-your-title.md`.
2. Replace the title, date, and description; write the article body.
3. Use `-0400` during Eastern daylight time and `-0500` during Eastern standard time. The site timezone is `America/New_York`.
4. Add categories and tags only as needed, for example `categories: [Technology]` and `tags: [reading, software]`. Chirpy treats multiple categories as a hierarchy; use tags for topics that overlap.
5. Add an optional image with meaningful alt text, or leave the image fields commented out.
6. Preview, verify, and commit the post. Future-dated posts stay unpublished until their date and a subsequent build.

The template lives in `docs/`, which is excluded from the published site. No sample articles are published. For unpublished work, use `_drafts/your-title.md` and preview with `bundle exec jekyll serve --drafts`.

Chirpy continues to supply dates, author attribution, descriptions, categories, tags, search, archives, a table of contents, footnotes, image handling, code highlighting, related posts, and pagination. The author defaults to `social.name` in `_config.yml`; no per-post author is needed.

Use normal Markdown for Scripture references. An optional no-wrap class is available: `John 1:1–5{: .scripture-reference }`. Footnotes use `[^1]` and a definition such as `[^1]: Source details.`

## Adjust the design and content

| Change | File |
| --- | --- |
| Colors | `assets/css/publication.css`: brand tokens, light/dark palettes, then Chirpy variable mappings |
| Typography | `assets/css/publication.css`: serif and sans font stacks, followed by reading styles |
| Title, tagline, author, SEO description | `_config.yml` |
| Homepage introductory labels | `index.html` |
| About text | `_tabs/about.md` |
| Navigation | `_tabs/*.md`: `order` and `icon` front matter; Chirpy generates the sidebar |
| Public contact links | `_data/contact.yml` and corresponding configuration fields |
| Content license wording | `_data/locales/en.yml` (starter CC BY statement omitted) |
| Optional share platforms | `_data/share.yml` (currently empty; copy-link remains available) |
| Favicon and installed-app branding | `assets/img/favicons/` |

The **Midnight & Parchment** palette starts with parchment `#F6F2E9`, midnight `#233C50`, antique gold `#B38A55`, and charcoal `#33353A`. Change the four `--publication-*` brand tokens at the top of the stylesheet, then adjust the semantic light/dark palette as needed. Gold is used for small rules and borders. For ordinary text, use `--publication-gold-ink` (`#79572F` in light mode, `#D4AE78` in dark mode), which has stronger contrast. The sidebar has its own text, hover, and focus tokens because it stays dark in both modes. Recheck text and focus contrast after changing colors. Browser theme colors in `_includes/head.html` and installed-app/favicon colors in `assets/img/favicons/` should follow palette changes.

The publication uses system fonts for its custom typography. There is no additional font download, JavaScript dependency, CMS, or backend. Existing comments and analytics are disabled. RSS and Chirpy's existing PWA remain available. Leave `theme_mode` empty to retain system preference and the Light/Dark/System menu.

## Theme upgrades and local overrides

Most customization is plain CSS, loaded last through `_includes/metadata-hook.html`. Chirpy retains control of responsive layout, search, navigation, theme switching, and article markup.

Only two full templates are overridden, both based on Chirpy **7.6.0**:

- `_layouts/home.html`: renders `index.html` content above the existing post feed, provides an empty state, and uses `h2` for article titles under the publication's `h1`. Categories appear above titles; dates and reading times appear below excerpts using Chirpy’s helpers. Pinned posts, preview images, summaries, and pagination retain upstream behavior.
- `_includes/head.html`: allows browser zoom in the viewport declaration and sets parchment light/navy dark browser theme colors, and omits unused remote font loading. All SEO, asset loading, analytics guards, and metadata hooks retain upstream behavior.

`assets/img/favicons/site.webmanifest` retains Chirpy's generated metadata and paths with custom theme/background colors. Other favicon files replace the theme's starter mark.

When updating Chirpy, compare these overrides against the installed gem (`bundle info jekyll-theme-chirpy --path`) and reapply the small documented changes. Check light, dark, and system modes, the mobile menu, search, post images, TOC, and pagination. The small `_data/locales/en.yml` override suppresses the starter's Creative Commons statement so it does not assign a license to future articles; other English labels are inherited.

The theme and starter code remain covered by the repository's MIT [license](LICENSE).
