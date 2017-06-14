# Maven Cache Resource [![Build Status](https://travis-ci.org/olhtbr/maven-cache-resource.svg?branch=master)](https://travis-ci.org/olhtbr/maven-cache-resource)
A [Concourse.ci](http://concourse.ci/) resource for caching Maven dependencies.

The approach and code is based on [gradle-cache-resource](https://github.com/projectfalcon/gradle-cache-resource).

## Source Configuration
The resource uses the [git-resource](https://github.com/concourse/git-resource) internally, so any of
the git-resource parameters can be used. It is advisable to use the `paths` parameter to only listen
to changes of the `pom.xml` of the Maven project.

Additionally, the following Maven specific configuration is supported.

- `settings.url`: *Optional*. A URL, which points to a custom Maven `settings.xml` file.
- `master-password`: *Optional*. An encrypted Maven master password, which is written to the [`settings-security.xml`](https://maven.apache.org/guides/mini/guide-encryption.html) file by the resource.

## Behavior
### `check`: Check for git repo changes
Simply forwards the control to the `check` script of the git-resource to check for any changes in
the source repository.

It is advisable to track changes to the `pom.xml` only, since that describes the project dependencies.

### `in`: Cache dependencies
The source repository is first cloned using the git-resource and then dependencies are cached
with `mvn dependency:go-offline`.

### `out`: Not used

## Usage
An example usage is documented in `example-pipeline.yml`.

Docker image is available on [Docker Hub](https://hub.docker.com/r/olhtbr/maven-cache-resource).
