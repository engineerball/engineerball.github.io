# Google Cloud Platform Fundamental Week 1
## Organization resource hierarchy

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/cloud-folders-hierarchy.png)

## Google IAM
	* IAM **primitive** roles apply across all GCP Services in a project
	* IAM **predefined** roles apply to a particular GCP service in a project
	* IAM **custom** roles let you define a precise set of permissions
		* Service Accounts control server-to-server interaction
## Google VPC

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/1409A16A-4F61-48D5-9009-E93F91785C48.png)

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/11083F94-7CEB-4D0E-9E75-A2469405C97F.png)
## Google Cloud Storage

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/95572CCF-188B-4047-8436-2741AE1147A2.png)

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/E0FE094D-49DA-4323-AA00-A5B7AA6CC31C.png)

## Google Cloud Bigtable
Managed NoSQL, wide-column database  service, for analytics or IoT (same as HBase)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/AC181969-6A9F-474C-94A3-112EE899C94A.png)
	* Scalibility
	* Data encryption
	* Control access with IAM

## Google Cloud SQL and Google Cloud Spanner
Cloud SQL is managed RDBMS
	* offers MySQL and PostgreSQL (beta)  DbaaS
	* Provide replicate data
	* Managed backup
	* Vertical scaling (r&w)
	* Horizontal scaling (read)
	* Security
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/27083991-0D89-4B7C-9F58-815F4D671A37.png)

Cloud Spanner is horizontally scalable RDBMS example financial application
	* String global consistency
	* Managed instances with HA
	* SQL queries
	* Automatic replication

## Google Cloud Datastore
Horizontally scalable NoSQL DB
Use cases: store structured data from App Engine app
Design for backend
Automatic handle sharding
Provide free daily quotas for r&w
Unstructure (NoSQL document like MongoDB)

## Comparing storage options 
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/C0598360-AE82-4277-9CDE-7C14BC263746.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/5741499E-5294-4EDC-B5C4-F07974A6505E.png)

## Google App Engine
* Standard Environment 
	* Easily deploy you application
	* Auto scale
	* Free daily quota
	* Usage based pricing
	* Specific versions of Java, Python, PHP and Go
	* Code running in “Sandbox” 
		* No writing to local files
		* All requests time out at 60s
		* Limits on third-party software
	* Use SDK to deploy with automatic provision and load balancer

* App Engine flexible environment
	* Build and deploy containerize
	* No sandbox 
	* Can access app engine resources
	* Provide health check
	* Let’s you ssh into vm 

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%203.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%204.png)

## Google Cloud Endpoints and Apigee Edge

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/9D5FD4BD-63FD-4501-99A2-6683366F361E.png)
	* Help create and maintain APIs
	* Distributed API management  through an API console
	* Expose your API using RESTful interface
	* Control access and validate calls with JWT and Service API
Apigee
	* control rate limit
	* not be in GCP
	* often use it hen the are “taking apart” a legacy application
	* Apigee Edge to peel off its services one by one, standing up microservices to implement each in turn, until the legacy application can be finally retired.

## Google Cloud Functions
	* Create single-purpose functions that respond to events without a server or runtime
## Google Deployment Manager
	* Provides repeatable deployments
	* Create a .yaml template describing your environment and use Deployment Manager to create resources
	* Can store in version control in Cloud Source repositories
## Summary

![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%206.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%207.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%208.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%209.png)
![](Google%20Cloud%20Platform%20Fundamental%20Week%201/Image%2010.png)