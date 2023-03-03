# About me

![About Me](speaker.jpg)

# MLOPS AzureMachineLearning

- **MLOps** helps us to understand how to build a Continuous Integration and Continuous Delivery pipeline for an ML/AI project.

- Let us use the Azure DevOps Project for build and release/deployment pipelines along with Azure ML services for model retraining pipeline, model management and operationalization.

![Architecture](pics/Picture1.png)


# PREREQUISITE:
- •	Active Azure subscription
- •	At least contributor access to Azure subscription

> In this example, we are using a sample ML project diabetes_regression to set up MLOPSPython. The project creates a linear regression model to predict diabetes and has CI/CD DevOps practices enabled for model training and serving.

- For the purpose of demo, I am using a “Pay as you go” subscription model of azure to be able to run CI/CD jobs.


## STEP1: CREATION OF AZURE ACCOUNT

- For details on how to create an azure account please use the link below
- https://azure.microsoft.com/en-in/free/ 

## STEP2: CREATION OF DEVOPS ORGANIZATION

- To create an Azure DevOps organization, please refer to 
- https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops

## STEP3: CREATION OF PROJECT IN AZURE DEVOPS

- (i)	Navigate to Azure DevOps Organization, Click on “New Project” 

![Architecture](pics/Picture2.png)

- (ii)	Enter the name of the project, click create

![Architecture](pics/Picture3.png)

> Now we have the Azure DevOps Project Created.  

![Architecture](pics/Picture4.png)


## Install the Azure Machine Learning extension

> Install the Azure Machine Learning extension to your Azure DevOps organization from the Visual Studio Marketplace by clicking "Get it free" and following the steps. The UI will tell you if try to add it and it's already installed.

> This extension contains the Azure ML pipeline tasks and adds the ability to create Azure ML Workspace service connections.

![Architecture](pics/Picture5.png)


> Click on it --> Go to “Browse Marketplace” --> search for “Machine Learning Extension”

![Architecture](pics/Picture6.png)



![Architecture](pics/Picture7.png)

> Once it is installed, go back to the project that has been created and navigate to 

> Pipelines --> Library --> Create Variable Group

- Create a Variable Group for your Pipeline:
- Create a variable group named devopsforai-aml-vg. The YAML pipeline definitions in this repository refer to this variable group by name.


- The variable group should contain the following required variables. 


![Architecture](pics/Picture8.png)

![Architecture](pics/Picture9.png)

![Architecture](pics/Picture10.png)

![Architecture](pics/Picture11.png)

![Architecture](pics/table.png)

![Architecture](pics/table1.png)

![Architecture](pics/Picture12.png)


![Architecture](pics/Picture14.png)

![Architecture](pics/Picture15.png)

![Architecture](pics/Picture16.png)

> While trying to add service connection, we will be asked to authenticate using the azure account.


![Architecture](pics/Picture17.png)

![Architecture](pics/Picture18.png)

![Architecture](pics/Picture19.png)

![Architecture](pics/table2.png)

![Architecture](pics/Picture20.png)

![Architecture](pics/Picture21.png)

![Architecture](pics/Picture22.png)

![Architecture](pics/Picture23.png)

![Architecture](pics/Picture24.png)

![Architecture](pics/Picture25.png)

![Architecture](pics/Picture26.png)

![Architecture](pics/Picture27.png)

> Having done that, run the pipeline: - this should create a resource group, a Key Vault, a Storage Account, a Container Registry, an Application Insights and a Machine Learning workspace.

![Architecture](pics/Picture28.png)

![Architecture](pics/Picture29.png)

![Architecture](pics/Picture30.png)

> Once the build job is successful, Check on the resources created via Azure portal.

![Architecture](pics/Picture31.png)

![Architecture](pics/table3.png)

![Architecture](pics/Picture32.png)

![Architecture](pics/Picture33.png)

![Architecture](pics/table4.png)

![Architecture](pics/Picture34.png)

![Architecture](pics/Picture35.png)

![Architecture](pics/Picture36.png)


> Great, you now have the build pipeline for training set up which automatically triggers every time there's a change in the master branch!


> After the pipeline is finished, you'll also see a new model in the AML Workspace model registry section:


![Architecture](pics/Picture37.png)


![Architecture](pics/Picture38.png)


![Architecture](pics/table5.png)


![Architecture](pics/table6.png)


![Architecture](pics/Picture39.png)

![Architecture](pics/table7.png)

![Architecture](pics/Picture40.png)

![Architecture](pics/Picture41.png)

![Architecture](pics/Picture42.png)

![Architecture](pics/Picture43.png)