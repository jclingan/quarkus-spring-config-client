# Quarkus Spring Cloud Config Client

This project uses Spring Cloud Config Server as a Quarkus configuration property source. This example will require 3 terminals -
one to run config server, one to run config client, and one to run curl (or use browser instead)

## Create a local git repo
Update spring.cloud.config.server.git.uri property in config-server/src/main/resources/application.properties if a different location is used.

```
mkdir ${HOME}/configrepo
cd ${HOME}/configrepo
git init
echo "message=world" > quarkus-client.properties
git add quarkus-client.properties
git commit -m "Initial revision"
```

## Build and run the Spring Config Server

```
cd config-server
mvn clean package
java -jar target/config-server-0.0.1-SNAPSHOT.jar
```

Verify endpoint:
```
curl localhost:8888/quarkus-client/default
```
_{"name":"quarkus-client","profiles":["default"],"label":null,"version":"e12042adead2db55ff3502a12bf45d2c245b522f","state":null,"propertySources":[{"name":"/Users/jclingan/configrepo//quarkus-client.properties","source":{"message":"world"}}]}_

## Build and run Quarkus Client

### JVM

```
cd quarkus-client
mvn clean package
java -jar target/quarkus-client-1.0-SNAPSHOT-runner.jar
```

### Native binary (requires GraalVM)
```
cd quarkus-client
mvn clean package -Pnative
target/quarkus-client-1.0-SNAPSHOT-runner
```

Verify endpoint:
```
curl localhost:8080/greeting
```
_Hello world_