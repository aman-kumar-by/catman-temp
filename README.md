# NEO

## Overview

## Technology Stack and Resource uses

* Python 3.8+ <= 3.9.9
* ActiveMQ version: 5.15.x + 
  
    * NEO supports communications to ActiveMQ using STOMP protocol. 
  
    * stomp port must be configured in activemq.xml file. By default, the port is 61613 
* Kafka: 3.x.x + 

* SQL Server Driver

    See documentation from Microsoft here for more details:

    https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-ver15

    **macOS**
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
    brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
    brew update
    HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=Y brew install msodbcsql17 mssql-tools
    ```

## Deployment

### Dev Deployment

Build on command line or IDE
```
  cd plat-con-catman-adapter
  python -m pip install -e .
  python -m launch
```

Build using script

Linux
```
$ cd plat-con-catman-adapter
$ ./build.sh 
```

Windows
```
$ cd plat-con-catman-adapter
$ build.bat
```
### Build Docker Image and Deploy

##### Development phase
Install docker on your local and run below command to build the docker image and push to ACR. 

$cd plat-con-catman-adapter

$docker buildx build --tag "<azure-resource-name-of-your-container-registry>.azurecr.io/<your-image-name>:v1" .


##### Production phase
Install docker on your local and run below command to build the docker image and push to ACR. 
```
$ az login 
$ az acr login --name stratospherelive 
$ az acr login --name <azure-resource-name-of-your-stratosphere-registry> -$docker build --tag <azure-resource-name-of-your-container-registry.azurecr.io/your-image-name:<version> . 
$ docker push <azure-resource-name-of-your-container-registry.azurecr.io/your-image-name:<version>
$ docker push "<azure-resource-name-of-your-container-registry>.azurecr.io/<your-image-name>:v1"

```

## Run Test Cases
```
$pytest
```
