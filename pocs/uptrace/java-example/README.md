# Uptrace for Java example

The [Realworld example app](https://github.com/gothinkster/spring-boot-realworld-example-app) is used to demonstrate the observability capabilities OOTB by attaching an OpenTelemtry Java Agent.

## Java Agent

~~~bash
# Download the OpenTelemetry agent
$ wget https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent.jar
~~~

## Backend App

First, clone the reference backend app:

~~~bash
$ git clone https://github.com/gothinkster/spring-boot-realworld-example-app.git
~~~

Next, add the following snippet to the `spring-boot-realworld-example-app/build.gradle`; this will update the JVM arguments so the OpenTelemetry Agent is attached during startup:

~~~json
bootRun { 
    jvmArgs = ["-javaagent:$rootDir/../opentelemetry-javaagent.jar"] 
}
~~~

Next, set the environment variables so the OpenTelemetry agent can connect with Uptrace:

~~~bash
export OTEL_TRACES_EXPORTER=otlp
export OTEL_METRICS_EXPORTER=otlp
export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4317
export OTEL_EXPORTER_OTLP_HEADERS=uptrace-dsn=http://project2_secret_token@localhost:14317/2
export OTEL_RESOURCE_ATTRIBUTES=service.name=my-java-service,service.version=1.0.0
~~~

Start the backend application:

~~~bash
$ cd spring-boot-realworld-example-app
$ ./gradlew bootRun
~~~

Last, test if the backend application is up:

~~~bash
$ curl http://localhost:8080/tags
~~~

## Frontend App

First, clone the reference frontend app:

~~~bash
$ git clone https://github.com/gothinkster/react-redux-realworld-example-app.git
~~~

The app comes with many dependencies, let's download these:

~~~bash
$ cd react-redux-realworld-example-app
$ npm install
~~~

Now we need to configure the frontend app to use our backend that is running at `http://localhost:8080/`. You can do that by editing `src/agent.js` file:

~~~js
const API_ROOT = 'http://localhost:8080'
~~~

After which we can start the React app and enjoy the UI at [http://localhost:4100/register](http://localhost:4100/register):

~~~bash
$ npm start
~~~
