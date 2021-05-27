# Google Cloud Essentials

* GCP well known cloud service provider

* physical infrastructure overview -- basically every CSP does the same basic stuff.

* App Engine is PaaS

## Running Apps With Compute

### App Engine

* no vms needed

* great for initial onboarding

* auto load balancing

* great for websites and mobile apps and line of business

* has standard and flexible environment

### Compute Engine

* more flexible

* flagship service

* often core of compute

* traditional IaaS solution

* can use instance templates

### Standardizing on Kubernetes

* clusters built on Compute Engine

* K8s cluster management

### Cloud Functions

* AWS Lambda 

* JavaScript Functions in node.js wrapper

* HTTP Requests

* Cloud Storage Event

* Pub/sub event

* See more [Docs: Google Functions](https://cloud.google.com/functions/docs/quickstarts)
  * Node.js
  * Python
  * Go
  * Java
  * .Net
  * Ruby
  * PHP

### Lab 2

You’ve been asked to lay the groundwork for one aspect of the new app that relies on code being executed when a message is received from any number of outlets. To do this, you’ll need to establish a Cloud Pub/Sub topic and then create an example Cloud Function that uses the topic as a trigger. Naturally, you’ll need to confirm the Cloud Function has successfully executed.

You’ll need to accomplish the following steps to complete your task: 1. Enable APIs. 2. Create Pub/Sub topic. 3. Create Cloud Function. 4. Publish message on topic. 5. Confirm Cloud Function executed via logs. 6. Trigger directly via the command line. 7. Confirm Cloud Function executed via logs. 8. Send message to topic from command line. 9. Confirm Cloud Function executed via logs.

Note: In addition to the lab mentioned libraries, use the API Library to find and enable the Cloud Build API.

#### Enable Apis

Use the API Library to find and enable the Cloud Pub/Sub API.
Use the API Library to find and enable the Cloud Functions API.
Use the API Library to find and enable the Cloud Build API.

#### Create Pub/Sub topic

From the main console navigation, go to Cloud Pub/Sub.
Click Create a topic.
In the dialog, enter a name greetings for the topic.
Click Create.

#### Create a Cloud Function

* From the main console, go to Cloud Functions.
* Click Create function.
* Configure the function with the following values:
  * Name: la-pubsub-function
  * Trigger: Cloud Pub/Sub
  * Topic: greetings
  * Source code: Inline editor
  * Runtime: Python 3.7

* In the main.py field, enter the following code:

```Python
import base64

def greetings_pubsub(data, context):

    if 'data' in data:
        name = base64.b64decode(data['data']).decode('utf-8')
    else:
        name = 'folks'
    print('Greetings {} from Linux Academy!'.format(name))
```

* Set Function to Execute to greetings_pubsub.
* Click Create.

#### Publish message to topic from console

Click the newly created Cloud Function name.
Switch to Trigger.
Click the topic link to go to the Cloud Pub/Sub topic.
From the Topic page, click Publish Message.
In the Message field, enter everyone around the world.
Click Publish

#### Publish message to topic from command line

In the Cloud Shell, enter the following command:

`gcloud pubsub topics publish greetings --message "y'all"`

After a moment, refresh the log page to confirm the function has executed.

### Lab 3

You’ve been tasked with getting a Windows web server up and running on a Compute Engine instance. To accomplish this, you’ll need to create the appropriate instance, use RDP to set up necessary software, and create a home page to test the server.

You’ll need to accomplish the following steps to complete your task:

1. Create a Compute Engine VM instance
2. Set your Windows password
3. Access RDP.
4. Install the required IIS components.
5. Create an index.html page. 6. View the final page in a browser.

## Securing Cloud Identity

* [Google Cloud Identity](https://cloud.google.com/identity)

* Identity as a Service

* you can use primitives or fine grained

* cloud KMS
  * encrypt them in cloud storage 

* cloud IAP 
  * application level authorization service  (Identity aware proxy)

## Managing Storage and Databases

### Cloud Storage

* basically S3

* BLOB storage

* images, video, audio etc

* auto encryption

* buckets

### Cloud Data Store

* for those non-relational data problems

* NO-SQL

* ACID transactions

* SQL-like "GQL"

* structure
  * kinds -- like tables
  * entity -- like row
  * property
  * key
  * supports optional ancestors and children

* Product catalogs, user profiles ACID transaction

### Cloud SQL

* for those relational data problem

* Fully managed relation database service

* supports PostgreSQL 9.6

* supports MySQL

* supports SQL Server (Microsoft)

* auto replication and back up

* data auto encryption

### Cloud BigTable

* massive non relation table big data problems

* although also NoSQL, different from Cloud Datastore
  * wide column database vs the document database
  * No SQL-like language
  * single key per row

* hundreds of peta bytes

* use cases : graph data, financial data, IoT data, marketing data

### Cloud Spanner

* Fully Managed enterprise grade relational database service

* Cloud Spanner is to CloudSQl AS Cloud BigTable is to Cloud Datastore

### Cloud Memory Store

* fully managed in memory datastore

* Redis

## Big Data

### Big Query 

* Fully Managed data warehouse for big data

* near real-time interactive analysis of massive datasets

* analyze terabytes of data in seconds

* standard sql supported

* storage and computing handled and billed separately

* use cases: real-time inventory, predictive digital marketing, analytical events

### Processing Data with Cloud Dataflow

* fully manage service for creating pipelines to process data

* serverless

* based on Apache Beam

* processes data on multiple machines in parallel

* handles both streaming (live) and batch (archived ) data

* use cases : analytical dashboards, forecasting sales trends, ETL operations

### Cloud Data Proc

* Hadoop Based

* Runs on clusters

* fully managed cluster data processing service

* compatible with Hadoop Spark and Hive

## VPC

* private netowrk with in google cloud network infrastructure

* adds network to Compute engine, Kubernetes Engine, and App Engine(Flex)

* global resource consisting of regional subnets, connected by WAN

* Includes:
  * firewalls
  * routes
  * forwarding rules
  * configuration of IP address 

* two types of VPC creation: auto mode and custom mode

### Load Balancers

## Cutting Edge

### Machine Learning

* cloud AI

* collection of services and APIs deigned to facilitate machine learning

* includes hardware accelerators : TPUs (TensorFlow Processing Units)

* Primary service : Cloud Machine Learning Engine (ML Engine)

* Training

* Prediction

* Data must be stored in an accessible location (Cloud Storage)

### Cloud IoT

* Fully managed service for connecting and managing IoT devices

* devices must be registered

* works with both telemetry(event data) and device state data

* receives and sends to Cloud Pub/Sub topic

* supports HTTP and MQTT protocols for communication

* Highly secure:
  * each device uses JSON Web Tokes for public/private keys
  * supports RSA or Elliptic Curve Algorithm to verify signatures
  * key rotation support
  * access to IoT core controlled by Cloud IAM roles and permissions
* Part of an IoT eco-system with Android Things and Google Beacon

### Data Transfer Option

* Online Transfer -- standard way

* Storage Transfer Service  - From an S3 bucket

* Transfer Appliance -- Kinda like AWS Snowball
