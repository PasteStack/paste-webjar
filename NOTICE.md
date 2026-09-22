# NOTICE

## paste-webjar

Copyright 2025–present Tomshley LLC

This product includes software developed and maintained by Tomshley LLC as part
of the PasteStack project.

---

## License

This repository's own build files are licensed under the **Apache License,
Version 2.0**; the full text is in the `LICENSE` file at the root of this
repository. The published jar's terms are the packaged upstream version's: upstream
`paste` 2.0.1 is Apache-2.0 licensed, which is what `pom.xml` declares.

---

## Trademarks

**Tomshley** and the **Tomshley logo** are trademarks of Tomshley LLC.

Use of these trademarks is governed by applicable trademark law and Tomshley
brand usage guidelines. Brand assets are **not** licensed under the Apache
License 2.0.

---

## Bundled Content

The published jar repackages the `paste` sources of the upstream version named by
the `upstreamVersion` property in `pom.xml`. That upstream project is licensed
under the Apache License, Version 2.0.

## Third-Party Notices

This repository carries no sources of its own beyond the build. What the jar
redistributes is decided by `upstreamVersion`, so the notices below describe that
version's contents rather than this repository's.

Upstream `paste` 2.0.1 includes the following third-party components under their
own terms. Each file retains its upstream notice, and those terms govern the
third-party portions rather than the Apache License 2.0 grant above.

| Path in the packaged sources | Component | Terms |
|---|---|---|
| `js/polyfills/ie8head/json2.js` | json2.js (json.org) | Public domain |
| `js/polyfills/ie8head/html5.js` | html5shiv / iepp | MIT or GPL-2.0, at the recipient's option |
| `js/polyfills/selectors.js` | selectivizr (Keith Clark), with ContentLoaded.js (Diego Perini) — forked, with local modifications | MIT |

Upstream has since removed all three. This section is cleared in the same change
that raises `upstreamVersion` to the release that drops them — not before, because
until then the jar still ships them.
