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

## GoatCounter

- GoatCounter tracking is wired into `_layouts/default.html`
- The visible counter is shown only on `index.html`
- To enable it, set `goatcounter_site` in `_config.yml`:

```yml
goatcounter_site: "YOURCODE.goatcounter.com"
```

- In GoatCounter settings, enable visitor counters if you want the visible homepage counter to appear

## Useful Notes

- The generated site output lives in `_site/`.
- Local gems are installed under `vendor/bundle/`.
- This setup is compatible with standard GitHub Pages Jekyll workflows.
