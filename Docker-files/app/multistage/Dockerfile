FROM openjdk:11 AS BUILD_IMAGE

# Install necessary packages
RUN apt update && apt install -y git maven

# Clone the repository and build
RUN git clone https://github.com/devopshydclub/vprofile-project.git \
    && cd vprofile-project \
    && git checkout docker \
    && mvn install

FROM tomcat:9-jre11

# Remove existing webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy WAR file from build stage
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
