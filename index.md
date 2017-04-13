# Table of Contents
* [About TableTop Manoa](#about-tabletop-manoa)
* [Project Goals](#project-goals)
* [Database](#database)
* [Development History](#development-history)
  * [Milestone 1: Mockup development](#milestone-1-mockup-development)
  * [Milestone 2: DataBase development](#milestone-2-database-development)
* [Installation](#installation-notes)
  
## About Tabletop Manoa

Tabletop Manoa is an application designed to allow those in the UH community to coordinate and join in various tabletop games. The ability to do this will enable students to get together in a safe environment for fun and socialization as they play in games ranging from Monopoly and Spades to WarMachine and Pathfinder.

### Landing Platform
Anyone with a UH account can login with the login button
<img src="../projectImages/landingPage.jpg">


### Login Page
Access granted only to students. Allows students comfort in knowing the general demographic of the other players
![image](https://cloud.githubusercontent.com/assets/17040099/24215014/7f8513f6-0edb-11e7-9885-ae784b995aca.png)


### Home Page
Welcome for users and instructions
![image](https://cloud.githubusercontent.com/assets/17040099/24744263/1f7f18c6-1a4d-11e7-9740-2d0928f52e1b.png)


### Manage Games
If users are following a game, the link will be here. Also would be the information on games they are in charge of.
![image](https://cloud.githubusercontent.com/assets/17040099/24744277/2fbb2ce8-1a4d-11e7-97bb-158c303cdb91.png)

### Coordinate a Game
Allows a student to set up their own games. Would like the 'meeting date' to be similar to the scheduling app on Google Calendar (calendar dropdown, recurrence option with day of week, clock selection)
![image](https://cloud.githubusercontent.com/assets/17040099/24744301/48e1d244-1a4d-11e7-83bb-d420dfd23111.png)
![image](https://cloud.githubusercontent.com/assets/17040099/24744330/632d3346-1a4d-11e7-8a8b-ff0925193261.png)


### Browse Games 
Four main categories of the games allows users to select all. Games that are active (not past their play date) in the selected categories should pop up. Selecting the game will give detailed information on the game (the information filled out from coordinate game) and the user can save the game (which will allow for an email push)
![image](https://cloud.githubusercontent.com/assets/17040099/24744364/828a8fcc-1a4d-11e7-95e0-4201a4f3d449.png)

### Calendar
Calendar shows all games planned in the month. Allows user to browse by date. If overcrowding of events occur, calendar will be separated by category and then game. Initially all games should be shown to prevent the site from looking too 'empty'.
![image](https://cloud.githubusercontent.com/assets/17040099/24744382/93a5dc44-1a4d-11e7-98c8-9d595a8f0e0a.png)




## Project Goals
  * User can browse games by calendar
  * User can browse games by system
  * User can select games to play
  * User can manage selection of games playing
  * User can coordinate own game
  * User can manage games coordinated 
  * A [database](#database) will be created to represent games already scheduled

## Database

### Games Database
 The schema determined to keep the 
 
  * Game ID
  * Creator User ID (Defined by UH)
  * System
  * Reoccuring (true/false)
  * Date
  * Time
  

### Player Database
  * UserID (Defined by UH)
  * Game ID

## Development History
The development process for Tabletop Manoa conformed to [Issue Driven Project Management](http://courses.ics.hawaii.edu/ics314f16/modules/project-management/) practices. In a nutshell, development consists of a sequence of Milestones. Milestones consist of issues corresponding to 2-3 day tasks. GitHub projects are used to manage the processing of tasks during a milestone.  

The following sections document the development history of Tabletop Manoa.

### Milestone 1: Mockup Development

This milestone started on Apr 4, 2017 and ended on Apr 13, 2017.

The goal of Milestone 1 was to create a set of HTML pages providing a mockup of the pages in the system. To simplify things, the mockup was developed as a Meteor app. This meant that each page was a template and that FlowRouter was used to implement routing to the pages.

Mockups for the following four pages were implemented during M1:

<img width="200px" src="../projectImages/landingPage.jpg"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24215014/7f8513f6-0edb-11e7-9885-ae784b995aca.png"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24744263/1f7f18c6-1a4d-11e7-9740-2d0928f52e1b.png"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24744277/2fbb2ce8-1a4d-11e7-97bb-158c303cdb91.png"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24744330/632d3346-1a4d-11e7-8a8b-ff0925193261.png"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24744364/828a8fcc-1a4d-11e7-95e0-4201a4f3d449.png"/>
<img width="200px" src="https://cloud.githubusercontent.com/assets/17040099/24744382/93a5dc44-1a4d-11e7-98c8-9d595a8f0e0a.png"/>


Milestone 1 was implemented as [Tabletop Manoa Milestone M1](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/issues?q=is%3Aopen+is%3Aissue+milestone%3AM1)::

![image](https://cloud.githubusercontent.com/assets/17040099/24991980/51562ab6-1fba-11e7-9803-1e83840daead.png)


Milestone 1 consisted of seven issues, and progress was managed via the [Tabletop Manoa Project M1](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/projects/1):

![image](https://cloud.githubusercontent.com/assets/17040099/24992097/31fb786e-1fbb-11e7-830e-b46fd435465e.png)

Each issue was implemented in its own branch, and merged into master when completed:

![image](https://cloud.githubusercontent.com/assets/17040099/24992142/77364878-1fbb-11e7-8b6e-9ed4bf697330.png)

Once this milestone was complete, the program was deployed on [Galaxy](https://galaxy.meteor.com/app/tabletopmanoa.meteorapp.com) 

![image](https://cloud.githubusercontent.com/assets/17040099/24992298/5bb9934c-1fbc-11e7-9501-afda2a9d8706.png)

## Milestone 2: DataBase development

This milestone started on April 13, 2017 and is scheduled to end on April 25, 2017.

The primary goal of Milestone 2 is to implement the database model: the underlying set of Mongo Collections and the operations upon them that would support the Tabletop Manoa application.  We shall the data model as a set of Javascript classes. The GamesCollection and CategoryCollection classes provide the persistent data structures useful for Tabletop Manoa. Once the database model is complete, testing the database and then connecting the database to the forms will occur. 
 
For this milestone, we will implement a set of mocha tests for the data model classes. These tests will make sure we can create, manipulate, and delete the data model documents successfully. These tests will be documented upon completion.

Milestone 2 is implemented as [Tabletop Manoa Milestone M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/issues?q=is%3Aopen+is%3Aissue+milestone%3AM2)::

Milestone 2 consists of six issues, and progress is being managed via the [Tabletop Manoa Project M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/projects/2):

## Installation Notes: 
First, [install Meteor](https://www.meteor.com/install).

Second, [download a copy of tabletopmanoa](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/), or clone it using git.
  
Third, cd into the app/ directory and install libraries with:

```
$ meteor npm install
```

Fourth, install the calendar

```
$ meteor add rzymek:fullcalendar
```

Fifth, run the system with:

```
$ meteor npm run start
```

