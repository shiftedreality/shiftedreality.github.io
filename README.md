# shiftedreality.dev

Source for [shiftedreality.dev](https://shiftedreality.dev) — Oleg Posyniak's personal landing page. Built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages.

## Structure

- `index.html` — landing page content
- `_layouts/landing.html` — document structure and SEO metadata
- `_includes/` — inline landing-page styles, favicons, and deferred analytics
- `_config.yml` — site identity, social links, and analytics configuration
- `CNAME` — custom domain for GitHub Pages

## Local development

```bash
bundle install
bundle exec jekyll serve
```

Site will be available at `http://localhost:4000`.

## Publishing

Push to `main`; GitHub Pages builds and deploys automatically.

## License

MIT — see [LICENSE](LICENSE).
