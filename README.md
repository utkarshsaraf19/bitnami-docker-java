# Java packaged by Bitnami

## What is Java?

> Java is a general-purpose computer programming language that is concurrent, class-based, object-oriented, and specifically designed to have as few implementation dependencies as possible.

[Overview of Java](https://openjdk.java.net/)

Trademarks: This software listing is packaged by Bitnami. The respective trademarks mentioned in the offering are owned by the respective companies, and use of them does not imply any affiliation or endorsement.

## TL;DR

```console
$ docker run -it --name java bitnami/java
```

### Docker Compose

```console
$ curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-java/master/docker-compose.yml > docker-compose.yml
$ docker-compose up -d
```

## Why use Bitnami Images?

* Bitnami closely tracks upstream source changes and promptly publishes new versions of this image using our automated systems.
* With Bitnami images the latest bug fixes and features are available as soon as possible.
* Bitnami containers, virtual machines and cloud images use the same components and configuration approach - making it easy to switch between formats based on your project needs.
* All our images are based on [minideb](https://github.com/bitnami/minideb) a minimalist Debian based container image which gives you a small base container image and the familiarity of a leading Linux distribution.
* All Bitnami images available in Docker Hub are signed with [Docker Content Trust (DCT)](https://docs.docker.com/engine/security/trust/content_trust/). You can use `DOCKER_CONTENT_TRUST=1` to verify the integrity of the images.
* Bitnami container images are released daily with the latest distribution packages available.

## Supported tags and respective `Dockerfile` links

Learn more about the Bitnami tagging policy and the difference between rolling tags and immutable tags [in our documentation page](https://docs.bitnami.com/tutorials/understand-rolling-tags-containers/).


* [`17`, `17-debian-10`, `17.0.3`, `17.0.3-debian-10-r23`, `latest` (17/debian-10/Dockerfile)](https://github.com/bitnami/bitnami-docker-java/blob/17.0.3-debian-10-r23/17/debian-10/Dockerfile)
* [`11`, `11-debian-10`, `11.0.15`, `11.0.15-debian-10-r24` (11/debian-10/Dockerfile)](https://github.com/bitnami/bitnami-docker-java/blob/11.0.15-debian-10-r24/11/debian-10/Dockerfile)
* [`1.8`, `1.8-debian-10`, `1.8.332`, `1.8.332-debian-10-r24` (1.8/debian-10/Dockerfile)](https://github.com/bitnami/bitnami-docker-java/blob/1.8.332-debian-10-r24/1.8/debian-10/Dockerfile)

Subscribe to project updates by watching the [bitnami/java GitHub repo](https://github.com/bitnami/bitnami-docker-java).

### Deprecation Note (2022-01-21)

The `prod` tags has been removed; from now on just the regular container images will be released.

### Deprecation Note (2020-08-18)

The formatting convention for `prod` tags has been changed:

* `BRANCH-debian-10-prod` is now tagged as `BRANCH-prod-debian-10`
* `VERSION-debian-10-rX-prod` is now tagged as `VERSION-prod-debian-10-rX`
* `latest-prod` is now deprecated

## Get this image

The recommended way to get the Bitnami Java Docker Image is to pull the prebuilt image from the [Docker Hub Registry](https://hub.docker.com/r/bitnami/java).

```console
$ docker pull bitnami/java:latest
```

To use a specific version, you can pull a versioned tag. You can view the [list of available versions](https://hub.docker.com/r/bitnami/java/tags/) in the Docker Hub Registry.

```console
$ docker pull bitnami/java:[TAG]
```

If you wish, you can also build the image yourself.

```console
$ docker build -t bitnami/java 'https://github.com/bitnami/bitnami-docker-java.git#master:17/debian-10'
```

## Configuration

### Running your Java jar or war

The default work directory for the Java image is `/app`. You can mount a folder from your host here that includes your Java jar or war, and run it normally using the `java` command.

```console
$ docker run -it --name java -v /path/to/app:/app bitnami/java:latest \
  java -jar package.jar
```

or using Docker Compose:

```yaml
java:
  image: bitnami/java:latest
  command: "java -jar package.jar"
  volumes:
    - .:/app
```

**Further Reading:**

  - [Java SE Documentation](https://docs.oracle.com/javase/8/docs/api/)

## Replace the default truststore using a custom base image

In case you are replacing the default [minideb](https://github.com/bitnami/minideb) base image with a custom base image (based on Debian), it is possible to replace the default truststore located in the `/opt/bitnami/java/lib/security` folder. This is done by setting the `JAVA_EXTRA_SECURITY_DIR` docker build ARG variable, which needs to point to a location that contains a *cacerts* file that would substitute the originally bundled truststore. In the following example we will use a minideb fork that contains a custom *cacerts* file in the */bitnami/java/extra-security* folder:

- In the Dockerfile, replace `FROM docker.io/bitnami/minideb:buster` to use a custom image, defined with the `MYJAVAFORK:TAG` placeholder:

```diff
- FROM bitnami/minideb:latest
+ FROM MYFORK:TAG
```

- Run `docker build` setting the value of `JAVA_EXTRA_SECURITY_DIR`. Remember to replace the `MYJAVAFORK:TAG` placeholder.

```
docker build --build-arg JAVA_EXTRA_SECURITY_DIR=/bitnami/java/extra-security -t MYJAVAFORK:TAG .
```

## Maintenance

### Upgrade this image

Bitnami provides up-to-date versions of Java, including security patches, soon after they are made upstream. We recommend that you follow these steps to upgrade your container.

#### Step 1: Get the updated image

```console
$ docker pull bitnami/java:latest
```

or if you're using Docker Compose, update the value of the image property to `bitnami/java:latest`.

#### Step 2: Remove the currently running container

```console
$ docker rm -v java
```

or using Docker Compose:

```console
$ docker-compose rm -v java
```

#### Step 3: Run the new image

Re-create your container from the new image.

```console
$ docker run --name java bitnami/java:latest
```

or using Docker Compose:

```console
$ docker-compose up java
```

## Notable Changes

### 1.8.252-debian-10-r0, 11.0.7-debian-10-r7, and 15.0.1-debian-10-r20

- Java distribution has been migrated from AdoptOpenJDK to OpenJDK Liberica. As part of VMware, we have an agreement with Bell Software to distribute the Liberica distribution of OpenJDK. That way, we can provide support & the latest versions and security releases for Java.

## Contributing

We'd love for you to contribute to this Docker image. You can request new features by creating an [issue](https://github.com/bitnami/bitnami-docker-java/issues), or submit a [pull request](https://github.com/bitnami/bitnami-docker-java/pulls) with your contribution.

## Issues

If you encountered a problem running this container, you can file an [issue](https://github.com/bitnami/bitnami-docker-java/issues/new). For us to provide better support, be sure to include the following information in your issue:

- Host OS and version
- Docker version (`docker version`)
- Output of `docker info`
- Version of this container
- The command you used to run the container, and any relevant output you saw (masking any sensitive
information)

## License

Copyright &copy; 2022 Bitnami

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
