# Temporary blog-only deployment

This branch intentionally publishes only the following article:

```text
https://jsous.github.io/blogs/is-physics-dead/
```

The complete lab website remains on the `main` branch and should not be used as
the GitHub Pages source yet.

## Build locally

```zsh
bundle install
bundle exec jekyll serve
```

Preview the article at:

```text
http://127.0.0.1:4000/blogs/is-physics-dead/
```

## Publish temporarily

In the repository's GitHub Pages settings, select **Deploy from a branch**, then
choose `tmp-blog-is-physics-dead` and `/(root)`.

When the full site is ready, change the publishing branch back to `main`.
