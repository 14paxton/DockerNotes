# Use Java 7, SDKMAN, and Tomcat to build and run Grails app in a Dockerfile

  <a href="https://gist.github.com/14paxton/c9fba71cd90ec3716974a48e386b3e1f"> Docker File for building Grails 2.0.3 app </a>

# Partial Code example for building Grails app and running in docker container

https://github.com/14paxton/run_grails_in_docker_container

# MySQL

```shell
docker pull mysql
```

## Run Container

```shell
docker run --detach --name=jspmysql --env="MYSQL_ROOT_PASSWORD=jsppassword" --publish 6603:3306 mysql
```

### Exposing MySQL Container to Host

> Expose the MySQL container to the outside world by mapping the container’s MySQL port to the host machine port using the publish flag. Now, we can connect to the MySQL container through port 6703.
> Notice, the IP address comes from docker machine. For my docker machine, it is 192.168.99.100.

```shell
 docker rm -f jspmysql
 docker run --detach --name=jspmysql --env="MYSQL_ROOT_PASSWORD=jsppassword" --publish 6703:3306 mysql
```

## Creating MySQL Image

```shell
 docker run --detach --name=jspmysql --env="MYSQL_ROOT_PASSWORD=jsppassword" --publish 6603:3306 mysql
```

> What is this command doing?

Create a MySQL container named jspmysql.
Set environment variable MYSQL_ROOT_PASSWORD to jsppassword.
Expose 3306 and map to 6603 for outside world to connect to this MySQL database.
In addition, we manually created database jsptutorial and table Product.

``` mysqladmin -u root -p create jsptutorial```
``` mysql -u root -p jsptutorial < jsp_backup.sql```

In this posting, we will use Dockerfile to simplify the way how to create MySQL container for our JSP Tutorial application.

### Creating MySQL Image with Dockerfile

### Creating Docker File

Create one file named Dockerfile in any directory on local machine.

``` cd ~/Johnny```
``` mkdir DockerMySQL```
``` cd DockerMySQL```
``` vim Dockerfile```

Edit Dockerfile, fill with following content.

### Create MySQL Image for JSP Tutorial Application

```
FROM mysql
MAINTAINER csgeek@mail.com

ENV MYSQL_ROOT_PASSWORD jsppassword
ADD jsp_backup.sql /docker-entrypoint-initdb.d

EXPOSE 3306
```

The following points need to be noted about the above file.

- The first line is a comment. You can add comments to the Docker File with the help of the # command
- The FROM keyword tells which base image you want to use. In our example, we are creating an image from the mysql image.
- The next command is the person who is going to maintain this image.
- The ENV command is used to set environment variable. We set MYSQL_ROOT_PASSWORD to jsppassword for MySQL database.
- The ADD command copy the database backup file to /docker-entrypoint-initdb.d directory in the Docker container. The docker-entrypoint.sh file will run any files in this directory ending with “.sql”
  against the MySQL database. In our example, we have only one sql script file jsp_backup.sql.
- The EXPOSE command exposes port 3306 of the image.

### Creating Image with Dockerfile

Open Docker terminal, navigate to the folder where the Dockerfile and MySQL backup file locates. Run the following command.

``` docker build -t jspmysql:0.1 .```
