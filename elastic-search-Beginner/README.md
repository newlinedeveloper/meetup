# About me

[![Watch the video](profile.jpg)]

# INSTALLATION OF ELASTICSEARCH ON AWS EC2

- Before start this excercise,you must have running **AmazonEC2 Windows(minimum 2vcpus and 4GB Memory) machine**.



# AWS EC2

 - Create 1 AmazonEC2 Windows machine in the AWS Cloud Portal
 - Note that this will work only in 'Pay-As-You-Go' Subscription and not on Free Tier
 - Turn off Windows Defender/firewall on the EC2 machine
 - Make sure you open RDP,http,https and  9200,9300 ports for this new linux AZURE VM or you can also open any port by using port * any


# Steps

- Step 1:  Connect to the AWS EC2 Windows Machine by downloading the RDP Client and generating password using the keyfile.
- Step 2:  Install Google Chrome on AWS EC2 Windows Machine
- Step 3:  Download ElasticSearch for windows
- Step 4:  Running Elasticsearch From the CommandLine
- Step 5:  Testing ElasticSearch Installation Using a Curl Command
- Step 6:  Installation Successful


#

# Step 2: Install Google Chrome 

- Open the Edge Browser which is readily available on the instance and download Google Chrome

# Step 3: Download ElasticSearch for Windows

- Download ElasticSearch for installation on windows - https://www.elastic.co/downloads/elasticsearch

- Unzip the folder elasticsearch-8.6.1-windows-x86_64.zip.This will create a folder called elasticsearch-8.6.1.

- Open a command Prompt,Navigate to the elasticsearch-8.6.1 folder to which the files of ELastic Search has been extracted.
  

# Step 4 - Running Elasticsearch From the CommandLine

- From cmd, run the script beloow

```
 .\bin\elasticsearch.bat

```

## Step 4.1 - Execution Details of ElasticSearch from Console

- when the script is being executed,logs will be printed to the console(STDOUT) which will have details of password printed.

- Copy and save the credentials of the installation on to a notepad as it is required for future reference.

- On the logs being printed during the installation, the detials of password for the user elastic will be shown, which can be copied on to a notepad

```
Γ£à Elasticsearch security features have been automatically configured!
Γ£à Authentication is enabled and cluster connections are encrypted.

Γä╣∩╕Å  Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  k3XHvWTpMrRFtZ0bAzIb

Γä╣∩╕Å  HTTP CA certificate SHA-256 fingerprint:
  f126cdfbe59d6efc25e3ead5f07ae7e5221abfa75dd35d2aeeb9436716483147

Γä╣∩╕Å  Configure Kibana to use this cluster:
ΓÇó Run Kibana and click the configuration link in the terminal when Kibana starts.
ΓÇó Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjYuMSIsImFkciI6WyIxNzIuMzEuMzEuMTQ1OjkyMDAiXSwiZmdyIjoiZjEyNmNkZmJlNTlkNmVmYzI1ZTNlYWQ1ZjA3YWU3ZTUyMjFhYmZhNzVkZDM1ZDJhZWViOTQzNjcxNjQ4MzE0NyIsImtleSI6IkdBYkZfSVVCaXdGeC1CaWhSWE1XOkFiUmlrZnp2U3ZLUGFEQ29WZWl2LWcifQ==

Γä╣∩╕Å  Configure other nodes to join this cluster:
ΓÇó On this node:
  Γüâ Create an enrollment token with `bin/elasticsearch-create-enrollment-token -s node`.
  Γüâ Uncomment the transport.host setting at the end of config/elasticsearch.yml.
  Γüâ Restart Elasticsearch.
ΓÇó On other nodes:
  Γüâ Start Elasticsearch with `bin/elasticsearch --enrollment-token <token>`, using the enrollment token that you generated.
```


- When starting Elasticsearch for the first time, security features are enabled and configured by default. The following security configuration occurs automatically:

- Authentication and authorization are enabled, and a password is generated for the elastic built-in superuser.
- Certificates and keys for TLS are generated for the transport and HTTP layer, and TLS is enabled and configured with these keys and certificates.
- An enrollment token is generated for Kibana, which is valid for 30 minutes.

## Step 4.2 - Console Logs

- By default Elasticsearch prints its logs to the console (STDOUT) and to the <clustername>.log file within the logs directory.

- Elasticsearch logs some information while it is starting, but after it has finished initializing it will continue to run in the foreground and won’t log anything further until something happens that is worth recording. 

- While Elasticsearch is running you can interact with it through its HTTP interface which is on port 9200 by default.

- Open another instance of cmd, where we can check the functionality of ElasticSearch that has been installed.

- We can test that our Elasticsearch node is running by sending an HTTPS request to port 9200 on localhost:


# Step 5 - Testing ElasticSearch Installation Using a Curl Command


Open another instance of cmd, where we can check the functionality of ElasticSearch that has been installed using the curl command below.


```
curl --cacert %ES_HOME%\config\certs\http_ca.crt -u elastic https://localhost:9200 --insecure

```

- Here is the response of the curl command which gives a lot of details about the version of elasticsearch, clustername and a lot more details.


```
C:\Users\Administrator\Downloads\elasticsearch-8.6.1-windows-x86_64\elasticsearch-8.6.1>curl --cacert %ES_HOME%\config\certs\http_ca.crt -u elastic https://localhost:9200 --insecure
Enter host password for user 'elastic':
{
  "name" : "EC2AMAZ-6ACTCAV",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "BCOAmYZAS36vgypuOnsYpQ",
  "version" : {
    "number" : "8.6.1",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "180c9830da956993e59e2cd70eb32b5e383ea42c",
    "build_date" : "2023-01-24T21:35:11.506992272Z",
    "build_snapshot" : false,
    "lucene_version" : "9.4.2",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}

```

## Step 5.1 - Similar to the curl command, we can as well use the browser to check on https://localhost:9200 to check if we get the same JSON response

```
https://localhost:9200

```

- Tyype in username - elastic and password- from the output of elasticsearch installation. Here is the response from the browser

```
{
  "name" : "EC2AMAZ-6ACTCAV",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "BCOAmYZAS36vgypuOnsYpQ",
  "version" : {
    "number" : "8.6.1",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "180c9830da956993e59e2cd70eb32b5e383ea42c",
    "build_date" : "2023-01-24T21:35:11.506992272Z",
    "build_snapshot" : false,
    "lucene_version" : "9.4.2",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```


# Step 6: Installation Successful

We now have a Single node Elastic Cluster setup on a AWS EC2 windows machine with the default configurations.