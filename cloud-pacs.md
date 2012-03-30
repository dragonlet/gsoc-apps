Cloud Based Research PACS
=========================

Basics
------

  - Name: Clarence Leung
  - E-mail: clarence.leung@mail.mcgill.ca

Project Description
-------------------

A Python-based backend system will be designed and implemented for populating a MongoDB database with DICOM metadata, and the DICOM image itself, as a GridFS instance.  The system will be composed of the following three parts, each launched as an Amazon EC2 instance:

  - A load balancer (implemented with HAProxy)
  - Application nodes (the Python backend)
  - Database nodes (the MongoDB shards)

This system is designed with concurrent access and data scalability as a priority.  Sharding techniques are used to distribute the MongoDB database over several EC2 instances, and load balancing is performed to allow for large-scale simultaneous access of the system.  

Scaling the system horizontally is as simple as launching a new EC2 instance of an application node and/or a database node, and adjusting the load balancer as needed.  

Other priorities of this project include the security and reliability of the system.  IP restrictions will be set on the EC2 instances to prevent external access of the system, and user-level authentication will be set on the MongoDB instances to only allow specific access to data by certain users.  Document validation will be performed on any document insertion or update, to make sure there is no corrupt data on failed transactions.  Further document validation can be performed via the Python backend; however, as a goal of the project is to allow for dynamic document metadata, we will limit the validation we perform to the base DICOM format.

A comparison of the project to existing PACS implementations, such as DCM4CHEE, will be performed on an ongoing basis through the development of the project. The standard parameters of query performance, data storage size, ease of migration, hardware utilization, resource control and diagnostics, and more.  However, the main parameters we will be considering in all cases will be those of scalability and concurrency.

Testing will be performed using the standard MongoDB performance testing suite, mongo-perf.  Load testing will be performed with ApacheBench, and testing of the Python backend will be performed with custom unit tests written using the unittest module.

Mentor Discussion and Expectations
----------------------------------

I have previously spoken with the mentor in charge of this project, Dr. Ashish Sharma.  I would like for him to provide me with actual use cases of this project, so I can more easily deploy the project into production use as soon as possible.  Having constant feedback on the project as I continue to work on it will be of great use in the coding process. 

Languages, Libraries, and Testing Strategies
--------------------------------------------

The following languages will be used:

  - Python (backend language)
  - Bash (rapid deployment of additional nodes)
  - C++ (likely unnecessary, but if additional lower-level testing is required, C++ is easier to integrate with mongo-perf)
  - R (analysis of performance testing data)

The following applications and libraries will be used:

  - MongoDB - open source and scalable NoSQL database
  - PyMongo - recommended driver for Python and MongoDB
  - HAProxy - load balancer for application instances
  - ec2-ami-tools - CLI tools for accessing and manipulating EC2 instances 
  - git - version control to keep track of coding progress

The following testing libraries and techniques will be used:

  - unittest module in Python
  - mongo-perf and mongostat to test database performance
  - ApacheBench to test load concurrency

Deliverables (Timeline)
-----------------------

Qualifications
--------------

Other Commitments
-----------------
