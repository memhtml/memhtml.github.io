# memhtml.github.io

Publishes <https://memhtml.github.io/> — the memhtml documentation, at this origin's root.

The documentation's **source** lives in [`memhtml/memhtml`](https://github.com/memhtml/memhtml) under
`apps/docs`, beside the code it describes, so a doc ships in the same commit as the change it
documents. This repository only publishes it: `.github/workflows/docs.yml` checks that repository out,
builds the site with `DOCS_BASE=/`, and deploys the result to this repository's Pages.

The split exists because GitHub serves an origin root only from a repository named
`<org>.github.io`. Serving at the root rather than at `/memhtml` is not cosmetic — a base segment is a
standing source of defects, since a link comes out correct on whichever surface its producer prefixed
and wrong on the other. At the root, every consumer of the base becomes a no-op.

## What this repository adds to the build

Two things a docs build cannot provide, because both are anchored to an origin root by their own
specifications:

- `robots.txt` — RFC 9309 §2.3 requires it at `/robots.txt`.
- `.well-known/security.txt` — RFC 9116, and RFC 8615 anchors `/.well-known/` at the root.

The workflow copies them over the built site. `upload-pages-artifact` is called with
`include-hidden-files: true`, which is **required**: its default tar excludes `.[^/]*`, so
`/.well-known/` would be dropped and the site would build, deploy, and serve a 404 there with nothing
having failed.

## Freshness

A push to `memhtml/memhtml` does not trigger this. Publishing needs no credential — that repository is
public, and `GITHUB_TOKEN` cannot write across repositories — and the trade is that the site updates on
a daily schedule or whenever someone runs the workflow manually. To publish immediately:

```bash
gh workflow run docs.yml -R memhtml/memhtml.github.io
```
