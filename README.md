## General info
This project aims to create a Dockerized multi-container environment consisting of various services for a Multi-tier web application. 
The goal is to streamline the deployment process, allowing for customization of specific services while leveraging existing Docker Hub images as base images.

## Resources
  - Docker
  - Ubuntu OS (supported by Docker)
  - Docker Compose

## Setup
* ## For Building Images
  The steps are as follows:
   - Dockerfiles for services requiring customization (e.g., TomCat, Nginx, MySQL) to incorporate specific configurations and artifacts.
   - The Nginx Dockerfile is customized to make sure the container acts as a server with an upstream configuration for port 80, with a forwarded route at the 8080 port of the Tomcat container.
   - With Tomcat, we create a multi-stage Dockerfile for memory optimization while building, testing, and copying the built artifact (.war) as /usr/local/tomcat/webapps/ROOT.war so that the application server can serve our application at port 8080.
   - The MYSQL container is written with keeping MYSQL_ROOT_PASSWORD and MYSQL_DATABASE populated with our custom entries while using ```docker ADD``` to place our mysql dump (db_backup.sql) at /docker-entrypoint-initdb.d for initial instantiation.
   - The RabbitMQ and Memcached containers are initialized using Docker official images from DockerHub using ```docker pull``` with environment variable exported to customize RABBITMQ_DEFAULT_USER and RABBITMQ_DEFAULT_PASS.  

* ## For Running the containers
  A Docker-Compose file is used to orchestrate the simultaneous and parallel execution of the containers.

After proper testing of the containerized application, we push the customized images to Dockerhub.
The images can be found at [Tomcat](https://hub.docker.com/repository/docker/ardhendushekhar/vprofileapp/general), [Nginx](https://hub.docker.com/repository/docker/ardhendushekhar/vprofileweb/general) and [MYSQL](https://hub.docker.com/repository/docker/ardhendushekhar/vprofiledb/general).
