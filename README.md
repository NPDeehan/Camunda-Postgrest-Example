# Camunda Spring Boot Application
Spring Boot Application using [Camunda](http://docs.camunda.org).

This is a simple example which shows how you can connect Camunda to a postgres database.


## How does it work?

### Runing a Postgres Database
If you don't already have a postgres database up and running you do so by [installing docker](https://docs.docker.com/get-docker/) and using the `docker-compose.yml` file in the `resources` folder.

To start the database simple navegate to the directory 
``../src/main/resources`` and run `docker-compose up` 

That will download a postgres image from docker hub and start it up. Once it's finished you'll have a postgres database with the following settings:

```yaml
 environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
    ports:
      - 5432:5432
```

### Connecting Camunda to the Database

Connecting the database involves two changes, firstly you have to define the datasource in the `application.yaml` file. 
```yaml
spring.datasource:
   type: org.postgresql.ds.PGSimpleDataSource
   username: postgres
   password: postgres
   url: jdbc:postgresql://localhost:5432/postgres
```
Then you should get the driver by adding this dependency to your `pom.xml`

```XML
<dependency>
	<groupId>org.postgresql</groupId>
	<artifactId>postgresql</artifactId>
</dependency>
```

### Running the application
You can also build and run the process application with Spring Boot.

#### Manually
1. Build the application using:

```bash
mvn clean package
```
2. Run the *.jar file from the `target` directory using:

```bash
java -jar target/Camunda-Postgrest-Example.jar
```

For a faster 1-click (re-)deployment see the alternatives below.

#### Maven Spring Boot Plugin
1. Build and deploy the process application using:

```bash
mvn clean package spring-boot:run
```

#### Your Java IDE
1. Run the project as a Java application in your IDE using CamundaApplication as the main class.

### Run and Inspect with Tasklist and Cockpit
Once you deployed the application you can run it using
[Camunda Tasklist](http://docs.camunda.org/latest/guides/user-guide/#tasklist)
and inspect it using
[Camunda Cockpit](http://docs.camunda.org/latest/guides/user-guide/#cockpit).

## Environment Restrictions
Built and tested against Camunda Platform version 7.15.0.

## License
[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

<!-- Tweet
New @Camunda example: Camunda Spring Boot Application - Spring Boot Application using [Camunda](http://docs.camunda.org). https://github.com/camunda-consulting/code/tree/master/snippets/Camunda-Postgrest-Example
-->
