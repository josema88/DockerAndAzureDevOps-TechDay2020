# CI and CD Pipeline for a ASP.NET Core Application in a Docker Container

At this demo we will use the Demo 2 app: [josema88/eShopOnWeb](https://github.com/josema88/eShopOnWeb) and we will build a CI and CD pipelines with an [Azure DevOps'](https://azure.microsoft.com/en-us/services/devops/) service called [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/). For the CI process we will use a **Build Pipeline** and for the CD Process a **Release Pipeline**.

At this demo we will also see the importance of quality on the CI process in order to delivery reliable and secure software. We will automate the Unit Tests execution and the Static Code Analysis before build our application within a Docker Container.

At the CD process we will deploy our Docker Container to an [Azure App Service: Web App for Containers](https://azure.microsoft.com/es-es/services/app-service/containers/)

The Build Pipeline (CI) will perform:
- Static Code Analysis with [Sonar Qube](https://www.sonarqube.org/) and [Azure Container Instances](https://azure.microsoft.com/en-us/services/container-instances/)
- Unit Tests Execution
- Build and Push the Docker Container Image with Docker Compose.

The Release Pipeline (CD) Will perform: 
- The deployment of the Docker Container to Azure App Service.

The following diagram shows the CI/CD Process:
![CI CD Procecss](/images/CI-CD-Diagram.png)

You can find all the steps and processes to build the pipelines in the session's video (in spanish):
https://youtu.be/sLQSxPIvhbw


## Implementing SonarQube with Azure Container Instances and Azure SQL

You can create the resources through Azure CLI.

```
# Create Resource Group
$ az group create --name $resourceGroupName --location $location

# Create Azure SQL Server
$ az sql server create \
    --name $serverName \
    --resource-group $resourceGroupName \
    --location eastus \
    --admin-user "user_name" \
    --admin-password "user_password"

# Create Azure SQL Database
$ az sql db create \
    --resource-group $resourceGroupName \
    --server $serverName \
    --name $databaseName \
    --service-objective Basic \
    --collation SQL_Latin1_General_CP1_CS_AS

# Create Azure Container Instance
$ az container create --resource-group $resourceGroupName \
    --location eastus  --name sonarqube  \
    --cpu 2 --memory 2.5 \
    --image sonarqube:7.7-community \
    --os-type Linux \
    --ip-address Public --dns-name-label $Dns \
    --environment-variables \
    'SONARQUBE_JDBC_USERNAME'='user_name' \
    'SONARQUBE_JDBC_PASSWORD'='user_password' \
    'SONARQUBE_JDBC_URL'='jdbc_connection_string' \
    --ports 9000 --protocol TCP

```
Now you have your SonarQube Server running in Azure Container Instances.

You can enter at **your-dns.eastus.azurecontainer.io:9000** and you can login with the default user and password (admin/admin).