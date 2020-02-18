---
layout: post
title:  "RESTful Web Service Invoker (Spring Boot)"
date:   2020-02-18
excerpt: "RESTful Web Service Invoker (Spring Boot)"
project: true
tag:
- spring boot 
- rest services
comments: true
---

# RESTful Web Service Invoker (Spring Boot)

RESTful Web Service Invoker that binds remote rest services to java interfaces similarily to how InvocationHandler works. 

Invoking methods on those interfaces will make an HTTP request to the remote service and (de)serialize any objects.

Available methods : **GET, PATCH, POST, PUT**


![arch](https://raw.githubusercontent.com/gurkanakdeniz/rws-invoker/master/screen/arch.png "arch")


**example use in project** : [https://github.com/gurkanakdeniz/rws-invoker-sample](https://github.com/gurkanakdeniz/rws-invoker-sample) 

### 0. Getting

```xml
<repositories>
	<repository>
		<id>jitpack.io</id>
		<url>https://jitpack.io</url>
	</repository>
</repositories>
```
```xml
<dependency>
	<groupId>com.github.gurkanakdeniz</groupId>
	<artifactId>rws-invoker</artifactId>
	<version>1.0.5</version>
</dependency>
```

### Building

```mvn clean install```


### 1. Declare an interface, eg:

```java
public interface TestRestClient {

    @RestWebServiceType(RestWebServiceMethod.GET)
    public ResponseModel test();
    
    @RestWebServiceType(RestWebServiceMethod.GET)
    public ResponseModel testPathVariable(RequestModel request);
    
    @RestWebServiceType(RestWebServiceMethod.GET)
    public ResponseRequestParam testRequestParam(RequestRequestParam request);
    
    @RestWebServiceType(RestWebServiceMethod.POST)
    public ResponsePostModel testPost(RequestPostModel request);
}
```

Note :  If get HTTP codes extends ```RestWebServiceBaseResponse ``` , eg:

```java
public class ResponseModel extends RestWebServiceBaseResponse {

    private String name;
    private String blog;
    
    ....
}
```

```java
public class RestWebServiceBaseResponse implements Serializable {

    private static final long serialVersionUID = 1L;
    private transient String invokeStatus;
    private transient String invokeStatusCode;

    public String getInvokeStatus() {
        return invokeStatus;
    }

    public void setInvokeStatus(String invokeStatus) {
        this.invokeStatus = invokeStatus;
    }

    public String getInvokeStatusCode() {
        return invokeStatusCode;
    }

    public void setInvokeStatusCode(String invokeStatusCode) {
        this.invokeStatusCode = invokeStatusCode;
    }
}
```

### 2. Configuration

Interface name and method name registries : 

```java
@RestWebServiceInvokerEnable
@Configuration
public class RestServicesConfig extends RestWebServiceConfig {

    @Override
    public HashMap<String, RestWebServiceEndpoint> endpoints() {
        HashMap<String, RestWebServiceEndpoint> response = new HashMap<String, RestWebServiceEndpoint>();
        
        // config file or table

        RestWebServiceEndpoint restWebServiceEndpoint = new RestWebServiceEndpoint("https://api.github.com/",
                "com.example.demo.sample.TestRestClient", "test", RestWebServiceMethod.GET);
        response.put(restWebServiceEndpoint.getEndpointKey(), restWebServiceEndpoint);
        
        ... blah blah
        
        return response;
    }

}
```

### 3. Use it

use example :

```java
@RestWebService
private TestRestClient testRestClient;

...

public String test() {
	ResponseModel test = testRestClient.test();
	RequestModel request1 = new RequestModel();
	request1.setPathVariable("gurkanakdeniz");
       	ResponseModel test1 = testRestClient.testPathVariable(request1);

	RequestRequestParam request2 = new RequestRequestParam();
       	request2.setPage(2);
       	ResponseRequestParam test2 = testRestClient.testRequestParam(request2);

	RequestPostModel request3 = new RequestPostModel();
       	request3.setJob("jedi");
       	request3.setName("yoda");
       	ResponsePostModel test3 = testRestClient.testPost(request3);

       	return "of the jedi";
}

```


use example customer invoker :

```java
private TestRestClient testRestClient2 = RestWebServiceFactory.newInstance(TestRestClient.class,
	new RestWebServiceHandler() {
		@Override
		public Object invoke(Object arg0, Method arg1, Object[] arg2) throws Throwable {
			System.out.println(" ------ custom invoke rest service ----");
                    	return null;
               }
   	});
```

### 4. Examples

Path Variable:
```java
public class RequestModel {

    @PathVariable(name = "userName")
    private String pathVariable;

    public String getPathVariable() {
        return pathVariable;
    }

    public void setPathVariable(String pathVariable) {
        this.pathVariable = pathVariable;
    }
}
```

```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-------- REQUEST START ----------
URL        : https://api.github.com/users/gurkanakdeniz
REQ        : {"pathVariable":"gurkanakdeniz"}
--------  REQUEST END  ----------

-------- RESPONSE START ----------
URL        : https://api.github.com/users/gurkanakdeniz
STATUS     : HTTP/1.1 200 OK
STATUSCODE : 200
RES        : {"name":"Gürkan Akdeniz","blog":"https://gurkanakdeniz.github.io/"}
--------  RESPONSE END  ----------
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
Request Param:

```java

public class RequestRequestParam {
    
    @RequestParam(name = "page")
    private int page;

    public int getPage() {
        return page;
    }

    public void setPage(int page) {
        this.page = page;
    }    
}

```

```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-------- REQUEST START ----------
URL        : https://reqres.in/api/users?page=2
REQ        : {"page":2}
--------  REQUEST END  ----------

-------- RESPONSE START ----------
URL        : https://reqres.in/api/users?page=2
STATUS     : HTTP/1.1 200 OK
STATUSCODE : 200
RES        : {"page":2,"per_page":6,"total":12}
--------  RESPONSE END  ----------
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

Request Json:

```java
public class RequestPostModel {

    private String name;
    private String job;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

}
```

```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-------- REQUEST START ----------
URL        : https://reqres.in/api/users
REQ        : {"name":"yoda","job":"jedi"}
--------  REQUEST END  ----------

-------- RESPONSE START ----------
URL        : https://reqres.in/api/users
STATUS     : HTTP/1.1 201 Created
STATUSCODE : 201
RES        : {"name":"yoda","job":"jedi","id":"914","createdAt":"Feb 18, 2020, 9:11:26 PM"}
--------  RESPONSE END  ----------
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details
