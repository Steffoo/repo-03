FROM openjdk:8
COPY target/tomcat-6.0.53-1.0.0-jar-with-dependencies.jar .
ADD conf/ conf/
ADD webapps/ webapps/
EXPOSE 8081
CMD java -jar tomcat-6.0.53-1.0.0-jar-with-dependencies.jar
