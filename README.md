# springbootDocker

This project shows how to deploy a spring boot Rest application in a Docker container.

1. Running the application without Docker

Let's try to start application with the maven command : ./mvnw spring-boot:run

```
2017-09-10 15:58:17.223  INFO 8966 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2017-09-10 15:58:17.280  INFO 8966 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2017-09-10 15:58:17.285  INFO 8966 --- [           main] c.e.s.SpringbootDockerApplication        : Started SpringbootDockerApplication in 2.972 seconds (JVM running for 5.646)
2017-09-10 15:58:34.554  INFO 8966 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring FrameworkServlet 'dispatcherServlet'
2017-09-10 15:58:34.555  INFO 8966 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : FrameworkServlet 'dispatcherServlet': initialization started
2017-09-10 15:58:34.567  INFO 8966 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : FrameworkServlet 'dispatcherServlet': initialization completed in 12 ms
```

To test the application, just do : http://localhost:8080/ping


2. Running the application with a Dockerfile

Now, let's try to start our application with a container docker.

First, we build our docker container : docker build src/main/docker -t springbootdocker

Then we run it : docker run --rm -d -p 8383:8080 springbootdocker

To be sure our container is up, we do : docker ps

➜  springbootDocker git:(master) ✗ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
69c8a1f61cc1        springbootdocker    "/bin/sh -c 'java ..."   28 seconds ago      Up 27 seconds       0.0.0.0:8383->8080/tcp   relaxed_jones

to test the application, just do : http://192.168.43.90:8383/ping (replace the url with machine ip)


3. Running the application with a Docker-compose file

Another way to use docker is to use a docker-compose file. First stop your running docker with command : docker stop container_id.
If you test your applcation, you should have this:

➜  springbootDocker git:(master) ✗ curl -X GET http://192.168.43.90:8383/ping
curl: (7) Failed to connect to 192.168.43.90 port 8383: Connection refused

to start container with docker-compose, just do : docker-compose up -d (-d for detached mode)

➜  docker git:(master) ✗ docker-compose up -d
Starting docker_api-ping_1 ...
Starting docker_api-ping_1 ... done

We test our application with this url : http://192.168.43.90:8383/ping


