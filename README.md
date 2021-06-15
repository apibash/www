# www.apibash.com


## Why Use Shell Scripts?

Shell scripts are great tools for rapid development and validation for simple (smaller) requirements. 

Most likely, your company employs more Java and/or PHP programmers than Linux Shell script programmers.

The "use cases" will be programmed using either Unix/Linux Shell and/or Windows PowerShell scripts. You can easily port the logic from these scripts into your favorite programming language. Basic examples of connection with API will be provided for a number of major programming languages in a later section of this document.
Shell scripts are great tools for rapid development and validation for simple (smaller) requirements. Most development is done iteratively, and shell scripts provide immediate feedback on logic and code.

**Company-supported programming languages are the preferred tools for enterprise applications.**


Most likely, your company employs more Java and/or PHP programmers than Linux Shell script programmers.

The "use cases" will be programmed using either Unix/Linux Shell and/or Windows PowerShell scripts. You can easily port the logic from these scripts into your favorite programming language. Basic examples of connection with API will be provided for a number of major programming languages in a later section of this document.

## Linux/Unix/(and Mac too) Shell Scripts

There are numerous shell environments, including sh, bash, csh, ksh, and tsh. 


## Windows PowerShell

Powershell Open Source is now available for Linux and Mac OS.

https://techcrunch.com/2016/08/18/microsoft-open-sources-powershell-brings-it-to-linux-and-os-x/
Requirements

Windows has a number of versions of Powershell.

## Unix/Linux/Mac Shell
https://gist.github.com/cjus/1047794

Unix/Linux tools come natively with a host of shell utilities that one can use for parsing out the desired name/value pairs. Tools include sed, awk, cut, tr, and grep, to name a few. System administrators use these utilities frequently and may be able to assist with the methods for parsing JSON strings.
Basic awk and sed parsing
    
    echo $json | sed -e 's/[{}]/''/g' | awk -v RS=',' -F: '{print $1 $2}'

## Examples

### GITLAB
[cClaude/gitlab-bash-api: Configure GitLab using bash scripts](https://github.com/cClaude/gitlab-bash-api)

### bamboo: cURL, um REST Api - Bash, Curl

Diese API benötigt einen Benutzernamen und ein Passwort, kann aber nicht in Bamboo gespeichert werden,
da sie in der Bash-Historie des Build-Agenten angezeigt werden kann.

    curl -f -v -k --user "${bamboo.user}":"${bamboo.password}" -X POST https://bamboo.url/builds/rest/api/latest/queue/project_name"/



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
curl -s -k -X <<COMMAND>–header Content-Type: application/json' \\  
                        –header 'Accept:application/json' \\  
                        <<AUTHENTICATION>> <<OPTIONALDATA>\\  
                        <<RESTAPIENDPOINT>>
```
  
+ -s is the silent mode. It limits the output of the curl command execution.
+ -k is to allow self-signed certificate or "in-secured connection"
+ -X <<COMMAND>> specifies the HTTP operation to be used.
+ <<RESTAPIENDPOINT>depends on your API design and deployment. Typically, it is characterized as https://<<HOST>>:<<PORT>>/<<BASEURL>>/<<OTHERSPECIFICS>>
+ <<OPTIONALDATA>tends to be required for POST and PUT and can simply be -d @”$JSONFILE”, where $JSONFILE is an environment variable that points to the JSON data file.


    –header 'Content-Type: application/json' 
 
indicates the data coming with the request are JSON formatted


    –header 'Accept:application/json'

tells the API endpoint that JSON output is expected


 

### Typical examples for AUTHENTICATION

<AUTHENTICATION>varies and depends on the particular API.

#### Basic Authentication:
    –header 'Authorization: Basic <<Id:PasswordBase64EncodedValue>>'_

#### Bearer Token:
    –header 'Authorization: Bearer <<BearerToken>>'_

#### Cookie: 
    _\-cookie CookieJarFileToReadFrom –cookiejar CookieJarFileToWriteTo_

#### Authentication Module

For privileged API operations that require authentication/authorization, the security token is specified through the curl command as shown above, the diversity of authentication options and REST API deployment instances suggest having a separate shell script as a module for all other REST API calls. This authentication module would export out the HOST, PORT, and AUTHN environment variables.
```
#!/bin/bash  
export HOST=…  
export PORT=…  
export AUTHN=…
```

To increase the maintainability of a Rest API client script, we suggest constructing the commonly used CRUD (Create, Read, Update, Delete) commands using more descriptive file names. For example, with the authentication module in place, a Read operation named as **read.sh** could look like:

```
#!/bin/bash
. ${HOMEDIR}/authn
curl -s -k -X GET –header Content-Type: application/json' \\  
                    –header 'Accept: application/json' \\  
                    "${AUTHN}” \\  
                    "https://${HOST}${PORT}”/<<BASEURL>>/<<ENDPOINTSPECIFIC>>”
```

In addition to the common CRUD operations, there may be other application specific operations implemented through the POST/GET/PUT/DELETE verbs. In those cases, please name the operation similar to **read.sh** to correctly reflect the nature of them.

#### Directory Structure and Objects

The API CRUD operations operate on objects, represented by their URIs, used in the applications. When there are more object types, a simple read.sh could become readobjtype1.sh, readobjtype2.sh, …, and so on. Alternatively, a hierarchical directory structure similar to the URI itself can be used to group operations that belong to the same object type. Then, we could have objtype1/read.sh, objtype1/create.sh, …, and so on.

For applications that use endpoints with multi-level structures, you can choose to adopt the same subdirectory structures, for example domains/realms/rules/create.sh or you may choose to flatten it up as rules/create.sh so long as doing so does not result in conflicts.

#### Templates and JSON Files.

The create operation of a REST API usually takes a JSON input to hold the attributes of the object. Instead of attempting to use a program that accepts parameters to construct the JSON data on the fly, it is actually more appropriate to set aside commonly used templates to save the users from having to specify all those attributes. These templates could include both simple objects and more complicated relationships.

A template could simply be a shell script that takes parameters and uses the echo command to help deliver the desired JSON data. A minimal example could look like:

```
#!/bin/bash  
Name=$1  
echo <<EOF  
{  
 "Name": "$Name" 
}  
EOF
```




  
---
+ [edit](https://github.com/apibash/www/edit/main/README.md)
+ [git](https://github.com/apibash/www)
  
```
https://github.com/apibash/www.git
```  
