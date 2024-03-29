<br>


**Apache Spark Scala Base**


<br>
<br>


* [Background](#background)
* [Docker](#docker)
  * [A base image](#a-base-image)
  * [Registering the base image](#registering-the-base-image)
  * [Remote Development](#remote-development)
  * [Production States](#production-states)
* [Submitting Applications](#submitting-applications)


<br>
<br>


## Background

Apache Spark Scala projects depend on

* POM (Project Object Model)
  * [Repositories for POM (Project Object Model)](https://mvnrepository.com/repos)
  * [Project Object Model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)

* [OpenJDK by Eclipse Temurin](https://hub.docker.com/_/eclipse-temurin)
  * Example: [Java Development Kit (JDK)](https://hub.docker.com/_/eclipse-temurin/tags?page=1&name=jdk)
  * The openjdk.org images [OpenJDK](https://hub.docker.com/_/openjdk) are under deprecation.

* [Scala](https://scala-lang.org)
  * [Releases](https://scala-lang.org/download/all.html)

* [Apache Maven](https://maven.apache.org)
  * [Releases 3](https://dlcdn.apache.org/maven/maven-3/)

* [Hadoop](https://hadoop.apache.org)
  * [Releases](https://dlcdn.apache.org/hadoop/common/)

* [Apache Spark](https://spark.apache.org)
  * [Releases](https://dlcdn.apache.org/spark/)

<br>

Outline the software versions via

> ```shell
> java -version
> scala -version
> mvn --version
> hadoop version
> spark-submit --version
> ```


<br>
<br>


## Docker

### A base image

Herein, a base apache spark scala image is built via

```shell
docker build . --file .base/Dockerfile --tag {registry.name/repository.name:image.tag}
```

within a GitHub container.  The build script is within the GitHub Actions workflow file [main.yml](.github/workflows/main.yml).

<br>

### Registering the base image

The GitHub Actions workflow file [main.yml](.github/workflows/main.yml) includes Docker Hub registration instructions, i.e., the image built via GitHub is registered within Docker Hub for public use.

<br>

### Remote Development

Hence, to use the registered image for remote development, i.e., development via a container, run the command

```shell
docker pull {registry.name/repository.name:image.tag}
```

Subsequently, a container/instance of the image `tag.name` may be used as a development environment via the commands

```shell
docker run --rm -i -t -p 127.0.0.1:10000:8888 -w /app \
  --mount type=bind,src="$(pwd)",target=/app {registry.name/repository.name:image.tag}
```

whereby

* [--rm](https://docs.docker.com/engine/reference/commandline/run/#:~:text=a%20container%20exits-,%2D%2Drm,-Automatically%20remove%20the): Automatically remove container on exit ...
* [-i](https://docs.docker.com/engine/reference/commandline/run/#:~:text=and%20reaps%20processes-,%2D%2Dinteractive,-%2C%20%2Di): Interactive mode.
* [-p](https://docs.docker.com/engine/reference/commandline/run/#:~:text=%2D%2Dpublish%20%2C-,%2Dp,-Publish%20a%20container%E2%80%99s): Maps the host port 10000 to the container port 8888.

The docker pages discuss the [--mount](https://docs.docker.com/build/guide/mounts/) flag in detail.


<br>

### Production States

Upcoming:
- [ ] The production image


<br>
<br>


## Submitting Applications

Remember, for local exploration of apache spark scala executions via the interface you will need the commands

```bash
    spark-class.cmd org.apache.spark.deploy.master.Master
    spark-class.cmd org.apache.spark.deploy.worker.Worker spark://___.___._.__:7077
    mvn clean package
```

```shell
    spark-submit --class com.grey...App 
        --master spark://___.___._.__:7077 
        --total-executor-cores 4 
        target/...-#.#.##-jar-with-dependencies.jars
```

wherein `#.#.##` is the build number; depending on <span title='Project Object Model'>POM</span> settings, each run of `mvn clean package` creates a string of the form `...-#.#.##-jar-with-dependencies.jars`.


<br>
<br>

<br>
<br>

<br>
<br>

<br>
<br>
