---
title: Deploying Spring Boot Application to PCF (Pivotal Cloud Foundry)
date: 2018-03-28
draft: false

---
PaaS (Platform as a Service) is changing the way of how we build production ready software in a much faster and simpler way. Pivotal Cloud Foundry (PCF) is a major commercial version of open source Cloud Foundry. As part of this post, I have take a sample spring boot application and deploying the same to PCF via CLI. The demo application has two REST api end point `/addTask` and `/fetchTasks` for adding a new task to ToDo and fetch all the ToDo tasks. Application is deployed as a self contained fat jar with embedded tomcat. 


## Clone the source code from GitHub repository

https://github.com/sujittripathy/ToDoPlannerCF

## Create a deployment artifact (jar)
After cloning the code, on the project root execute below command to create maven jar artifact. This will create the self contained jar at `/target` path.

```
mvn package
```

## Start the application in local

To verify application running in location, run the target jar.

```
java -jar ToDoPlannerCF-0.0.1-SNAPSHOT.jar
```

Verify if server gets started at port 8080. The REST api should be accessible at `http:\\localhost:8080\addTask` and `http:\\localhost:8080\fetchTasks`

```
2018-03-28 21:31:25.775  INFO 9509 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2018-03-28 21:31:25.781  INFO 9509 --- [           main] c.t.T.ToDoPlannerCfApplication           : Started ToDoPlannerCfApplication in 11.394 seconds (JVM running for 12.069)

```

## Let's deploy the application to PCF

*Note: Registration is required at https://run.pivotal.io to deploy to [PCF]. The space need to be created in PCF where app will be deployment prior to pushing the app to PCF.*

A manifest file need to exists on the project root folder for deployment of application to PCF. This is a type of descriptor file which has properties of application such as name, path, memory requirement, number of instances, service dependency etc. Below is the `manifest.yml` file for the demo application which we are going to deploy to PCF via CLI. For now, ignore the rabbitmq service dependency.

```
---
 applications:
 - name: ToDoPlannerCF
   memory: 1gb
   instances: 1
   path: ./target/ToDoPlannerCF-0.0.1-SNAPSHOT.jar
   services:
    - postgress
    - rabbitmq

```

**Step 1** - Navigate to project root location and execute `cf push`. PCF will take care of build pack download for specific language (in this case Java) and deploying the same in PCF container via
BOSH.

```
Binding service rabbitmq to app ToDoPlannerCF in org Neon / space development as tripathy1.kits@gmail.com...
OK

Starting app ToDoPlannerCF in org Neon / space development as tripathy1.kits@gmail.com...
.
.
.
Cell 9a954275-7f82-421f-9904-247e12f74292 creating container for instance 19350fe5-fc36-410f-bfc3-84f43783c815
Cell 9a954275-7f82-421f-9904-247e12f74292 successfully created container for instance 19350fe5-fc36-410f-bfc3-84f43783c815
Downloading build artifacts cache...
Downloading app package...
Downloaded build artifacts cache (132B)
Downloaded app package (33.7M)
-----> Java Buildpack v4.9 (offline) | https://github.com/cloudfoundry/java-buildpack.git#830f4c3
-----> Downloading Jvmkill Agent 1.12.0_RELEASE from https://java-buildpack.cloudfoundry.org/jvmkill/trusty/x86_64/jvmkill-1.12.0_RELEASE.so (found in cache)
-----> Downloading Open Jdk JRE 1.8.0_162 from https://java-buildpack.cloudfoundry.org/openjdk/trusty/x86_64/openjdk-1.8.0_162.tar.gz (found in cache)
       Expanding Open Jdk JRE to .java-buildpack/open_jdk_jre (1.1s)
       JVM DNS caching disabled in lieu of BOSH DNS caching
-----> Downloading Open JDK Like Memory Calculator 3.10.0_RELEASE from https://java-buildpack.cloudfoundry.org/memory-calculator/trusty/x86_64/memory-calculator-3.10.0_RELEASE.tar.gz (found in cache)
       Loaded Classes: 18656, Threads: 250
-----> Downloading Client Certificate Mapper 1.5.0_RELEASE from https://java-buildpack.cloudfoundry.org/client-certificate-mapper/client-certificate-mapper-1.5.0_RELEASE.jar (found in cache)
-----> Downloading Container Security Provider 1.13.0_RELEASE from
.
.
.

```

**Step 2** - Verify the status of the app instance with the command `cf apps`. The recently application is in started state.

```
ToDoPlannerCF $cf apps
Getting apps in org Neon / space development as tripathy1.kits@gmail.com...
OK

name                    requested state   instances   memory   disk   urls
ToDoPlannerCF           started           1/1         1G       1G     todoplannercf.cfapps.io

```

**Step 3** - Let's login to PCF web console and verify the application running status. As we are seeing below the application is running at `https://todoplannercf.cfapps.io/` which is running in cloud.

![](/img/spring_boot_deployment_pcf/img1.png)

As part of **Last Step**, let's trigger the REST API from postman and verify if the request is executing successfully.

![](/img/spring_boot_deployment_pcf/img2.png)

The API response code was 200 which executed successfully executed and received the To Do task id in response body.

