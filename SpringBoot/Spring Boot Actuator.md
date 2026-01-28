Actuator: 

Provides production-ready endpoints to monitor and manage the Spring boot application. 


Project setup:  

<dependency> 

<groupId>org.springframework.boot</groupId> 

<artifactId>spring-boot-starter-actuator</artifactId> 

</dependency> 

application.properties 



Let's start the server and hit the Actuator endpoints: 



Health API : '/health' 

Metrics API : '/metrics' 


'/metrics' gives list of all metrics endpoint available 

Hitting specific metrics endpoint 


Lets first see some useful in-built Actuator endpoints: 

GET:  /health 

Provides health status of our application: UP, DOWN, OUT_OF_SERVICE, UNKNOWN  

By-default, its shows only the overall status of the application 

But if we want more details, we need to add:  


// by-default is 'never' 


/health endpoint can be extended to add additional checks like DB health, Cache status etc. beyond just application server status 



Adding DB health check: 

Adding Cache health check: 



Db is UP 

Cache is DOWN 

This shows Aggregate status, if 1 component down, overall status is down 

GET:   /metrics  
                and 

           /metrics/{metric name} 

 

Metric name 

What it represents 

Example 

JVM Memory Metrics 

 

 

 

 

jvm.memory.used 

Memory currently in use by JVM 

 { 
      "statistic": "VALUE", 
      "value": 99478616 
  } 
   

 

jvm.memory.max 

Max memory JVM can use 

  { 
      "statistic": "VALUE", 
      "value": 10989076477 
  } 

Garbage Collection Metrics 

 

 

 

 

jvm.gc.pause 

Time spent in GC. 
 
COUNT: total no. of  GC events occurred. 
 
TOTAL_TIME: total time spent in GC (usually seconds) 
 
MAX: longest single GC pause observed 

[ 
    { 
      "statistic": "COUNT", 
      "value": 12  
    }, 
    { 
      "statistic": "TOTAL_TIME", 
      "value": 2.305 
    }, 
    { 
      "statistic": "MAX", 
      "value": 0.9 
    } 
  ] 

Threads 

 

 

 

 

jvm.threads.live 

Number of live threads 

{ 
      "statistic": "VALUE", 
      "value": 22 
    } 

 

jvm.threads.peak 

Peak live thread count, since JVM started 

{ 
      "statistic": "VALUE", 
      "value": 50 
    } 

System Metrics 

 

 

 

 

system.cpu.usage 

CPU used by JVM  (range 0.0 - 1.0) 
 
 

Value: 0.10 -> 10%  

HTTP Server / Requests 

 

 

 

 

http.server.requests 

COUNT: Total no of HTTP requests received 
 
TOTAL_TIME: total time spent handling all requests (usually in seconds) 
 
MAX: longest time taken to handle a single request 

 

  "measurements": [ 

    { "statistic": "COUNT", "value": 152 }, 

    { "statistic": "TOTAL_TIME", "value": 23.45 }, 

    { "statistic": "MAX", "value": 0.89 } 

  ], 

  "availableTags": [ 

    { "tag": "method", "values": ["GET", "POST"] }, 

    { "tag": "status", "values": ["200", "404", "500"] } 

  ] 

} 

Database/ JDBC Metric 

 

 

 

 

jdbc.connections.active 

Connections currently in use 

 

VALUE: 3 

 

jdbc.connections.idle 

 

Idle connections in pool 

 

VALUE: 7 

 

jdbc.connections.max 

 

Max connections allowed 

 

VALUE: 10 

There are so many metrics, just showing some important ones: 

GET:   /threaddump 
              

Helps to diagnose deadlock or thread leaks. 

Which threads are active, blocked or waiting. 

Stack trace for each thread (what code it is executing) 

Thread name, id, priority etc. 

[ 

  { 

    "threadName": "main", 

    "threadId": 1, 

    "blockedTime": -1, 

    "blockedCount": 0, 

    "waitedTime": -1, 

    "waitedCount": 0, 

    "threadState": "RUNNABLE", 

    "stackTrace": [ 

      "com.concepts.MyService.methodName(MyService.java:142)", 

      "com.concepts.ActuatorApp.main(ActuatorApp.java:10)" 

    ] 

  }, 

 { 

    "threadName": "thread2", 

    "threadId": 2, 

    "blockedTime": -2, 

    "blockedCount": 0, 

    "waitedTime": -1, 

    "waitedCount": 0, 

    "threadState": "WAITING", 

    "stackTrace": [ 

      "com.concepts.ClassName.methodName(ClassName.java:12)", 

      "com.concepts.ActuatorApp.main(ActuatorApp.java:10)" 

    ] 

  } 

 ] 

What all other API's available:  
Official Documentation: https://docs.spring.io/spring-boot/reference/actuator/endpoints.html#actuator.endpoints 

/heapdump 

GET 

Downloads JVM heap as .hprof file 

/mappings 

GET 

Lists all Spring MVC request mappings 

/beans 

GET 

Displays a complete list of all the Spring beans in your application 

/configprops 

GET 

Lists all @ConfigurationProperties beans 

/loggers 

GET 

Lists all loggers and their current levels 

/shutdown 

POST 

Lets the application be gracefully shutdown 

/env 

GET 

Shows environment properties 

/actuator/env/{property} 

GET 

Shows a specific environment property 

By default, access to all endpoints except for "/shutdown" and "/heapdump" is unrestricted 

Both these endpoints are very critical: 

/shutdown can stop your application 

/heapdump can expose sensitive information about your application like tokens, password etc. 
 
So, by default they are restricted and specifically want us to unrestricted it (assuming, we have accepted the risk involved) 


Security: 



We have already covered Spring Security in depth (total 9 parts), so kindly check it out, if there is any doubt with that: 



Trying to access /evn without providing the authentication, request denied: 

Able to access, after successful Authentication: 


application.properties 

pom.xml 


Custom Actuator Endpoint: 

Class annotated with @Endpoint(id = "custom endpoint name") 

 

 

 

@Component 

@Endpoint(id = "my-custom-stats")               

public class MyCustomStatsEndpoint { ... } 

 

 

id → forms the URL path: /actuator/{id} 

@ReadOperation 
 
(equivalent to HTTP GET) 

@WriteOperation 

@DeleteOperation 

Type of operation, our custom endpoint going to support: 

(equivalent to HTTP POST) 

(equivalent to HTTP DELETE) 

// our endpoint becomes '/actuator/my-custom-stats' 

@Component 

@Endpoint(id = "my-custom-stats")               

public class MyCustomStatsEndpoint { 

 

    @ReadOperation 

    public String readAll() { 

        return "Hello, Spring Boot!"; 

    } 

 

   @ReadOperation 

    public String read(@Selector String name, @Selector String message) { 

        return "Hello: " + name + " msg for you is: " + message; 

    } 

} 



GET: 


GET: 

@Component 

@Endpoint(id = "my-custom-stats")               

public class MyCustomStatsEndpoint { 

 

    @WriteOperation 

    public String refresh() { 

          // simulate say cache refresh 

           return "refreshed"; 

    } 

 

   @DeleteOperation 

    public String remove(@Selector String key) { 

        return "reset done for key: " + key; 

    } 

} 

Return type can be any serializable object like Map, List, String, POJO, primitive etc. 

/my-custom-stats/{name}/{message} 
selector follows sequence 

For POST and DELETE operation, it requires authentication 



application.properties 



Pushing the metrics to Datadog (Monitoring platform) 
 
we can also push to different other platforms like: Prometheus, CloudWatch etc.. 


Datadog (we can test with Free trial) 



application.properties 

Every 5s it will push the metrics to datadog 

When its true then only it try to push the metrics 


pom.xml 

All the metrics of Spring Boot Actuator are automatically pushed to Datadog. 


choose the metric we want to monitor 
for example: http.server.requests.count 


