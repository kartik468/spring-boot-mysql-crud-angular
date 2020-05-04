
## start mysql
```
$ sudo systmectl start mysql
$ sudo systmectl stop mysql
$ sudo systmectl status mysql

- go to console
$ sudo mysql
```

### create db and table
```
mysql> CREATE DATABASE `users_database`;

mysql> CREATE TABLE `employees` (
  `id` int NOT NULL AUTO_INCREMENT,
  `first_name` varchar(45) DEFAULT NULL,
  `last_name` varchar(45) DEFAULT NULL,
  `email_address` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`id`)
);
```

- mysql server should be running with 'root' user and 'admin' as password because it is configured in that way in spring boot.

```
spring.datasource.url = jdbc:mysql://localhost:3306/users_database?useSSL=false
spring.datasource.username = root
spring.datasource.password = admin
```
---

## start tomcat
```
$ cd /opt/tomcat/latest/
$ bin/startup.sh; tail -f logs/catalina.out
```

### tomcat spring boot metrics
http://localhost:8080/springboot2-jpa-crud-example-0.0.1-SNAPSHOT/actuator/prometheus
http://localhost:8080/springboot2-jpa-crud-example-0.0.1-SNAPSHOT/actuator

http://localhost:8080/angular8-springboot-client/employees


### spring build war
```
mvn clean install -DskipTests 

rm -rf /opt/tomcat/latest/webapps/springboot2-jpa-crud-example-0.0.1-SNAPSHOT.war
rm -rf /opt/tomcat/latest/webapps/springboot2-jpa-crud-example-0.0.1-SNAPSHOT

cp -r /home/ubuntu/Desktop/kartik/GIT/spring-boot-mysql-crud-angular/springboot2-jpa-crud-example/target/springboot2-jpa-crud-example-0.0.1-SNAPSHOT.war /opt/tomcat/latest/webapps/
```

### UI
```
npm run build

rm -rf /opt/tomcat/latest/webapps/angular8-springboot-client

cp -r /home/ubuntu/Desktop/kartik/GIT/spring-boot-mysql-crud-angular/angular8-springboot-client/dist/angular8-springboot-client/ /opt/tomcat/latest/webapps/
```
---

## start mongodb
```
- sudo systemctl start mongod
- sudo systemctl status mongod

- create mongodb database
  - use apache-logs

- go to mongo console
- $ mongo
```

### commands
```
> show dbs;
> use fluentd-db;
> show collections;

//  to show all the records in the collection
> db.tomcat_access_logs.find();

// drop the collection
> db.tomcat_access_logs.drop();

```
---

## fluentd

- go to '/etc/td-agent'
- update td-agent.conf file to your needs
- start fluentd
  - $ sudo /etc/init.d/td-agent start

### fluentd metrics
http://localhost:24231/metrics

### fluentd path

Status
```
$ sudo /etc/init.d/td-agent start
$ sudo /etc/init.d/td-agent stop
$ sudo /etc/init.d/td-agent restart
$ sudo /etc/init.d/td-agent status
```

### see fluentd log
$ sudo tail -f /var/log/td-agent/td-agent.log 

---

### start alert manager
```
$ cd /home/ubuntu/Desktop/kartik/devopsPOC/alertmanager-0.20.0.linux-amd64
$ ./alertmanager
```

#### url
localhost:9093

---

## prometheus

### start

```
$ cd /home/ubuntu/Desktop/kartik/devopsPOC/prometheus-2.17.2.linux-amd64
$ ./prometheus
```

### link

http://localhost:9090

---

## grafana

### start
```
$ cd /home/ubuntu/Desktop/kartik/devopsPOC/grafana-6.7.2
$ bin/grafana-server
```

### url
localhost:3000

---