FROM hypriot/rpi-java
RUN echo 'Acquire::http::proxy "http://10.0.4.2:3128/";' > /etc/apt/apt.conf.d/proxy.conf


RUN apt-get update -qq && apt-get install -y maven && apt-get clean
ADD settings.xml /root/.m2/settings.xml
WORKDIR /code

ADD pom.xml /code/pom.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-8-oracle/jre/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
