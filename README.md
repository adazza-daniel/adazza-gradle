# adazza-gradle
Collection of easy to reference build scripts for Adazza gradle builds.

## Manually Publish Scala 2.11 and 2.12 Artifacts
### Background
Currently, all Adazza services are written, compiled, and published in
Scala 2.12.

However, Apache Spark only supports Scala 2.11 and some of our spark jobs
will need to make API calls, therefore, at minimum, we have a
need to compile our service api libraries in Scala 2.11.

What we do today is provide the ability to compile our services modules
entirely in both scala 2.11 and 2.12, instead of the ideal scenario of
compiling a service and all it's modules in 2.12 but only a service's
api module in 2.11. This is due a gradle limitation with Nebula Release
Plugin which does not allow for release and publishing of artifacts at
a subproject level.

## Passing Scala version to Gradle
When building and publishing artifacts (locally or to S3) for a specific
version of Scala. Use the gradle project property `-PscalaVersion=<version_number>`.

Example: `gradle snapshot build clean publishToLocalMaven -PscalaVersion=2.11`

Only Scala version 2.11 and 2.12 are currently support (exactly Scala
versions, ie. 2.11.11 or 2.12.1 are not to be used). All other values passed
to this project property are invalid and cause a failure in Gradle. If
no version is provided, the Scala 2.12 is used by default.