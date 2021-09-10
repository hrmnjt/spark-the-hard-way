# Setting up Scala Spark project structure

Starting with Spark project structure can be very confusing and in light of
lots of opinionated approaches (and absence of an unified guidelines compared
to other languages). Observing multiple open source projects and libraries, I
realized there is a pattern to Spark application structure which is not widely
spoken of.

A good Spark application structure must separate side-effects from core logic,
making it easier to test the logic independently. There must be a separation
of concerns in codebase improving modularity and ease of collaboration.

## Project Structure

TBD

## Setup steps

Initializing codebase using Scala Giter8 seed project. Choose the project name
when prompted e.g. in case of this project, `spark-the-hard-way`

```bash
sbt new scala/scala-seed.g8
```

This creates a seed Scala project which has structure as below
```bash
.
├── src
│   ├── main
│   │   └── scala
│   │       └── example
│   │           └── Hello.scala
│   └── test
│       └── scala
│           └── example
│               └── HelloSpec.scala
├── project
│   ├── Dependencies.scala
│   ├── build.properties
│   └── target
└── build.sbt
```

Initializing git to version source code

```bash
cd spark-the-hard-way
git init
git branch -m main
```

Update `.gitignore` to handle which files would be tracked by Git. Possible
`.gitignore` could be taken from
https://www.toptal.com/developers/gitignore/api/scala,spark,sbt,visualstudiocode,metals.

Change your organization and personalize the Scala application build by editing
below lines in `build.sbt`

```scala
ThisBuild / scalaVersion     := "2.13.6"
ThisBuild / version          := "0.1.0-SNAPSHOT"
ThisBuild / organization     := "dev.hrmnjt"
ThisBuild / organizationName := "hrmnjt"
```

With this change, we would need to change folder structure as well to create
application structure to enable `sbt` functionalities.

