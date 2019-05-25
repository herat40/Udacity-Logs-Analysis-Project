# Udacity-Logs-Analysis-Project
It is the first project in Udacity's Full Stack Web Developer Nano-degree program.


## Project Description:

You've been asked to build an internal reporting tool that will use information from a database for a newspaper site to discover what kind of articles the site's readers like. The database contains newspaper articles, as well as the web server log for the site. The log has a database row for each time a reader loaded a web page. Using that information, your code will answer questions about the site's user activity.

The reporting tool is a Python program using the psycopg2 module to connect to the database. The code must use only one single SQL query to answer each question. We are going to answer the following questions:

What are the most popular three articles of all time?
Who are the most popular article authors of all time?
On which days did more than 1% of requests lead to errors?

### Requirements:

[Python3](https://www.python.org): The code is using python version 3.7.1.     
[Vagrant](https://www.vagrantup.com): Tool for building and managing virtual machine environments.   
[VirtualBox](https://www.virtualbox.org): Open source virtualization software.


### Steps To Run The Code:

1. Download and install the latest version of [Python](https://www.python.org).
2. Download and install [Vagrant](https://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
3. Download the data provided by Udacity [here](https://d17h27t6h515a5.cloudfront.net/topher/2016/August/57b5f748_newsdata/newsdata.zip). You will need to unzip this file after downloading it. The file inside is called newsdata.sql. Put this file into the vagrant directory, which is shared with your virtual machine.
4. Navigate to the /Vagrant folder and use vagrant up to bring the virtual machine online and vagrant ssh to login.
5. The command line will show Vagrant which means you are connected to the virtual machine. Change directory to /vagrant. This folder is on your virtual machine.
6. Load the database using psql -d news -f newsdata.sql.
7. Connect to the database using psql -d news.
8. Create views that are given below.
9. Run the python file project.py

### Views For Question 3:

CREATE VIEW logstat AS       
SELECT count(*) as stat,            
status, cast(time as date) as day             
FROM log WHERE status like '%404%'           
GROUP BY status, day           
ORDER BY stat desc limit 3;

CREATE VIEW allvisitors AS     
SELECT count(*) as visitors,      
cast(time as date) as errortime        
FROM log     
GROUP BY errortime;       

CREATE VIEW errorcount AS       
SELECT * from logstat join allvisitors       
ON logstat.day = allvisitors.errortime;      
