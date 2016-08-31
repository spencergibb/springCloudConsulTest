Test code to reproduce memory leak of AnnotationConfigApplicationContext.

To reproduce:

* update src/main/resources/bootstrap.yml to put the host and port of a running instance of consul
* Launch the service

`./gradlew bootRun`

* issue updates to consul that cause content refreshes in the service

`curl -X PUT -d "test value" http://<yourhost and port>/v1/kv/config/HelloWorld/test`

* each update will leak an instance of AnnotationConfigApplicationContext. 

I have been unable to reproduce using spring-boot 1.3.5. I am able to reproduce with 1.3.6, 1.3.7 and 1.4.0. 