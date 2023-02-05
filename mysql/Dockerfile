FROM mysql:5.7

ENV MYSQL_ROOT_PASSWORD=Admin0101

COPY setup.sql /docker-entrypoint-initdb.d/

EXPOSE 3306
CMD ["mysqld"]
