.EXPORT_ALL_VARIABLES:
OTEL_TRACES_EXPORTER=otlp
OTEL_METRICS_EXPORTER=otlp
OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4317
OTEL_EXPORTER_OTLP_HEADERS=uptrace-dsn=http://project2_secret_token@localhost:14317/2
OTEL_RESOURCE_ATTRIBUTES=service.name=my-java-service,service.version=1.0.0
# OTEL_JAVAAGENT_ENABLED=true

.SILENT:
agent:
	[ ! -f ./opentelemetry-javaagent.jar ] \
		&& wget https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent.jar \
		|| exit 0

backend-clone:
	[ ! -d ./spring-boot-realworld-example-app ] \
		&& git clone https://github.com/gothinkster/spring-boot-realworld-example-app.git \
		|| exit 0
	# [[ `grep  "opentelemetry-javaagent" ./spring-boot-realworld-example-app/build.gradle` ]] \
	# 	|| echo 'bootRun { jvmArgs = ["-javaagent:$$rootDir/../opentelemetry-javaagent.jar"] }' >> ./spring-boot-realworld-example-app/build.gradle \
	# 	&& exit 0

backend-run:
	cd ./spring-boot-realworld-example-app && ./gradlew bootRun

frontend-clone:
	[ ! -d ./react-redux-realworld-example-app ] \
		&& git clone https://github.com/gothinkster/react-redux-realworld-example-app.git \
		|| exit 0	

frontend-run:
	cd ./react-redux-realworld-example-app && npm install && npm start