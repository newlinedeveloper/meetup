### Elastic Machine Learning Demo - Global AI Bootcamp Meetup

##### Presenting by Veerasolaiyappan - Fullstack developer

![profile](./presentation-profile.png)


#### Prequestics

**Elastic cloud Account**

```
https://cloud.elastic.co/registration

```



#### Steps to find out Anomaly Detection in Elastic machine learing

##### step 1 : Sign up for an Elastic Cloud account

If you don't already have an Elastic Cloud account, sign up for one on the Elastic Cloud website.

###### Account creation 

![Elastic cloud registration](./elastic-registration.png)

###### login

![Elastic cloud login](./login.png)

##### step 2 : Create an Elasticsearch cluster

In the Elastic Cloud console, create an Elasticsearch cluster. You can choose the size, location, and other parameters of your cluster based on your needs and budget


###### Create deployment

![Create deployment](./create-deployment.png)




###### Machine learning node Autoscaling configuration

![Create deployment](./create-deployment.png)

![Select service provider](./select-cloudprovider.png)

![Enable Autoscaling](./autoscaling-configure.png)

###### Deployment completion

![Deployment Completion](./deployment-complete.png)


##### step 3 : Enable machine learning

Once your Elasticsearch cluster is created, you can enable machine learning by going to the Kibana tab in the Elastic Cloud console and clicking on the "Machine Learning" button



###### Kibana Dashboard 

![Kibana Dashbaord](./view-dashboard.png)


###### Machine learning section
![Machine Learning section](./machine-learning-overview.png)


##### step 4 : Ingest sample data

Elastic Cloud provides sample data sets that you can use to test and demonstrate the capabilities of Elastic machine learning. In Kibana, go to the "Machine Learning" tab, click on "Data Visualizer", and select "Sample data" to ingest a sample data set.


###### View all sample dataset
![Select sample dataset](./select-dataset.png)


###### Select Ecommerce sample dataset
![Select ecommerce dataset](./select-ecommerce-dataset.png)



##### step 5 : Create an anomaly detection job

 In Kibana, create an anomaly detection job using the sample data set by specifying the data source, selecting the machine learning algorithm, and setting the analysis parameters

###### Create job
![create job](./create-anomaly-job.png)

###### View job
![view job](./view-job.png)

##### step 6 : Train the model

Once the anomaly detection job is configured, train the machine learning model on the sample data set.


###### Train job
![Train job](./train-models.png)

##### step 7 : Review the results

After the model is trained, review the results in Kibana. The anomaly detection job will flag any data points that are considered anomalous based on the model's analysis.


###### Anomaly detection details

![Anomaly detection](./anomaly-detection-view.png)

![Anomaly detection 2](./anomaly-detection-2.png)

![Anomaly detection 3](./anomaly-detection-3.png)



##### step 8 : Take action

Finally, take action on the anomalous data points, such as investigating the root cause of the anomaly, alerting stakeholders, or triggering automated responses.



