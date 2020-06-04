# Quarkus Spring Boot Client

This project uses Spring Config Server as a Quarkus configuration property source. This example will require 2 terminals.

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
_{"name":"quarkus-client","profiles":["default"],"label":null,"version":"a0d265595bfe822efcad0c4c68593b47e882ae45","state":null,"propertySources":[{"name":"file://Users/jclingan/working/quarkus/springconfig/localrepo//quarkus-client.properties","source":{"message":"world"}}]}_

## Build and run quarkus-client
```
cd quarkus-client
mvn clean package
java -jar target/quarkus-client-1.0-SNAPSHOT-runner.jar
```

Verify endpoint:
```
curl localhost:8080/greeting
```
_Hello world_