# shiftedreality.dev

Source for [shiftedreality.dev](https://shiftedreality.dev) — Oleg Posyniak's personal blog, covering **tech & AI** and **finance & investing**. Built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages.

The theme is a heavily customized fork of [Reverie](https://github.com/amitmerchant1990/reverie) by Amit Merchant (see [LICENSE](LICENSE)).

## Structure

- `_posts/` — blog posts (Markdown, front matter sets `categories: it-ai` or `categories: finance-investing`)
- `_pages/` — static pages: [about](_pages/about.md), [archive](_pages/archive.md), [categories](_pages/categories.md), [search](_pages/search.md), and the two category landing pages ([it-ai](_pages/it-ai.md), [finance-investing](_pages/finance-investing.md))
- `_layouts/` / `_includes/` — page templates and shared partials (head meta, analytics, Disqus, social icons)
- `_sass/` / `assets/style.scss` — styling
- `search.json` + `assets/simple-jekyll-search.min.js` — client-side fuzzy search across posts
- `_config.yml` — site config (name, description, social links, analytics, pagination)
- `CNAME` — custom domain for GitHub Pages
- `app-ads.txt` — AdSense app-ads verification

## Local development

```bash
bundle install
bundle exec jekyll serve
```

Site will be available at `http://localhost:4000`.

## Publishing

Push to `main`; GitHub Pages builds and deploys automatically.

## License

MIT, inherited from the original [Reverie](https://github.com/amitmerchant1990/reverie) theme — see [LICENSE](LICENSE).
