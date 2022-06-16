# Run Spring-boot sample

## Overview
This sample showcases the how to integrate a spring-boot application with WSO2 Identity Server for
 secure authentication using OpenID Connect standard.

## Register Application

 1. Access WSO2 Identity Server Developer Portal .
 
 2. Go to **Applications** and click **New Application**.
  
 3. Click **Show More**
 
 4. Open the **OIDC Web Application** template.
  
 5. Enter **Name** and **Description** and click **Next**.
 
 6. Enter **Callback URL**. 
 
     The **Callback URL** is the exact location in the service provider's application where an authorization code
      would be sent. This should always be `{baseUrl}/login/oauth2/code/wso2` .
      
      If you want configure oidc logout also, then you need to add post-logout-url.  You can add multiple callback
       urls. In WSO2 Identity Server, post-logout-url can be configured via callback URL.
       
       Add the two callBack URLs:
         - http://localhost:8080/spring-boot-sample/login/oauth2/code/wso2
         - http://localhost:8080/spring-boot-sample/login
     
 7. Click **Next**
 
 8. View the application details and Click **Finish**
 
 9. Click on **Access** tab and Note the the **Client ID** and **Client Secret** that appears. 
 
  
| Field                 | Value                                                             | 
| --------------------- | ------------------------------                                    | 
| Service Provider Name | your-application-name                                             |
| Description           | This is a spring-boot app                                         | 
| CallBack Url          | {baseUrl}/login/oauth2/code/wso2, {baseUrl}/spring-boot-app/login |
                                

**Eg:**
 
| Field                 | Value                                                                                                     | 
| --------------------- | -----------------------------                                                                             | 
| Service Provider Name | sample-app                                                                                                |
| Description           | This is a spring-boot application                                                                         | 
| CallBack Url          | http://localhost:8080/spring-boot-app/login/oauth2/code/wso2,http://localhost:8080/spring-boot-app/login  |

  ## Import the IS certificate

1. Download the certificate from the management console (for example, as IsCertificate.cer)

2. Locate $JAVA_HOME/jre/lib/security/cacerts

3. Import the certificate into the cacerts file using the following:
  keytool -import -alias isCertificate -keystore cacerts -file <IS_CERTIFICATE_FILE_LOCATION>
                         
  ## Build the sample and Run it
  
  - You can clone this project and build it. 
  - Run `mvn clean install`. 
  - Get the `spring-boot-sample.war` file from `target` folder.
  - Deploy the sample into the tomcat and start the tomcat.
  - Access `http://localhost:8080/spring-boot-sample/login` if your tomcat is running in port 8080. If not, change the
   port and host accordingly.
  
  
 ## Configure the Sample
  
- Open the `application.yml` file located in `spring-boot-sample/WEB-INF/classes` from the exploded war file.
  
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
