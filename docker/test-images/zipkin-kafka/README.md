## zipkin-kafka Docker image

The `zipkin-kafka` testing image runs both Kafka+ZooKeeper for the [Kafka collector](../../../zipkin-collector/kafka)
and the upcoming [Kafka storage](https://github.com/openzipkin-contrib/zipkin-storage-kafka).

Besides norms defined in [docker-java](https://github.com/openzipkin/docker-java), this accepts the
following environment variables:

 * `LOGGING_LEVEL`: Root Log4J logging level sent to stdout. Defaults to "WARN"


To build `openzipkin/zipkin-kafka:test`, from the top-level of the repository, run:
```bash
$ DOCKER_FILE=docker/test-images/zipkin-kafka/Dockerfile build-bin/docker/docker_build openzipkin/zipkin-kafka:test
```

Then configure the [Kafka sender](https://github.com/openzipkin/zipkin-reporter-java/blob/master/kafka/src/main/java/zipkin2/reporter/kafka/KafkaSender.java) using a `bootstrapServers` value of `host.docker.internal:9092` if your application is inside the same docker network or `localhost:19092` if not, but running on the same host.

In other words, if you are running a sample application on your laptop, you would use `localhost:19092` bootstrap server to send spans to the Kafka broker running in Docker.
