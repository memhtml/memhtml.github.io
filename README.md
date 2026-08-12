# memhtml.github.io

Origin-root files for `memhtml.github.io`. The documentation itself is built from
[`memhtml/memhtml`](https://github.com/memhtml/memhtml) and served at
<https://memhtml.github.io/memhtml/>.

This repository holds only what a project site cannot serve, because both are anchored to the
origin root by their own specifications:

- `robots.txt` — RFC 9309 §2.3 requires it at `/robots.txt`.
- `.well-known/security.txt` — RFC 9116, and RFC 8615 anchors `/.well-known/` at the root.
- `index.html` — a pointer, so the origin root is not a 404.

Nothing here is generated. If you are looking for the docs, their source is in the other
repository under `apps/docs`.
