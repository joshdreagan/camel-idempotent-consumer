# camel-idempotent-consumer

An example project showing how to do idempotent consumption in Camel as a viable replacement for XA transactions.

## Requirements

- [Apache Maven 3.x](http://maven.apache.org)
- [MySQL 5.7.18](https://www.mysql.com/oem/)
  - [Docker Image](https://hub.docker.com/r/mysql/mysql-server/)

## Preparing

Install and run MySQL [https://dev.mysql.com/doc/refman/5.7/en/installing.html]

_Note: For my tests, I chose to run the docker image [https://hub.docker.com/r/mysql/mysql-server/]. You can run it using the command `docker run --name mysql -e MYSQL_DATABASE=example -e MYSQL_ROOT_PASSWORD=Abcd1234 -e MYSQL_ROOT_HOST=172.17.0.1 -p 3306:3306 -d mysql/mysql-server:5.7`. You can then connect and run SQL statements using the command `docker exec -it mysql mysql -uroot -p`._

Build the project source code

```
$ cd $PROJECT_ROOT
$ mvn clean install
```

## Running the example standalone

```
$ cd $PROJECT_ROOT
$ mvn spring-boot:run
```

## Testing the code

There are a couple of test files in the `src/test/data` folder. You can drop them in the `target/messages` folder to kick off the route.

```
$ cd $PROJECT_ROOT
$ cp src/test/data/message_01.txt target/messages/
```

If the file successfully processed, you will see the message in the DB only once. You can check it using the SQL command `select * from example.MESSAGES;`. You will also see a single copy in the `target/processed` folder.
