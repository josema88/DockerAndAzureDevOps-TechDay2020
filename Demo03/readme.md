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
https://www.youtube.com/watch?v=sLQSxPIvhbw