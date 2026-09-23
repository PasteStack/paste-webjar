# paste-webjar

WebJar packaging for the PasteStack core JavaScript utilities. The default release
build downloads the upstream `paste` release tag named by the `upstreamVersion`
property in `pom.xml` and repackages its sources under
`META-INF/resources/webjars/paste-webjar/{project.version}/`, so a JVM application can
serve them without a separate asset checkout.

Branch builds instead run with `-Pdevelopment-upstream`, which downloads the immutable
upstream development archive committed in the pom (`upstream.development.url`,
`upstream.development.version`, `upstream.development.sha256`), verifies its SHA-256
before extracting, and packages that tree under the same namespace. The jar records
the pin it was built from in `META-INF/paste-upstream.properties`.

## Consuming

```xml
<repository>
  <id>paste-registry</id>
  <url>https://gitlab.com/api/v4/projects/70289607/packages/maven</url>
</repository>

<dependency>
  <groupId>com.pastestack</groupId>
  <artifactId>paste-webjar</artifactId>
  <version>2.1.0</version>
</dependency>
```

```scala
// build.sbt
resolvers += "paste-registry" at "https://gitlab.com/api/v4/projects/70289607/packages/maven"

libraryDependencies += "com.pastestack" % "paste-webjar" % "2.1.0"
```

Assets resolve at `/webjars/paste-webjar/{version}/...`.

## Versioning

`VERSION`, the pom's `<version>`, and the pom's `<upstreamVersion>` are one value: the
WebJar's version is the upstream version it wraps. CI refuses to build when they differ,
and refuses to publish a tag that does not match `VERSION`.

Tag pipelines run the release build and wrap the upstream release tag. Branch
pipelines activate `-Pdevelopment-upstream` instead: they wrap the pinned development
archive and publish under CI-assigned branch versions, so the resource namespace
always matches the published Maven version. The development pin is refreshed by
updating `upstream.development.version`, `upstream.development.url`, and
`upstream.development.sha256` together to a new immutable upstream archive; the base
version follows the repository's release flow; CI assigns development versions
with `versions:set` during publication.

## Building

```shell
mvn --settings ./settings.xml clean package
mvn --settings ./settings.xml -Pdevelopment-upstream clean package
```

`unzip` must be on the path — the release build extracts the downloaded upstream
archive with it.

Publishing is CI's job. To deploy by hand, supply the registry credentials the
`settings.xml` server entry reads and run the deploy:

```shell
export GL_USERNAME=<user> GL_PASSWORD=<token>
mvn --settings ./settings.xml deploy
```

## License

This repository's build files: Apache License, Version 2.0 (`LICENSE`, `NOTICE.md`).

The published jar contains only the packaged upstream tree, so its terms are that
tree's — Apache-2.0 for `paste`, both for the 2.1.0 release and for the pinned
development archive, as `pom.xml` declares. The upstream `LICENSE` travels inside
the jar.
