
# build imager

FROM maven:3.6.1-jdk-11 as build

WORKDIR /build

RUN apt-get update && \
	apt-get install -y git && \
	git clone https://github.com/diegogomesaraujo/spring-cloud.git && \
	cd spring-cloud/eureka-server && \
	mvn clean package
	
# final image

FROM openjdk:11.0-jdk-slim

WORKDIR /app

COPY --from=build /build/spring-cloud/eureka-server/target/*.jar ./application.jar

EXPOSE 8761

CMD java -jar application.jar