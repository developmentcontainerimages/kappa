<br>

**Apache Spark Scala Base**

<br>

### Apache Spark Notes

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

### Docker

The development container is built via

```shell
docker build . --file .devcontainer/Dockerfile --tag kappa
```

Afterwards, the list of images should include an image named `kappa`

```shell
# Listing docker images
docker images
```

Subsequently, a container/instance of the image `kappa` may be used as a development environment via the commands

```shell
docker run --rm -i -t -p 127.0.0.1:10000:8888 -w /app --mount type=bind,src="$(pwd)",target=/app kappa
```

whereby

* [--rm](https://docs.docker.com/engine/reference/commandline/run/#:~:text=a%20container%20exits-,%2D%2Drm,-Automatically%20remove%20the): Automatically remove container on exit ...
* [-i](https://docs.docker.com/engine/reference/commandline/run/#:~:text=and%20reaps%20processes-,%2D%2Dinteractive,-%2C%20%2Di): Interactive mode.
* [-p](https://docs.docker.com/engine/reference/commandline/run/#:~:text=%2D%2Dpublish%20%2C-,%2Dp,-Publish%20a%20container%E2%80%99s): Maps the host port 10000 to the container port 8888.

The docker pages discuss the [--mount](https://docs.docker.com/build/guide/mounts/) flag in detail.


<br>

### Development Environment Notes

Apache Spark Scala projects depend on

* POM (Project Object Model)
  * [Repositories for POM (Project Object Model)](https://mvnrepository.com/repos)
  * [Project Object Model](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)

* [OpenJDK](https://hub.docker.com/_/openjdk)
  * [19](https://hub.docker.com/layers/library/openjdk/19-rc/images/sha256-973fe414a4e1f3e41e291b068183684a88827dd2cb5f78214da26632d5218702?context=explore)

* [Scala](https://scala-lang.org)
  * [2.13.12](https://scala-lang.org/download/2.13.12.html)

* [Apache Maven](https://maven.apache.org)
  * [3.9.6](https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/)

* [Hadoop](https://hadoop.apache.org)
  * [3.3.6](https://dlcdn.apache.org/hadoop/common/hadoop-3.3.6/)

* [Apache Spark](https://spark.apache.org)
  * [3.4.2](https://dlcdn.apache.org/spark/spark-3.4.2/)

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

<br>
<br>

<br>
<br>

<br>
<br>
