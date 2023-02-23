# About me

![About Me](speaker.jpg)

# WHAT IS AWX ?

AWX for short—is an opensource community project, sponsored by Red Hat, that enables users to better control their community Ansible project use in IT environments.

AWX is an opensource web application that provides a user interface, REST API, and task engine for Ansible. It's the opensource version of the Ansible Tower. The AWX allows you to manage Ansible playbooks, inventories, and schedule jobs to run using the web interface.

https://www.ansible.com/products/awx-project/faq




# Requirements

> The system that runs the AWX service will need to satisfy the following requirements:
- At least 4GB of memory
- At least 2 CPU cores
- At least 20GB of space
- Ansible Version 2.8+
- Python 3.6+
- docker Python module
- GNU Make
- Git Version 1.8.4+
- Node 10.x LTS version
- A running Docker, OpenShift, or Kubernetes
- A minimum PostgreSQL version 9.4 if you choose to use an external database

# Installation and configuration of AWX

## Step 1. Install required packages

- 01- First, we need to install the EPEL Repository as below:

```
dnf -y install epel-release
dnf -y install dnf-plugins-core
dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf config-manager --set-enabled powertools
```

- 02- Second, we need to install some dependencies packages like ansible:

```
dnf install git gcc gcc-c++ nodejs gettext device-mapper-persistent-data lvm2 bzip2 python3-pip ansible
```

## Step 2./ Install Docker

- 01- To install Docker, first, we need to install the Docker repository, so use the following command:

```
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

- 02- Next, use the below command to install docker-ce package:

```
dnf install docker-ce --nobest –y
```

- 03- Once the installation finished, let’s enable and start the Docker daemon:

```
systemctl enable --now docker.service
```

## Step 3./ Install Docker-compose tool


- 01- First, set python3 as the default one by running the below command:

```
alternatives --set python /usr/bin/python3
```

- 02- Next, use pip3 command to install the docker-compose tool:

```
pip3 install docker-compose
```

## Step 4. Install Ansible AWX

- 01- Now we can finally install Ansible AWX. Clone the latest release with the command:

```
git clone -b "17.1.0" https://github.com/ansible/awx.git
```

- 02- Next, generate a secret encryption key with the command:

```
openssl rand -base64 30
```

> PblrUyeSvBMVWqHaaDMFcABcjzgG5dAhfeOgge4S

- 03- navigate to the awx/installer directory and locate the inventory file. We need to adjust a few parameters:

```
cd awx/installer/
```

- ** open inventory file**

```
vi inventory
```

```

[all:vars]
dockerhub_base=ansible
awx_task_hostname=awx
awx_web_hostname=awxweb
postgres_data_dir="/myawx/pgdocker"
host_port=80
host_port_ssl=443
docker_compose_dir="/myawx/awxcompose"
pg_username=awx
pg_password=awxpass
pg_database=awx
pg_port=5432
admin_user=admin
admin_password=password
create_preload_data=True
secret_key=PblrUyeSvBMVWqHaaDMFcABcjzgG5dAhfeOgge4S
awx_official=true
project_data_dir=/myawx/projects
```

- 04- So, to install Ansible AWX run the Ansible command:

```
ansible-playbook -i inventory install.yml
```


- 05- After the installation is done, you can check the containers created by the docker-compose as below:


```
docker ps
```

- 06- In Case that the firewalld is enabled and running, then use the below commands to allow the http port (80) and https (443):


```
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd –reload
```

- 07- If the Selinux enabled, use the below commands to Allow the Awx web server to access the network:

```
semanage port -a -t http_port_t -p tcp 8052
setsebool -P httpd_can_network_connect 1
```

# USE-case-1

## 1. Login to the awx_task container

```
docker exec -it awx_task bash
```

## 2. Make directory 

```
mkdir inventory
```

## 3. Create file add the hosts list in that file
```
vi hosts_list
```

```
192.168.0.100
192.168.0.101
```

## 4. Import the host list to specific directory 

```
awx-manage inventory_import --inventory-name  APPS_Group-A --source hosts_list
```



