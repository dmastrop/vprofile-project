FROM openjdk:11 AS BUILD_IMAGE
# first image will be used to build the vprofile artifact .war file, etc....
# The name of this image is BUILD_IMAGE and will be referenced in tomcat state2 below.
# image tag is on jdk in dockerhub
RUN apt update && apt install maven -y
# this will install maven on this first docker build that has jdk.
#  this openjdk is debian  so apt is the command for loading the packages
RUN git clone https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install
# this will generate the vprofile artifact on the docker instance. In the vprofile-project folder
# there will be the usual target folder that has the .war artifact
# At this point this image has build the artifact and once we copy the artifact to the tomcat instance
# below, this instance can be discarded


FROM tomcat:9-jre11

LABEL "Project"="Vprofile"
LABEL "Author"="dmastrop"
# https://hub.docker.com/_/tomcat
# second image will run tomcat on which we will place the artifact so that the vprofile application
# can be installed on it
# image tag is found in dockerhub
RUN rm -rf /usr/local/tomcat/webapps/*
# this is the default app folder in tomcat. We do not want the default files in this directory 
# on the tomcat instance because we want
# the .war artifact above to be the default app on this tomcat instance.
# This directory is on dockerhub for the tomcat:9-jre11 above
COPY  --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
# Next, copy the .war artifact to the first stage instance (from BUILD_IMAGE) to this image
# The name ROOT.war will make this the default app on this tomcat instance.


EXPOSE 8080
# tomcat runs by default 8080 but just add the EXPOSE to be complete

CMD ["catalina.sh", "run"]
# this is run by default on tomcat server, but just adding this to be complete
# this is from the dockerhub tomcat image information
