# Delivery Web App Design Doc

## Functionality
* Main dashboard can show restaurants and menu.
* User log-in and sign-up (through third party accounts).
* User can manage their orders: place order, cancel order, see order detail.
* User can track his/her order in real time (location update in real time).
* Optional: User can add each other as friend. In friends dashboard, they can see their friends' update and comment on these posts.
* Optional: User can order together with friend, support split payment and order sharing.
* Optional: User can comment on the order and share the post to the friends dashboard.

## Architecture

### Technology stack
* Frontend stack: J2EE Servelet, JSP, Bootstrap
* Backend stack: Spring Boot, Spring Cloud, Spring Data, Rabbit MQ (or other AMQP), MySQL (or other RDBMS), MongoDB (or other NoSQL), Docker, and Redis.

- Spring Boot will be serve as stand-alone REST microservice.
- Spring Cloud will be used for registration and discovery for REST microservices.
- Spring Data will replace traditional ORM to serve as lightweight database access layer.
- Redis serve as a cache layer for popular data in RDBMS to provide quick access to restaurant listing and menu items listing.
- RabbitMQ provide two message brocker paradigms: P2P channel is used for competing message consumers to consume which is suitable for order processing while Pub/Sub channel allows all message subscribers to handle messages which is suitable for location updating.
- All microservices, databases, cache store and spring cloud intance will be dockerized.


### Architecture diagram
![diagram](https://github.com/benjasy1993/DeliveryApp/blob/master/images/diagram.jpg "Architecture Diagram")


## Members

* Yinong Wu (front-end)
* Leo Liu (back-end)
* Young Liu (back-end)
* Shaoqian Yang (back-end)

## References

* [Bootstrap templates](https://startbootstrap.com/template-categories/all/)
* [Spring Boot tutorial](https://spring.io/guides/gs/spring-boot/)
* [Dependency management tutorial](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)

## How to create your own microservice
### Option 1
* use intellij idea as IDE
* import project
* choose `DeliveryApp/spring-delivery-app`
* choose `Create project from existing model`
* `next` all the way down until you open the project
* create your child module like this
![submodule](https://github.com/benjasy1993/DeliveryApp/blob/master/images/submodule.jpg "create a sub module")

### Option 2
* `cd DeliveryApp/spring-delivery-app`
* create your maven project under this folder
* add such content into your project pom file
```
<parent>
        <artifactId>spring-delivery-app</artifactId>
        <groupId>com.delivery.app</groupId>
        <version>1.0-SNAPSHOT</version>
</parent>
```
* add such content into pom file in the parent project (spring-delivery-app)
```
<modules>
        <module>your-own-microservice</module>
</modules>
```
* If you have any problem, follow the content-service module example

