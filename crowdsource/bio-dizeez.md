Biological Games: Asymmetric Version of Dizeez
==============================================

Biography
---------

  - Name: 
       * Clarence Leung
  
  - E-mail: 
       * [clarence.leung@mail.mcgill.ca](mailto:clarence.leung@mail.mcgill.ca)

  - Education:
      * B.Sc. Joint Biology and Computer Science
      * McGill University, Montreal, QC, Canada

Internet Presence
-----------------

  - [GitHub](http://github.com/clarle)
  - [Google+](https://plus.google.com/114176550515061560911/)
  - [Facebook](http://www.facebook.com/clarle)


Known Programming Languages
---------------------------

  - Python (Advanced)
    * Specializations: NumPy/SciPy, Cython, Django
  - JavaScript (Advanced)
    * Specializations: jQuery, d3.js, node.js
  - C (Intermediate)
    * Specializations: Python/node.js modules and bindings
  - Bash (Intermediate)
  - Java (Intermediate)
  - Scala (Beginner)
 
Interests
---------

I have two major interests as a coder, bioinformatics and web development.
My specializations in the two fields are as follows:
  
  - Bioinformatics
    * Phylogenetic sequencing
    * Machine learning predictions
  - Web development
    * REST API design
    * Distributed computing and database scaling
    * User experience
 
Goals for the summer
--------------------

I hope to learn to design and implement more responsive client-side interfaces, that make users not notice the difference between a web application and a regular desktop-based application.  As well, I am interested in learning more about current difficult problems in biology, and how crowdsourcing may be able to provide better solutions than algorithmic techniques in some cases.

Other commitments this summer
-----------------------------

I was a lead developer on Phylo: A Human Computing Framework for Comparative Genomics last summer, one of the more well-known crowdsourced biological games.  I will likely take an advisory role this summer to help the new developers, which is currently my only commitment.  Other than that, I can work on the Google Summer of Code project full-time.

Project Plan
------------

### Summary (User Interface)

We will develop Dizeez (asymmetric) in the following manner.  From Phylo, I have had the experience of not having enough people online at a single time to develop a truly live form of multiplayer, so I created an asynchronous multiplayer mode (similar to that of Words With Friends), where two players do not be online at the same time to still be able to play the game.

Players can log in through our service to keep track of their score.  Players then have two options: setting themselves as being "available" for challenges, or browsing the players that are currently "available" to be challenged.  

If a player decides to set themselves as being available for challenges, any other player can browse through the list of available players, and send a Dizeez challenge to them.  Alternatively, a player can also challenge a player with a specific username as well.  

Once a challenge begins, each player is randomly assigned a role.  If a player is chosen as the disease namer, they are given a disease and genes to name the disease with.  The other player waits until the first player has finished.  Note that this happens asynchronously, such that games like these may take place over a period of several days.  If there is a correct guess between Player 1 and Player 2, both players will get points, which will persist in their user score.

### Summary (Technical)

A database is necessary to keep persistent data such as this, and a standard choice such as MySQL is fine.  Users must create user accounts, which store their username, a hashed password, their current Dizeez score, and other information inside the database.  A sample JSON object that encapsulates the user data could be:

'
{  
  id: "Integer: User ID number",
  name: "String: Desired username of the user",
  password: "String: Hashed version of password",
  email: "String (optional): E-mail to reset account if password forgotten",
  games_played: "Integer: Total number of games played",
  points: "Integer: Total number of Dizeez points"
}
'
   
To keep track of the games, we can keep track of the data for each game inside the database as well.  A sample JSON object that encapsulates the game data could be:

'
{
  id: "Integer: Game ID number",
  round: "Integer: Round number of the game",
  namer: "Integer: User ID number of the person naming related genes",
  guesser: "Integer: User ID number of the person guessing the disease",
  points: "Integer: Number of points the players have collectively scored",
  disease: "String: Current disease to be guessed by the players",
  genes: "Array(String): List of genes that the namer has chosen",
  complete: "Boolean: True/False value as to whether the game has finished"
}
'

These are the bare minimum parameters that are needed to build our game.  We switch around the namer and guesser parameters at each round.  This JSON data can be sent to the players and used to construct our views for the actual interface.

When a player reaches their dashboard, this sends an AJAX call to the Python backend, which queries the database for all existing games that the player is found in.  The view is constructed using the returned JSON data, which is formatted in a way similar to the above.  We update the HTML using client-side JavaScript techniques, which can be done with simple jQuery selectors.

For the game logic itself, we can simply build on top of the existing Dizeez game.  It seems most of it is simply complete, although I believe we can create a better interface than the current Twitter Bootstrap interface as well.

Timeline
--------

The timeline for Google Summer of Code is from April 20 to August 20.  The following calendar is proposed as a guideline for the project.

  - April 20 - April 27: 
    * Get to know the existing Dizeez code, and design and develop unit test cases for the project to come.

  - April 28 - May 5: 
    * Design and setup the MySQL database for persistent data.  Any system administration tasks to prepare the development/production environment should be done in this time.

  - May 6 - May 27: 
    * Develop the REST-based server for the backend, to transmit the JSON data that will be passed from server to client.

  - May 28 - June 10: 
    * Begin developing the HTML/CSS/JS game client.  Game browsing should be complete at the end of this timeframe.

  - June 11 - July 1: 
    * Continue development on the HTML/CSS/JS game client.  The actual gameplay should be complete at the end of this timeframe.

  - July 2 - July 22: 
    * Begin testing of all aspects of the game.  Certain portions of the game should be available for beta testing at this point.

  - July 23 - July 30: 
    * Setup mail server, application proxies, and any other production necessary steps for actual launch of the game.

  - August 1 - August 20: 
    * Deploy the game for playing, and fix any bugs that users may detect in the meantime.

Qualifications
--------------

I am an undergraduate Joint Computer Science and Biology Student at McGill University, with significant experience working on biological games, and specifically multiplayer aspects of those games.

My main qualification is that I was a lead developer on the Flash version of [Phylo: A Human Computing Framework for Comparative Genomics](phylo.cs.mcgill.ca) the previous summer, and part of the job was to implement an asynchronous multiplayer aspect to the game, which was done with the new Challenges mode.

Although the game itself is written in Flash/ActionScript 3.0, I am also a capable Python and JavaScript developer, having written several modules for Python and Node.js, as well as having done extensive jQuery work.

I also have a large amount of experience working with others on open source projects, some of them published as modules in PyPI or NPM.  Several notable ones are listed below:

  - [Wikinotes Framework](http://beta.wikinotes.ca)
      * A Git-based wiki for student courses developed using Django
      * Deployed in production with nginx and gunicorn
      * Actively used by students at McGill University

  - [Node Sunlight API](https://github.com/clarle/node-sunlightapi)
     * A Node.js client library for the Sunlight Labs Congress API
     
  - [Django Slides](https://github.com/clarle/django-slides)
     * A Django application to easily apply jQuery slideshows to templates

  - [Bayesian Models for Phylogenetic Trees](https://github.com/clarle/phylo-mcmc)
     * Implementation of Monte Carlo Markov Chain (MCMC) statistical algorithms for phylogenetic tree analysis
     * Written in Cython and the NumPy/SciPy scientific computing libraries

I am also a regular participant at hackathons in Montreal, and have won two so far, the Back-To-School Hackathon (won with the Wikinotes Framework) and Hacking Health (won with TextRX).

As well, I have done significant amounts of web development work for businesses and organizations in Montreal, particularly in developing REST APIs.  References for these can be provided upon request.

Project Interest
----------------

With many biological problems being NP-complete, they are not easy to solve algorithmically, and methods such as randomized and approximation algorithms are often necessary to solve them.  However, crowdsourcing is also a significant way to provide solutions to these difficult problems, that not too many people have explored as of yet.

I believe that crowdsourcing is important in both solving these problems, and introducing the average person to the latest in cutting-edge science.  As the web continues to grow, and browser-based web applications become more powerful, this is a good time to get people interested in science, through gaming.

Technically, the problem interests me as well, as I am interested in the latest in web development and user interface design, particularly as HTML5 and WebSockets become more popular in the community.  I hope to continue to develop better web applications in the future, and I'm hoping that this Google Summer of Code project can help me refine my skills to create even more complex things in the future.
