# Table of Contents
* [About TableTop Manoa](#about-tabletop-manoa)
* [User Guide](#user-guide)
* [Developers Guide](#developers-guide)
  * [Downloading and Installation](#downloading-and-installation)
  * [Application design](#application-design)
    * [Directory structure](#directory-structure)
    * [Import conventions](#import-conventions)
    * [Naming conventions](#naming-conventions)
    * [Data Model](#data-model)
    * [CSS](#css)
    * [Routing](#routing)
    * [Authentication](#authentication)
    * [Authorization](#authorization)
    * [Configuration](#configuration)
  * [Quality Assurance](#quality-assurance)
    * [ESLint](#eslint)
    * [Data model unit tests](#data-model-unit-tests)
    * [JSDoc](#JSDoc) 
    * [Quality Assurance](#quality-assurance)
    * [Initial User Studies](#initial-user-studies)
  * [Meteor Hosting](#meteor-hosting)
* [Development History](#development-history)
  * [Milestone 1: Mockup development](#milestone-1-mockup-development)
  * [Milestone 2: Data model development](#milestone-2-data-model-development)
  * [Milestone 3: Connect UI to data model](#milestone-3-connect-ui-to-data-model)

  
## About Tabletop Manoa

Tabletop Manoa is an application designed to allow those in the UH community to coordinate and join in various tabletop games. The ability to do this will enable students to get together in a safe environment for fun and socialization as they play in games ranging
from Monopoly and Spades to WarMachine and Pathfinder.

# User Guide

## Landing Platform
This is the only page accessable to the public. This page tells the user what the website is about, and provides a login. Anyone with a UH account can login with the login button
<img src="../projectImages/landingPage.jpg">


## Login Page
Access granted only to students. Allows students comfort in knowing the general demographic of the other players
![image](https://cloud.githubusercontent.com/assets/17040099/24215014/7f8513f6-0edb-11e7-9885-ae784b995aca.png)


## Home Page
Welcome for users and instructions
![image](https://cloud.githubusercontent.com/assets/17040099/25884681/e1b43360-34ef-11e7-904d-0183efdc41b0.png)


## Manage Games
Displays information of games the user is coordinating, along with any game the user is joining in. The games the user signed to attend in also has the option for the user to cancel.
![image](https://cloud.githubusercontent.com/assets/17040099/25884951/6839787c-34f1-11e7-9f4f-4daa6633f0b1.png)

## Coordinate a Game
Allows a student to set up their own games. The games are sorted into 4 categories the user will choose from.
![image](https://cloud.githubusercontent.com/assets/17040099/25885046/ee5b1974-34f1-11e7-8d01-7f221f29c3a5.png)

The user will be fill out the rest of the table, to include any extra notes.
![image](https://cloud.githubusercontent.com/assets/17040099/25885153/8e288ffe-34f2-11e7-88d9-4222777aa332.png)

Once successful, a confirmation notice will appear.
![image](https://cloud.githubusercontent.com/assets/17040099/25885165/a17ef9f8-34f2-11e7-8cc4-a52eda030614.png)

## Calendar
Calendar shows all games planned in the month. Allows user to browse by date. 
![image](https://cloud.githubusercontent.com/assets/17040099/25885276/50d26bce-34f3-11e7-97db-78690a69b5cd.png)

If the item on the calendar is selected, a notice about the information will pop up.
![image](https://cloud.githubusercontent.com/assets/17040099/25885305/743aeafa-34f3-11e7-8efb-fdb6ba302579.png)

## Browse Games 
Four main categories of the games allows users to select all. Games that are from the selected categories will be filtered. Selecting the game will give detailed information on the game, and the user can join in on the game, which will track the amount of people signed up.
![image](https://cloud.githubusercontent.com/assets/17040099/25885241/230e6c60-34f3-11e7-9319-82279e8691d1.png)

## More Information
This page will show all the additional information about the game. If the user chooses to join the game, the option is also available on this page.
![image](https://cloud.githubusercontent.com/assets/17040099/25885369/b5a56b64-34f3-11e7-814b-779a9f80d5e5.png)


# Developers Guide
   
## Downloading and Installation
  
First, [install Meteor](https://www.meteor.com/install).

Second, [download a copy of tabletopmanoa](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/), or clone it using git.
  
Third, cd into the app/ directory and install libraries with:

```
$ meteor npm install
```

Fourth, run the system with:

```
$ meteor npm run start
```
  
## Application Design

### Directory structure

The top-level directory structure contains:

```
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```
The configuration files are seperated in the config/ directory from the actual Meteor application in the app/ directory.

The app/ directory will be discussed in depth upon project completion

### Import conventions

Following the Meteor 1.4 guidlines, all the application codes have been filed in the  imports/ directory, with client/main.js and server/main.js used to import the code for the client and server.

Every imports/ subdirectory containing any Javascript or HTML files has a top-level index.js file that is responsible for importing all files in its associated directory.   

The client/main.js and server/main.js are responsible for importing all the directories containing code they need. 
```
client/
  lib/           # holds Semantic UI files.
  head.html      # the <head>
  main.js        # import all the client-side html and js files. 

imports/
  api/           # Define collection processing code (client + server side)
    
  startup/       # Define code to run when system starts up (client-only, server-only)
        
  ui/
    components/  # templates that appear inside a page template.
    layouts/     # Layouts contain common elements to all pages (i.e. menubar and footer)
    pages/       # Pages are navigated to by FlowRouter routes.
    stylesheets/ # CSS customizations, if any.

node_modules/    # managed by Meteor

public/          
  images/        # holds static images for landing page and predefined sample users.
  
server/
   main.js       # import all the server-side js files.
```


### Naming conventions

This system adopts the following naming conventions:

  * Files and directories are named in all lowercase, with words separated by hyphens. Example: accounts-config.js
  * "Global" Javascript variables (such as collections) are capitalized. Example: Games.
  * Other Javascript variables are camel-case. Example: addGame.
  * Templates representing pages are capitalized, with words separated by underscores. Example: Directory_Page. The files for this template are lower case, with hyphens rather than underscore. Example: directory-page.html, directory-page.js.
  * Routes to pages are named the same as their corresponding page. Example: Directory_Page.

  

### Data Model

The TableTop Manoa data model is implemented by two Javascript classes: [GamesCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/GameCollection.js) and [UsertoGamesCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/UserToGamesCollection.js). Both of these classes use a MongoDB collection with the same name and export a single variable (Games and UsertoGames)that provides access to that collection. 

Any part of the system that manipulates the Tabletop Manoa data model imports the Games or UsertoGames variable, and invokes methods of that class to get or set data.

There are many common operations on MongoDB collections. To simplify the implementation, the GamesCollection and UsertoGamesCollection classes inherit from the [BaseCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/base/BaseCollection.js) class.

Both GamesCollection and UsertoGamesCollection have Mocha unit tests in [GamesCollection.test.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/GameCollection.test.js) and [UsertoGamesCollection.test.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/UserToGamesCollection.test.js).

### CSS

The application uses the [Semantic UI](http://semantic-ui.com/) CSS framework. 

The Semantic UI theme files are located in [app/client/lib/semantic-ui](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/tree/master/app/client/lib/semantic-ui) directory. Because they are located in the client/ directory and not the imports/ directory, they do not need to be explicitly imported to be loaded. (Meteor automatically loads all files into the client that are located in the client/ directory). 

Note that the user pages contain a menu fixed to the top of the page, and thus the body element needs to have padding attached to it.  However, the landing page does not have a menu, and thus no padding should be attached to the body element on that page. To accomplish this, the [router](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/startup/client/router.js) uses "triggers" to add an remove the appropriate classes from the body element when a page is visited and then left by the user. 

### Routing

For display and navigation among its four pages, the application uses [Flow Router](https://github.com/kadirahq/flow-router).

Routing is defined in [imports/startup/client/router.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/startup/client/router.js).

TableTop Mana defines the following routes:

  * The `/` route goes to the public landing page.
  * The `/directory` route goes to the public directory page.
  * The `/<user>/profile` route goes to the profile page associated with `<user>`, which is the UH account name.
  * The `/<user>/filter` route goes to the filter page associated with `<user>`, which is the UH account name.


### Authentication

For authentication, the application uses the University of Hawaii CAS test server, and follows the approach shown in [meteor-example-uh-cas](http://ics-software-engineering.github.io/meteor-example-uh-cas/).

When the application is run, the CAS configuration information must be present in a configuration file such as  [config/settings.development.json](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/config/settings.development.json). 

Anyone with a UH account can login and use Tabletop Manoa to create a portfolio.  A profile document is created for them if none already exists for that username.

### Authorization

The landing and directory pages are public; anyone can access those pages.

The profile and filter pages require authorization: you must be logged in (i.e. authenticated) through the UH test CAS server, and the authenticated username returned by CAS must match the username specified in the URL.  So, for example, only the authenticated user `koday` can access the pages `http://localhost:3000/koday/browseGames` and  `http://localhost:3000/koday/manage`.

To prevent people from accessing pages they are not authorized to visit, template-based authorization is used following the recommendations in [Implementing Auth Logic and Permissions](https://kadira.io/academy/meteor-routing-guide/content/implementing-auth-logic-and-permissions). 

The application implements template-based authorization using an If_Authorized template, defined in [If_Authorized.html](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/ui/layouts/user/if-authorized.html) and [If_Authorized.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/ui/layouts/user/if-authorized.js).

### Configuration

The [config]( https://github.com/tabletopmanoa/Tabletop-Manoa-Website/tree/master/config) directory is intended to hold settings files.  The repository contains one file: [config/settings.development.json](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/tree/master/config).

The [.gitignore](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/.gitignore) file prevents a file named settings.production.json from being committed to the repository. So, if you are deploying the application, you can put settings in a file named settings.production.json and it will not be committed.

TableTop manoa checks on startup to see if it has an empty database in [initialize-database.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/startup/server/initialize-database.js), and if so, loads the file specified in the configuration file, such as [settings.development.json](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/config/settings.development.json).  



For development purposes, a sample initialization for this database is in [initial-collection-data.json](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/private/database/initial-collection-data.json).

## Quality Assurance

### ESLint

Tabletop Manoa includes a [.eslintrc](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/.eslintrc) file to define the coding style adhered to in this application. You can invoke ESLint from the command line as follows:

```
meteor npm run lint
```

ESLint should run without generating any errors.  

It's significantly easier to do development with ESLint integrated directly into your IDE (such as IntelliJ).

### Data model unit tests

Tabletop Manoa includes unit tests for the data model. You can invoke them with:

```
meteor npm run test-watch
```

To see the results, visit http://localhost:3100. Here is what a successful run looks like:
 
![image](https://cloud.githubusercontent.com/assets/17040099/25522661/7b8a0e60-2b9f-11e7-87cb-07b122216368.png)

### JSDoc

Tabletop Manoa supports documentation generation with [JSDoc](http://usejsdoc.org/). The package.json file defines a script called jsdoc that runs JSDoc over the source files and outputs html to the ../../https://github.com/tabletopmanoa/tabletopmanoa.github.io/tree/master/jsdocs directory.  When committed, the index.html file providing an overview of all the documentation generate at that point in time is available at [https://github.com/tabletopmanoa/tabletopmanoa.github.io/tree/master/jsdocs](https://github.com/tabletopmanoa/tabletopmanoa.github.io/tree/master/jsdocs). 

## Initial User Studies 

Our initial user studies were performed individually on five separate individuals, who ranged in both computer ability and tabletop knowledge. The users participated in a willing HCI style walkthrough, in which the users were asked to use the application to perform certain tasks. The users were asked to talk through their thought process while they used the application, to allow the survey taker to have a greater idea of where faults in the design might be. Afterwards the users were asked to state their thoughts on using the program and improvements that could be made. Users will be listed as letters to retain anonymity.

### User A:

**Major:** Animal Science

**Relationship to Tabletop Gaming:** Extensive knowledge, plays weekly. 

**Ability to Use Application:** The user was able to navigate through the pages and use them fairly easily. The user was able to add a game they wanted to play to their list and then remove it afterwards. The user was able to create a game but made a notable error, in which she attempted multiple times to complete the form without all required text boxes being filled. It is important to note that the calendar was not finished at the time of this users testing, so she was unable to test this part of the application.

**User Requested Improvements:** The user requested that the required fields of the add page where signified by some marker. The user also requested that there was a a way to gain more information about the games, like who is playing. 


### User B:

**Major:** Travel Industry Management

**Relationship to Tabletop Gaming:** Extensive Knowledge, runs a weekly game, plays frequently.

**Ability to Use Application:** The user was able to log-in and join a game fairly easily. The user had some difficulty finding out how they were supposed to add a game that they wanted to run. After around a minute of looking they were able to find the button. This negative effect of having to search for this button, left them in a poor mood while attempting to use the add game page. 

**User Requested Improvements:** The user was annoyed that the log in required a pop-up. After further questioning, it was revealed that the pop-up had a negative instinctual feel. This user also shared the sentiment that there was not enough information given about the game. The user also requested that an "Add game" button be moved to the navigation menu, so it was more visable. 

### User C:

**Major:** Graduated

**Relationship to Tabletop Gaming:** Has played card games.

**Ability to Use Application:** This user was able to use the application fairly easily, but repeatedly mentioned that they were unsure what a lot of the things mentioned in the application were. He mentioned that the application was a little unfriendly to people who weren't so accustomed to table-top games. He was delighted to use the add game-page after finding out that it included games he was familiar with like monopoly. 

**User Requested Improvements:** This user requested that the sight added more features or images relating to card games or games that normal people might be familiar with. 

### User D:

**Major:** Political Science

**Relationship to Tabletop Gaming:** Avid gamer of various types.

**Ability to Use Application:** This user had no issue navigating the website. He thought the instructions on the home page were useful and the buttons made sense. He believed that the application should expand to include video games, as many college student would be interested in LAN parties. 

**User Requested Improvements:** This user requested that the Role Playing seletion had an edition number dropdown menu. He also suggests that the miniature category have a point level. The Resource block in the Add Game menu was vague, and he recommended being more specific, and removing the requirement that it be a URL, as not all games have an online source. He also requested a delete button, so that the coordinater can cancel the game.

### User E:

**Major:** Nursing

**Relationship to Tabletop Gaming:** Has played chess.

**Ability to Use Application:** This user was a little confused as to all the requirments to coordinate a game. Not being familiar with tabletop games, she was not sure about what kind of information to produce to fill out the form. However, she did find reading the available games in the Browse Game and Info pages easy to understand. 

**User Requested Improvements:** This user requested that the browse game be sorted in chronological order in their categories, and that the time be in 12 hour standard instead of 24 hour. She also did not like the smoking and drinking options within a college environment. She recommended the option of recurring games, and having the first available start time for a game be 0900 instead of 0100.

## Meteor Hosting
Galaxy is a cloud platfom for Meteor apps, based on Docker and AWS cloud infrastructure. This program has a running deployment on the
[Galaxy](https://galaxy.meteor.com/app/tabletopmanoa.meteorapp.com) 

![image](https://cloud.githubusercontent.com/assets/17040099/24992298/5bb9934c-1fbc-11e7-9501-afda2a9d8706.png)

# Development History
The development process for Tabletop Manoa consists of a sequence of Milestones. Milestones consist of issues corresponding to 2-3 day tasks. GitHub projects are used to manage the processing of tasks during a milestone.  

The following sections document the development history of Tabletop Manoa.

## Milestone 1: Mockup Development

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

Once this milestone was complete, the program was deployed on [Galaxy](#meteor-hosting)

## Milestone 2: Data model development

This milestone started on April 13, 2017 and ended April 27, 2017.

The goal of Milestone 2 was to implement the database model: the underlying set of Mongo Collections and the operations upon them that would support the Tabletop Manoa application.  We constructed the data model as a set of Javascript classes. The GamesCollection and UserToGamesCollection classes provide the persistent data structures useful for Tabletop Manoa. 
 
For this milestone, we also created a set of mocha tests for the data model classes. These tests ensured that we can create, manipulate, and delete the data model documents successfully. The record of this test was documented in the [Data model unit tests](#data-model-unit-tests) section above.

Milestone 2 was implemented as [Tabletop Manoa Milestone M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/issues?q=is%3Aissue+milestone%3AM2+is%3Aclosed)::

![image](https://cloud.githubusercontent.com/assets/17040099/25521495/8b37bf6e-2b9b-11e7-95ef-6e45b4765139.png)

Milestone 2 consists of nine issues, and progress is being managed via the [Tabletop Manoa Project M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/projects/2):

![image](https://cloud.githubusercontent.com/assets/17040099/25521464/68319008-2b9b-11e7-9313-a7fea2298224.png)

Each issue was implemented in its own branch, and merged into master when completed:

![image](https://cloud.githubusercontent.com/assets/17040099/25521750/899adc30-2b9c-11e7-9003-0614b1d26aec.png)

Once the database was complete, the program was run through [ESLint](#eslint) to verify that the code conforms to proper formatting standards.

![image](https://cloud.githubusercontent.com/assets/17040099/25522019/48e4d3ac-2b9d-11e7-83c0-bd25c8b74f1a.png)

## Milestone 3: Connect UI to data model

This milestone started on April 27, 2017 and ended May 9, 2017.

The goal of Milestone 3 was to connect the user interface to the underlying data model. This meant that we updated the templates for each page with calls to helper functions, and we created Javascript files for the templates with helper functions.

Milestone 3 was implemented as [Tabletop Manoa Milestone M3](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/milestone/3)::
![image](https://cloud.githubusercontent.com/assets/17040099/25887615/863d82f2-34fe-11e7-87ea-c876a1e743c6.png)

Milestone 3 consisted of 24 issues, and progress was managed via the [Tabletop Manoa Project M3](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/projects/3)
![image](https://cloud.githubusercontent.com/assets/17040099/25887785/2ff2b998-34ff-11e7-98b2-3ee4caf42a73.png)

Each issue was implemented in its own branch, and merged into master when completed:
![image](https://cloud.githubusercontent.com/assets/17040099/25887077/44a44bac-34fc-11e7-8d50-f0fe9061c08a.png)

Once the database was complete, the program was run through [ESLint](#eslint) to verify that the code conforms to proper formatting standards.
![image](https://cloud.githubusercontent.com/assets/17040099/25522019/48e4d3ac-2b9d-11e7-83c0-bd25c8b74f1a.png)

Once this milestone was complete, the program was deployed on [Galaxy](#meteor-hosting). That program can be seen [here](http://tabletopmanoa.meteorapp.com/).
