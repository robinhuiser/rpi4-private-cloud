# Uptrace

Understand how [Uptrace](https://uptrace.dev/) works:

* Spin up Uptrace locally in Docker
* Example Java app
* Example Golang app

## Spin up Uptrace

~~~bash
# Start the services with Docker
$ docker-compose pull
$ docker-compose up -d

# Make sure uptrace is running
$ docker-compose logs uptrace
~~~

* Open Uptrace UI at [http://localhost:14318](http://localhost:14318)
* View notifications at [http://localhost:8025](http://localhost:8025)
* View alerts at [http://localhost:9093](http://localhost:9093)

## Example Java app

Clone, build & run instructions [here](./java-example/README.md).

## Example Golang app

Build & run instructions [here](./golang-example/README.md).