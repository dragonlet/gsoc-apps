Template-based Initialization of Amazon EC2 Services
====================================================

Basics
------

  - Name: Clarence Leung
  - E-mail: clarence.leung@mail.mcgill.ca

Project Description
-------------------

The goal of this project is to provide a simple interface in which users that wish to initialize an Amazon EC2 instance for Imaging Middleware applications, given particular parameters, can do so in a simple JSON-template based manner, or through some external client.  Parameters to consider for the template include the name of the instance, type of the instance, scripts to run on startup, DNS settings, and more.

This project will be separated into three major parts, a Python-based general CLI client, an Eclipse plugin to simplify template entry, and a web interface.

We first discuss an example template to be used, the JSON-formatted object to be send and parsed by our API, and how these core parameters are to be implemented.  The key information to be specified by the user is as follows:

  - AMI: The image to be used
  - Instance Name: The name of the instance, defined by EC2 tags
  - Instance Type: The type of the instance, defining the performance
  - Startup Sequence: When the sequence is to be launched
  - Configuration Script: Shell script to be executed on the new instance
  - DNS: Domain name by which this instance will be referred

Optional parameters can also be provided by the user, but these are the key ones that must be implemented.  A sample JSON object that encapsulates this data can be as follows:

`
{
    "instances": [
        { 
            "sequence" : 1 ,
            "AMI" : "some_ami" ,
            "name" : "app1" ,
            "type" : "t1.micro" ,
            "script" : "start_app1.sh" ,
            "DNS" : "app1.cci.emory.edu"
        } ,
        { 
            "sequence" : 2 ,
            "AMI" : "some_ami" ,
            "name" : "app2" ,
            "type" : "t1.micro" ,
            "script" : "start_app2.sh" ,
            "DNS" : "app2.cci.emory.edu"
        }
    ]
}
`

For each of this parameters, we now shortly describe how we can implement setting them on an instance launch:

  - Startup Sequence: We can simply sort the inputted data by sequence number, and then synchronously send the data to the API, waiting for a successful instance launch before launching the next one.
  - AMI, Instance Type: Available in the `RunInstances` API call
  - Instance Name: Available in the `CreateTags` API call
  - Configuration Script: We can send the name of the script to be run through the `user-data` parameter, and configure the AMI to run that script on boot.
  - DNS: Registering the domain name using Amazon Route 53 is probably the easiest way to manage our instances in this method.

We now provide example use cases of each of the three interfaces above that we have discussed.

Command line usage will be the most simple.  We will have a command line tool that takes a JSON file, which will appropriately call the AWS API as needed.  Usage will simply be of the form:

`$ ec2-template [JSON FILE]`

With optional flags that can be specified to change around parameters.

The Eclipse plugin will require porting the Python code over to Java.  Once that is done, we can just open up a small window where users can input the desired parameters as needed, which will then call the API.  We can also have the formatted data be written to a JSON file formatted in the above manner if needed.

Finally, the web interface can simply be a wrapper around the Python command line tool.  We provide a form where users can login, and then enter parameters as needed through an HTML based form.  The form will have JavaScript that converts the form parameters into the desired JSON object, which is sent to the backend containing a reworked version of the CLI tool, and executed.

Mentor Discussion and Expectations
----------------------------------

I have previously spoken with the mentor in charge of this project, Mr. Yusuf Nadir Saghar.  I would like him to provide me with possible real life use cases in order to help me prioritize which optional parameters should be implemented the earliest.  Also, although I have experience working with Amazon AWS in a professional capacity, I am hoping that Mr. Saghar can help me fine tune my work for researchers to use in an academic setting, as well as helping me simplify the interfaces to make the project be as easily usable as possible.  I would like to see my work be used as early as possible, so I am hoping he can help me find actual users to use the software I have created.

Languages, Libraries, and Testing Strategies
--------------------------------------------

The following languages will be used:

  - Python (CLI tool)
  - Java (Eclipse plugin)
  - JavaScript (web interface)

The following applications and libraries will be used:

  - boto (Python interface to AWS)
  - AWS SDK for Java (Java SDK for AWS)
  - Eclipse SDK (SDK for developing Eclipse plugins)
  - Django (Python web framework to develop the web interface)
  - jQuery (JavaScript library to handle HTML interactions)

The following testing libraries and techniques will be used:

  - unittest module in Python
  - jUnit framework for Java

Unit tests will be designed ahead of time based on actual use cases provided by the mentor, and more will be designed and implemented as coding proceeds.  Interface testing should be performed by actual users, which will also aid in developing new features for the project.

Deliverables (Timeline)
-----------------------

The timeline for Google Summer of Code 2012 is from April 20 to August 20.  The following calendar is proposed as a guideline for the project.

  - April 20 - April 27:  Receive real-life use cases from mentor and develop designs for unit test cases before any coding commences.

  - April 28 - May 5:  Note down all API calls that are necessary to perform the actions required for the base template parameters.  Begin implementation of the Python command line tool, using boto, for this task.  If the API calls are not available in boto, access the API directly.

  - May 6 - May 27:  Work on Python CLI tool, implementing all core functionality needed for the base parameters given above.  Design and implement unit tests to test the tool throughout coding.  

  - May 28 - June 10:  Discuss with mentor about optional parameters that should be implemented and considered.  Begin implementation of at least 5 other optional parameters that users may consider important.

  - June 11 - July 1:  Begin porting of code to Java to begin Eclipse plugin implementation.  A full Java implementation should be complete at the end of this time period.

  - July 1 - July 22:  Develop front-end of the Eclipse plugin, and unit tests to make sure it works.  Work with mentor to make sure interface is acceptable for users.

  - July 23 - July 30:  Begin setting up a server to wrap Python CLI tool around through a web interface.  It should be possible to send the JSON object via cURL at the end of this time.

  - July 31 - August 20:  Complete a front-end web interface, along with authentication system, for the project using Django.  The interface should be clean and easy to understand for the end user.  Work with mentor to test if product can be used in actual work at Emory University.

Qualifications
--------------

I am a second-year Biology and Computer Science undergraduate student at McGill University with experience deploying non-relational databases (particularly MongoDB and Redis) for professional and organizational use.  I currently maintain several Amazon EC2 instances for several organizations in Montreal, and am familiar with the API and have written Python and shell scripts to access it.  I have worked as a lead developer on the following research and open-source projects, particularly playing a large role in scalability and deployment:

  - [Wikinotes](http://beta.wikinotes.ca) - A Django-based collaborative learning site for students at McGill University
  - [Phylo](http://phylo.cs.mcgill.ca) - A crowdsourced Flash game for sequencing phylogenetic data
  - [Phylo-MCMC](http://github.com/clarle/phylo-mcmc) - MCMC algorithms for predicting genetic sequences (unrelated to the above Phylo)
  - [Sunlight Labs API](http://services.sunlightlabs.com) - A Node.js client library for the government data APIs of Sunlight Labs
  - [Django Slides](http://github.com/clarle/django-slides) - A Django-based application for easily integrating JavaScript slideshows into Django projects

I cannot provide specifics into the APIs developed for professional organizations due to non-disclosure agreements, but references can be provided upon request.

I am also a consistent partcipant in Montreal hackathons, and have won the Back-To-School Hackathon (with Wikinotes) and Hacking Health (with TextRX).

Other Commitments
-----------------

I will continue to be assisting with development on Phylo over the summer, but only in an advisory role for the new developers.  Beyond this commitments, I will be free to pursue development on this project full-time.
