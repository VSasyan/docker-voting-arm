FROM hypriot/rpi-java:1.7.0-jdk

RUN echo 'Acquire::http::Proxy "http://10.0.4.2:3128";' >> /etc/apt/apt.conf.d/proxy.conf

RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml
ADD settings.xml /etc/maven/settings.xml
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-1.7.0-openjdk-armhf/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
