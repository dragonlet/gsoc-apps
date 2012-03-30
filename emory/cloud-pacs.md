Cloud Based Research PACS
=========================

Basics
------

  - Name: Clarence Leung
  - E-mail: [clarence.leung@mail.mcgill.ca](mailto:clarence.leung@mail.mcgill.ca)

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

The timeline for Google Summer of Code 2012 is from April 20 to August 20.  The following calendar is proposed as a guideline for the project.

  - April 20 - April 27: Receive real-life use cases from mentor and develop designs for unit test cases before any coding commences.
  - April 28 - May 5: Propose a design sharding setup for the MongoDB instances, begin coding on the Python backend. 
  - May 6 - May 27: Work on code for the Python backend, testing with unit tests throughout the way.
  - May 28 - June 10: Begin deployment of the system on Amazon EC2 instances, and begin testing of the system in concurrency and query performance with sample data.
  - June 11 - July 1: Continue testing of system and continue to scale the amount of sample data inserted into the database until it reaches an amount similar to that of an actual use level.
  - July 1 - July 22: Begin comparison testing between the system and existing PACS systems such as DCM4CHEE. 
  - July 23 - 29: Perform a detailed quantitative analysis of the performance comparisons and write a corresponding report on that data.
  - July 30 - TBA: Begin actual deployment and usage of the system.
  - July 30 - TBA: Collect feedback from actual users and continue to maintain the system, or add improvements.  Additional tasks that are suggested during the project's development can be completed during this time as well.
  - April 20 - August 20: Provide a detailed writeup of testing progress, qualitative benefits of the PACS, and quantitative analysis of the PACS. 

Qualifications
--------------

I am a second-year Biology and Computer Science undergraduate student at McGill University with experience deploying non-relational databases (particularly MongoDB and Redis) for professional and organizational use.  I have worked as a lead developer on the following research and open-source projects, particularly playing a large role in scalability and deployment:

  - [Wikinotes](beta.wikinotes.ca) A Django-based collaborative learning site for students at McGill University
  - [Phylo](phylo.cs.mcgill.ca) - A crowdsourced Flash game for sequencing phylogenetic data
  - [Phylo-MCMC](github.com/clarle/phylo-mcmc) - MCMC algorithms for predicting genetic sequences (unrelated to the above Phylo)
  - [Sunlight Labs API](services.sunlightlabs.com) - A Node.js client library for the government data APIs of Sunlight Labs
  - [Django Slides](github.com/clarle/django-slides) - A Django-based application for easily integrating JavaScript slideshows into Django projects

I am also a consistent partcipant in Montreal hackathons, and have won the Back-To-School Hackathon (with Wikinotes) and Hacking Health (with TextRX).

Other Commitments
-----------------

I will continue to be assisting with development on Phylo over the summer, but only in an advisory role for the new developers.  I also may be taking a single course over the summer, but it will only be for a single month in the month of May.  Beyond these two commitments, I will be free to pursue development on this project full-time.
