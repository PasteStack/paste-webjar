# Unreleased

## Fixed

- The jar now carries upstream's `LICENSE` (and its notice file when upstream has
  one). It repackages upstream sources under the Apache License, whose
  redistribution terms require the license text to travel with them, and only the
  `src` tree was being copied. CI refuses a jar without it.
- The pipeline can run: the publish job no longer calls toolbox scripts that exist
  only inside the house runner images while running on a public Maven image.
- Branch pipelines publish the pinnable `{ref-slug}-{sha}` and rolling
  `{ref-slug}-latest` versions instead of redeploying the released coordinates.
- Version agreement (`VERSION`, the pom's `<version>`, and `<upstreamVersion>`) is
  read through Maven. A tag that does not match `VERSION` refuses to publish.
- The README's deploy instructions named an unrelated environment file; they now
  name the registry credentials the `settings.xml` server entry reads.

## Licensing

- This repository's own build files are licensed under the Apache License,
  Version 2.0 (`LICENSE`, `NOTICE.md`). The pom's `<licenses>` describes the packaged
  `upstreamVersion` and now matches it; it previously named MIT for Apache-2.0
  licensed upstream sources.
- `NOTICE.md` records the third-party components the packaged sources carry, keyed
  to `upstreamVersion` rather than to this repository, since that property decides
  what the jar redistributes.

# paste-webjar v0.1.0

**Date:** 2026-02-07

## Initial Release

- Updated `pom.xml`: PasteStack branding, license metadata, updated SCM URLs
- Added multi-project shared `.gitignore` with Maven ignores
- WebJar packaging for paste core JS via Maven
