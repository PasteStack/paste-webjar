# paste-webjar

WebJar packaging for the PasteStack core JavaScript utilities. The build downloads the
upstream `paste` archive named by the `upstreamVersion` property in `pom.xml` and
repackages its sources under `META-INF/resources/webjars/paste-webjar/{upstreamVersion}/`,
so a JVM application can serve them without a separate asset checkout.

## Consuming

```xml
<repository>
  <id>paste-registry</id>
  <url>https://gitlab.com/api/v4/projects/70289607/packages/maven</url>
</repository>

<dependency>
  <groupId>com.pastestack</groupId>
  <artifactId>paste-webjar</artifactId>
  <version>2.0.1</version>
</dependency>
```

```scala
// build.sbt
resolvers += "paste-registry" at "https://gitlab.com/api/v4/projects/70289607/packages/maven"

libraryDependencies += "com.pastestack" % "paste-webjar" % "2.0.1"
```

Assets resolve at `/webjars/paste-webjar/{upstreamVersion}/...`.

## Versioning

`VERSION`, the pom's `<version>`, and the pom's `<upstreamVersion>` are one value: the
WebJar's version is the upstream version it wraps. CI refuses to build when they differ,
and refuses to publish a tag that does not match `VERSION`.

## Building

```shell
mvn --settings ./settings.xml clean package
```

`unzip` must be on the path — the build extracts the downloaded upstream archive with it.

Publishing is CI's job. To deploy by hand, supply the registry credentials the
`settings.xml` server entry reads and run the deploy:

```shell
export GL_USERNAME=<user> GL_PASSWORD=<token>
mvn --settings ./settings.xml deploy
```

## License

This repository's build files: Apache License, Version 2.0 (`LICENSE`, `NOTICE.md`).

The published jar contains only the packaged `upstreamVersion`, so its terms are that
version's — Apache-2.0 for `paste` 2.0.1, as `pom.xml` declares. The upstream `LICENSE`
travels inside the jar.
