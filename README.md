# jsous.github.io

Minimal Jekyll starter site for John Sous' research lab at Yale University.

## Requirements

- Ruby 3.3+
- Bundler

On this machine, the Homebrew Ruby toolchain is used:

```zsh
ruby -v
bundle -v
```

## Install Dependencies

From the repository root, install the Jekyll and GitHub Pages gems:

```zsh
bundle install
```

## Build The Site

Generate the static site into `_site/`:

```zsh
bundle exec jekyll build
```

## Preview Locally

Start a local development server:

```zsh
bundle exec jekyll serve
```

Then open:

```text
http://127.0.0.1:4000/
```

## Edit Content

- Edit section pages in `pages/*.md`
- Current section pages live in:
  - `pages/about.md`
  - `pages/vitae.md`
  - `pages/people.md`
  - `pages/research.md`
  - `pages/publications.md`
  - `pages/blog-posts.md`
- Edit the homepage in `index.html`
- Edit the top navigation in `_includes/header.html`
- Edit site-wide layout wrappers in `_layouts/`
- Edit styles in `assets/css/style.scss`
- Edit placeholder images in `assets/images/`

## Group Members Page

Group members are cards in `pages/people.md`. To add or update yourself:

1. Put a headshot in `assets/images/` named `firstname-lastname.jpg`. Crop it to 4:3 (landscape) and resize to about 800 x 600 pixels; keep it under ~150 KB.
2. In your card, replace the placeholder `src` with your file, e.g.
   `{{ '/assets/images/firstname-lastname.jpg' | relative_url }}`,
   and change the `alt` text to `Portrait of Your Name.`
3. To link your name to a webpage, wrap it in a link inside the `<h3>`:
   `<h3><a href="https://your-site.example">Your Name</a></h3>`
4. Keep the one-line description in the same style as the others
   (role, program, `YYYY–present`; co-advisor if any).

Preview with `bundle exec jekyll serve`, then commit and push.

## GoatCounter

- Visit tracking is set in `_config.yml` (`goatcounter_site: "jsous.goatcounter.com"`) and loaded in `_layouts/default.html`.
- Stats are private, at https://jsous.goatcounter.com. There is no public visit counter on the site.
- To turn tracking off, set `goatcounter_site: ""`.

## Useful Notes

- The generated site output lives in `_site/`.
- Local gems are installed under `vendor/bundle/`.
- This setup is compatible with standard GitHub Pages Jekyll workflows.
