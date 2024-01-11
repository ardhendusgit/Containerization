FROM mysql:8.0.33
LABEL "Author"="Ardhendu Shekhar"
LABEL "Project"="Vprofile-Containerization"

ENV MYSQL_ROOT_PASSWORD="vprodbpass"
ENV MYSQL_DATABASE="accounts"

ADD db_backup.sql /docker-entrypoint-initdb.d

EXPOSE 3306



