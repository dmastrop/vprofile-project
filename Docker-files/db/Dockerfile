# this will be a mysql image and we will copy the db_backup.sql file into this image
# then build the image with this .sql file
# Tag is 8.0.33
FROM mysql:8.0.33

LABEL "Project"="Vprofile"
LABEL "Author"="dmastrop"

ENV MYSQL_ROOT_PASSWORD="vproddbpass"
# set the password with ENV; this password will be overwritten when we actually run the container
ENV MYSQL_DATABASE="accounts"

ADD db_backup.sql docker-entrypoint-initdb.d/db_backup.sql
# note this file is in the same directory as the Dockerfile on local workspace
# deploy the db_backup.sql into this mysql image that we are building.
# The instance will run the file. This file has mysql queries.
# https://hub.docker.com/_/mysql
# "Furthermore, it will execute files with extensions .sh, .sql and .sql.gz that are found 
# in /docker-entrypoint-initdb.d."
# We need to copy the db_backup.sql local workspace file into this directory on the docker container (build)

# the EXPOSE 3306 is implicit
