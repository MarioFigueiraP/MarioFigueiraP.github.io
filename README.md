# Project scaffold — Relearn docs site + custom hero homepage

This is the full file set needed to run the setup we built:
a Hugo site using the **Relearn** theme for documentation, with a
custom one-page **hero-style homepage** that
links into the docs.

```
site-scaffold/
├── hugo.toml                     # site config
├── content/
│   ├── _index.md                 # homepage stub (content ignored, see below)
│   └── inla/_index.md            # example doc chapter — replace with your real content
├── data/
│   └── profile.yaml              # ALL homepage text/links — edit this for content changes
├── layouts/
│   └── index.html                # homepage template, reads from data/profile.yaml
├── static/
│   └── README-static.txt         # delete after adding your CV/photos here
├── .github/workflows/hugo.yml    # builds & deploys to GitHub Pages automatically
└── .gitignore
```

## 1. Install Hugo (extended version)

You need the **extended** edition of Hugo (required by most themes, including Relearn).

- macOS: `brew install hugo`
- Windows: `choco install hugo-extended` or `winget install Hugo.Hugo.Extended`
- Linux: see https://gohugo.io/installation/linux/
- Verify with: `hugo version` — it should say `extended`.

## 2. Get this scaffold into a git repo

If you're starting fresh:

```bash
mkdir mariofigueirap.github.io
cd mariofigueirap.github.io
git init
# copy all files from this scaffold into this folder
```

If you're merging into your **existing** repo instead, just copy
`layouts/index.html`, `data/profile.yaml`, `.github/workflows/hugo.yml`,
and merge the settings from `hugo.toml` into your current config —
don't overwrite your existing `content/` folder.

## 3. Add the Relearn theme as a submodule

```bash
git submodule add https://github.com/McShelby/hugo-theme-relearn.git themes/relearn
git submodule update --init --recursive
```

(If you already have Relearn installed in your current repo, skip this —
just make sure `theme = "relearn"` in `hugo.toml` matches your folder name.)

## 4. Add your real content

- Edit `data/profile.yaml` — hero text, research topics, publications, career timeline, CV filename, contact links.
- Put your CV PDF and any images in `static/` (paths are documented inside `data/profile.yaml` and `static/README-static.txt`).
- Move your actual documentation pages into `content/inla/` (and any other chapters), replacing the placeholder `_index.md`.

## 5. Preview locally

```bash
hugo server -D
```

Visit `http://localhost:1313` — your homepage should now show the hero layout, while `/inla/` and other chapters render through Relearn as before.

## 6. Deploy to GitHub Pages

Two options:

**A. Automatic (recommended) — the included GitHub Action**

1. Push this repo to GitHub as `mariofigueirap.github.io`.
2. In the repo, go to **Settings → Pages → Build and deployment → Source**, and select **GitHub Actions**.
3. Push to `main` — `.github/workflows/hugo.yml` will build and deploy automatically on every push.

**B. Manual**

```bash
hugo --minify
# commit and push the contents of ./public to whichever branch
# your GitHub Pages settings currently point to
```

## Notes

- `content/_index.md` only needs front matter — Hugo requires *some* file there for the homepage, but `layouts/index.html` overrides all of its rendering.
- Everything under `content/` other than the homepage keeps using Relearn's normal chapter/sidebar layout untouched.
- If you use Relearn's language switcher (EN/ES) or theme switcher (Learn/Neon/etc.) today, those UI elements are **not** included in the custom homepage — they'll still work on your doc pages. Let me know if you'd like them added to the homepage nav too.
