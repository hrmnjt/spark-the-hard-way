# Packaging Scala (Spark) application

In order to run the Scala application, it needs to be packaged. Spark
applications are generally submitted to Spark using `spark-submit` which as
well requires application to be packaged. Depending on requirements project
could be packaged in multiple ways (highlighted below)

## Packaging application into fat Jar

TBD

## Packaging application as Docker images (local)

Packaging and publishing Scala applications to Docker can be done using
`sbt-native-packager` library which enabled different ways of packaging and
publishing in native formats.
[Documentation](https://sbt-native-packager.readthedocs.io/en/stable/).
[Repository](https://github.com/sbt/sbt-native-packager).

Add a new file or add to existing `project/plugins.sbt` the below line to enable
the autoplugins

```scala
addSbtPlugin("com.github.sbt" % "sbt-native-packager" % "1.9.4")
```

Enable the plugin in `build.sbt` by adding the as below

```scala
lazy val root = (project in file("."))
  .enablePlugins(JavaAppPackaging)
  .enablePlugins(DockerPlugin)
  .settings(
    name := "spark-the-hard-way",
    libraryDependencies += scalaTest % Test
  )
```

Post this, to publish the Scala application as Docker image on local Docker
server, we may use the below sbt command

```bash
sbt docker:publishLocal
# ...
# [info] Successfully tagged spark-the-hard-way:0.1.0-SNAPSHOT
# [info] Built image spark-the-hard-way:0.1.0-SNAPSHOT
```

Post successful completion, to run the project as docker container, we may
run as below

```bash
docker run --rm spark-the-hard-way:0.1.0-SNAPSHOT
# hello
```
