# Run Spring-boot sample

## Overview
This sample showcases the how to integrate a spring-boot application with WSO2 Identity Server for
 secure authentication using OpenID Connect standard.

## Register Application

 1. Access WSO2 Identity Server Developer Portal .
 
 2. Go to **Applications** and click **New Application**.
  
 3. Click **Show More**
 
 4. Open **OIDC Web Application** template.
  
 5. Enter **Name** and **Description** and click **Next**.
 
 6. Enter **Callback URL**. 
 
     The **Callback URL** is the exact location in the service provider's application where a authorization code
      would be sent. This should be always `{baseUrl}/login/oauth2/code/wso2` .
      
      If you want configure oidc logout also, then you need to add post-logout-url.  You can add multiple callback
       urls. In WSO2 Identity Server, post-logout-url can be configured via callback URL.
       
       Add the two callBack URLs:
         - http://localhost:8080/spring-boot-sample/login/oauth2/code/wso2
         - http://localhost:8080/spring-boot-sample/login
     
 7. Click **Next**
 
 8. View the application details and Click **Finish**
 
 9. Click on **Access** tab and Note the the **Client ID** and **Client Secret** that appears. 
 
  
| Field                 | Value                             | 
| --------------------- | ------------------------------    | 
| Service Provider Name | your-application-name             |
| Description           | This is a spring-boot app         | 
| CallBack Url          | {baseUrl}/login/oauth2/code/wso2  |
                        |{baseUrl}/spring-boot-app           |

**Eg:**
 
| Field                 | Value                                                         | 
| --------------------- | -----------------------------                                 | 
| Service Provider Name | sample-app                                                    |
| Description           | This is a spring-boot application                             | 
| CallBack Url          | http://localhost:8080/sprinb-boot-app/login/oauth2/code/wso2  |
                        | http://localhost:8080/spring-boot-app                         |
 
 # Configure the Sample
  
- Explode the war file.
  
- Open the `application.yml` file located in `spring-boot-sample/WEB-INF/classes`
  
- Update the following configuration. Please note that you should not change any other configurations
  
```yaml
 provider:
    host: <server-host-name> #Change the host
  
  client:
    client-id: <application-client-id> #Change client-id
    client-secret: <application-client-secret> # Change client-secret
    post-logout-uri: <base-url>/spring-boot-sample/login
    scope: openid
    authorization-grant-type: authorization_code
 
```

**Example**:

```yaml
provider:
  host: https://localhost:9443 #Change the host

client:
  client-id: LQTLEgDFil5Tyf0wS5KWUShkMDEa #Change client-id
  client-secret: ZuFwLrbBKhp74NWT1zBIjXuXuYUa # Change client-secret
  post-logout-uri: http://localhost:8080/spring-boot-sample/login
  scope: openid
  authorization-grant-type: authorization_code
 
```

 ## Build the sample and Run it
 
**Option 1:  Get the war file to deploy and Run it**
 - You can clone this project and build it. 
 - Run `mvn clean install`. 
 - Get the `spring-boot-sample.war` file from `target` folder
 - Deploy the sample into the tomcat and start the tomcat
 
 **Option 2: Run the sample using embedded tomcat**
 - You can clone this project. 
 - Comment out the following dependency in the `pom.xml` file.
 
     ```xml
    <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-tomcat</artifactId>
         <scope>provided</scope>
    </dependency>
    ```
- Run the command `mvn clean spring-boot:run`
 