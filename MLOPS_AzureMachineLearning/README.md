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
