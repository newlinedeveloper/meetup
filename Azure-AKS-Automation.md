# AZURE Kubernetes Automation

# Before start this excercise,you must have running CENTOS 7 linux machine.

 - ** create 1 centos 7 linux machine in AZURE Cloud**

- Step 1:  Install AZURE CLI in CentOS 7 Machine
- Step 2:  First install docker in the local linux machine
- Step 3:  Download sample application
- Step 4:  Test sample application
- Step 5:  Deploy and use Azure Container Registry
- Step 6:  Install kubectl command 
- Step 7:  Deploy an Azure Kubernetes Service (AKS) cluster
- Step 8:  Run applications in Azure Kubernetes Service (AKS)
- Step 9:  Scale applications in Azure Kubernetes Service (AKS)
- Step 10: Autoscale pods
- Step 11: Manually scale AKS nodes (worker nodes)
- Step 12: Update an application in Azure Kubernetes Service (AKS)

#

Step 1: Install AZURE CLI

sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

sudo sh -c 'echo -e "[azure-cli]
name=Azure CLI
baseurl=https://packages.microsoft.com/yumrepos/azure-cli
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'



sudo yum install azure-cli -y


az login

Now your linux machine has been fully authenticated with AZURE login.

**************************************************************************************************************************************

Step 2 - first install docker in the local linux machine

 yum install epel-release -y
 yum repolist

#Install the required dependencies:

yum install yum-utils device-mapper-persistent-data lvm2  bash-completion bash-completion-extras -y

source /etc/profile.d/bash_completion.sh

#Add the stable Docker repository by typing:

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo


#Now that we have Docker repository enabled, we can install the latest version of Docker CE (Community Edition) using yum by typing:

yum install docker-ce -y

yum install docker-compose -y

#Once the Docker package is installed, we start the Docker daemon with:

systemctl start docker

#To verify that the Docker service is running type:

systemctl status docker

#Enable the Docker service to be automatically started at boot time:

systemctl enable docker

#At the time of the writing of this article, the current stable version of Docker is 18.03.1, we can check our Docker version by typing:

docker -v

**************************************************************************************************************************************

Step 3: Download sample application

yum install git tree -y

git clone https://github.com/Azure-Samples/azure-voting-app-redis.git

cd azure-voting-app-redis

docker-compose up -d

docker images

**************************************************************************************************************************************
Step 4: Test sample application

Test application locally

To see the running application, enter http://localhost:8080 in a local web browser


**************************************************************************************************************************************

Step 5: Deploy and use Azure Container Registry

az group create --name myResourceGroup --location eastus

az acr create --resource-group myResourceGroup --name cnlacr --sku Basic

az acr login --name cnlacr

docker images

az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table

cnlacr.azurecr.io

docker tag mcr.microsoft.com/azuredocs/azure-vote-front:v1 cnlacr.azurecr.io/azure-vote-front:v1


docker images

docker push cnlacr.azurecr.io/azure-vote-front:v1


az acr repository list --name cnlacr --output table



az acr repository show-tags --name cnlacr --repository azure-vote-front --output table



**************************************************************************************************************************************
Step 6: install kubectl command 

coz it wont work (because of the the direct standalone centos machine)




cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF


yum install -y kubectl


to ensure all are ok the following command should work without any error

kubectl version --client

**************************************************************************************************************************************
Step 7: Deploy an Azure Kubernetes Service (AKS) cluster

az aks create \
    --resource-group myResourceGroup \
    --name myAKSCluster \
    --node-count 1 \
    --generate-ssh-keys \
    --attach-acr cnlacr
	
	
	az aks install-cli
	
	az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

kubectl get nodes

**************************************************************************************************************************************

Step 8: Run applications in Azure Kubernetes Service (AKS)


az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table

vi azure-vote-all-in-one-redis.yaml

containers:
- name: azure-vote-front
  image: cnlacr.azurecr.io/azure-vote-front:v1
  

kubectl apply -f azure-vote-all-in-one-redis.yaml

kubectl get service azure-vote-front --watch

from the above command output get the EXTERNAL-IP and access it from browser


**************************************************************************************************************************************

Step 9: Scale applications in Azure Kubernetes Service (AKS)

in another putty window run the following command

watch -n 1 kubectl get all -o wide

in another putty window run the below commands

kubectl get pods

kubectl scale --replicas=2 deployment/azure-vote-front

kubectl scale --replicas=4 deployment/azure-vote-front


**************************************************************************************************************************************

Step 10: Autoscale pods

Kubernetes supports horizontal pod autoscaling to adjust the number of pods in a deployment depending on CPU utilization or other select metrics. The Metrics Server is used to provide resource utilization to Kubernetes, and is automatically deployed in AKS clusters versions 1.10 and higher. To see the version of your AKS cluster, use the az aks show command, as shown in the following example:


az aks show --resource-group myResourceGroup --name myAKSCluster --query kubernetesVersion --output table


these days AKS cluster is above 1.10 only.

now open 3 putty window and do the following


in another putty window run the following command

watch -n 1 kubectl get hpa -o wide

in another putty window run the following command

watch -n 1 kubectl get all -o wide

in another putty window run the following command

kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=2 --max=10


wait for 10 mins and you can see azure-vote-front pod now came down to 2 


**************************************************************************************************************************************

Step 11: Manually scale AKS nodes (worker nodes)

az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3


**************************************************************************************************************************************


Step 12: Update an application in Azure Kubernetes Service (AKS)

make some change in application


vi azure-vote/azure-vote/config_file.cfg

# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'

docker-compose up --build -d

docker tag mcr.microsoft.com/azuredocs/azure-vote-front:v1 cnlacr.azurecr.io/azure-vote-front:v2

docker push cnlacr.azurecr.io/azure-vote-front:v2



kubectl scale --replicas=3 deployment/azure-vote-front



kubectl set image deployment azure-vote-front azure-vote-front=cnlacr.azurecr.io/azure-vote-front:v2

run kubectl get service azure-vote-front command

now access 20.72.185.232 (external ip) in browser

you will see Blue,Purple,

**************************************************************************************************************************************
