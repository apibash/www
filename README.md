# www.apibash.com


## CRUD
 In REST APIs, the commonly known CRUD:
 + Create
 + Read
 + Update
 + Delete
 
## REST 
The operations are usually translated into REST API REQUEST
+ POST
+ GET
+ PUT
+ DELETE

## CURL

The curl command allows us to address the API endpoints along with the desired HTTP method. 
The method can be specified in the curl command line in the -X <<HTTP Method>>. 
  
A common curl example is structured as follows:

```
curl -s -k -X <<COMMAND>> –header Content-Type: application/json’ \\  
         –header ‘Accept:application/json’  \\  
         <<AUTHENTICATION>>  <<OPTIONALDATA>> \\  
         <<RESTAPIENDPOINT>>
```
  
+ -s is the silent mode. It limits the output of the curl command execution.
+ -k is to allow self-signed certificate or "in-secured connection"
+ -X <<COMMAND>>_ specifies the HTTP operation to be used.
+ <<RESTAPIENDPOINT>> depends on your API design and deployment. Typically, it is characterized as https://<<HOST>>:<<PORT>>/<<BASEURL>>/<<OTHERSPECIFICS>>
+ <<OPTIONALDATA>> tends to be required for POST and PUT and can simply be -d @”$JSONFILE”, where $JSONFILE is an environment variable that points to the JSON data file.
> 
> _–header ‘Content-Type: application/json’_ indicates the data coming with the request are JSON formatted
> 
> _–header ‘Accept:application/json’_ tells the API endpoint that JSON output is expected
> 
> <AUTHENTICATION>> varies and depends on the particular API. Some typical examples are:
> 
> -   Basic Authentication: _–header ‘Authorization: Basic <<Id:PasswordBase64EncodedValue>>’_
> -   Bearer Token: _–header ‘Authorization: Bearer <<BearerToken>>’_
> -   Cookie: –_\-cookie CookieJarFileToReadFrom –cookiejar CookieJarFileToWriteTo_
> 
> #### Authentication Module
> 
> For privileged API operations that require authentication/authorization, the security token is specified through the curl command as shown above, the diversity of authentication options and REST API deployment instances suggest having a separate shell script as a module for all other REST API calls. This authentication module would export out the HOST, PORT, and AUTHN environment variables.
> 
> #!/bin/bash  
> export HOST=…  
> export PORT=…  
> export AUTHN=…
> 
> To increase the maintainability of a Rest API client script, we suggest constructing the commonly used CRUD (Create, Read, Update, Delete) commands using more descriptive file names. For example, with the authentication module in place, a Read operation named as **read.sh** could look like:
> 
> #!/bin/bash  
> . ${HOMEDIR}/authn  
> curl -s -k -X GET –header Content-Type: application/json’ \\  
>         –header ‘Accept: application/json’  \\  
>         “${AUTHN}” \\  
>         “https://${HOST}${PORT}”/<<BASEURL>>/<<ENDPOINTSPECIFIC>>”
> 
> In addition to the common CRUD operations, there may be other application specific operations implemented through the POST/GET/PUT/DELETE verbs. In those cases, please name the operation similar to **read.sh** to correctly reflect the nature of them.
> 
> #### Directory Structure and Objects
> 
> The API CRUD operations operate on objects, represented by their URIs, used in the applications. When there are more object types, a simple read.sh could become readobjtype1.sh, readobjtype2.sh, …, and so on. Alternatively, a hierarchical directory structure similar to the URI itself can be used to group operations that belong to the same object type. Then, we could have objtype1/read.sh, objtype1/create.sh, …, and so on.
> 
> For applications that use endpoints with multi-level structures, you can choose to adopt the same subdirectory structures, for example domains/realms/rules/create.sh or you may choose to flatten it up as rules/create.sh so long as doing so does not result in conflicts.
> 
> #### Templates and JSON Files.
> 
> The create operation of a REST API usually takes a JSON input to hold the attributes of the object. Instead of attempting to use a program that accepts parameters to construct the JSON data on the fly, it is actually more appropriate to set aside commonly used templates to save the users from having to specify all those attributes. These templates could include both simple objects and more complicated relationships.
> 
> A template could simply be a shell script that takes parameters and uses the echo command to help deliver the desired JSON data. A minimal example could look like:
> 
> #!/bin/bash  
> Name=$1  
> echo <<EOF  
> {  
>     "Name": "$Name" 
> }  
> EOF
  
  
---
+ [edit](https://github.com/apibash/www/edit/main/README.md)
+ [git](https://github.com/apibash/www)
  
```
https://github.com/apibash/www.git
```  
