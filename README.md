<br>


**Apache Spark Scala Base**


<br>
<br>


* [Background](#background)
  * [A base image](#a-base-image)
  * [Registering the base image](#registering-the-base-image)
*From base image](#from-base-image)
* [Docker](#docker)
* [Submitting Applications](#submitting-applications)


<br>
<br>


## Background

Apache Spark Scala projects depend on

* POM (Project Object Model)
  * [Repositories for POM (Project Object Model)](https://mvnrepository.com/repos)
  * [Project Object Model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)

* [OpenJDK by Eclipse Temurin](https://hub.docker.com/_/eclipse-temurin)
  * Example: [Java 17 Releases](https://hub.docker.com/_/eclipse-temurin/tags?page=1&name=17)
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

Herein, an apache spark scala image is built via

```shell
docker build . --file .devcontainer/Dockerfile --tag {tag.name}
```

Afterwards, the list of images should include an image named `tag.name`

```shell
# Listing docker images
docker images
```

Subsequently, a container/instance of the image `tag.name` may be used as a development environment via the commands

```shell
docker run --rm -i -t -p 127.0.0.1:10000:8888 -w /app \
  --mount type=bind,src="$(pwd)",target=/app {tag.name}
```

whereby

* [--rm](https://docs.docker.com/engine/reference/commandline/run/#:~:text=a%20container%20exits-,%2D%2Drm,-Automatically%20remove%20the): Automatically remove container on exit ...
* [-i](https://docs.docker.com/engine/reference/commandline/run/#:~:text=and%20reaps%20processes-,%2D%2Dinteractive,-%2C%20%2Di): Interactive mode.
* [-p](https://docs.docker.com/engine/reference/commandline/run/#:~:text=%2D%2Dpublish%20%2C-,%2Dp,-Publish%20a%20container%E2%80%99s): Maps the host port 10000 to the container port 8888.

The docker pages discuss the [--mount](https://docs.docker.com/build/guide/mounts/) flag in detail.

<br>

### Registering the base image

Upcoming Notes:

- [ ] Docker Hub registration via GitHub Actions

<br>

### FROM Base Image

Upcoming Notes:

- [ ] A remote development environment FROM base image
- [ ] The production image FROM base image.


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
