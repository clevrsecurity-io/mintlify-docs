# Clevr Sales & Channel Playbook — Mintlify source

Internal, confidential. This folder is a self-contained Mintlify docs project for the
playbook. Mintlify renders these files; there is no build step and nothing is stored
in Mintlify itself. Change the files, push, Mintlify redeploys.

## What's here
- `docs.json` — nav, theme (Clevr violet), logo, `noindex` (hidden from search engines).
- `*.mdx` — one page per playbook section (20 pages, grouped in `docs.json`).
- `style.css` — small custom CSS (verdict pills, intro lede).
- `images/` — logo (light/dark), favicon, and the diagrams as **light + dark SVG pairs**
  (`dg-*.svg` light, `dg-*-d.svg` dark; the `.mdx` shows the right one per theme).

## Preview locally (no Node needed, uses Docker)
```bash
cd "path/to/playbook-mintlify"
docker run --rm -it -p 3000:3000 -v "$PWD:/docs" -w /docs node:22-alpine \
  sh -c "npm i -g mint && mint dev"
# open http://localhost:3000
```
Do this before you connect it, to confirm it renders.

## Publish it (one time)
Keep this SEPARATE from the public product docs (it names competitors + pricing).
1. Put this folder in its **own private GitHub repo**.
2. In the Mintlify dashboard, **connect that repo**; set the docs directory to the repo root.
3. Push. Mintlify deploys on every push to the connected branch.
4. Custom domain: point a subdomain, e.g. **`partners.clevrsecurity.com`**, at the target Mintlify gives you.

After that, updating = edit an `.mdx`, commit, push. Live in seconds.

## Gating it (the "login" question)
- **Share by link (any plan):** it's live at your URL, `noindex` keeps it out of search,
  but anyone with the link can open it. This is "unlisted", not private.
- **Real login (paid plan):** Mintlify Authentication gates the whole site. Simplest is a
  **shared password**; for per-partner access use **SSO/JWT** wired to your app. Configure
  it in the Mintlify dashboard once you're on a plan that includes it.

## Editing the content
- Text/tables/callouts: edit the `.mdx` directly (Mintlify components: `<Info>`, `<Warning>`,
  `<Check>`, `<Card>`, `<CardGroup>`, `<Frame>`).
- Diagrams: they're SVG files in `images/`. To re-style, edit both the light and the dark
  file, or regenerate from the source playbook.
- Source of truth for the content is the playbook Artifact; this Mintlify copy was generated
  from it. If you change one, mirror the other (or tell Claude to regenerate).
