# Table of Contents
* [About TableTop Manoa](#about-tabletop-manoa)
* [Project Goals](#project-goals)
* [Database](#database)
* [Installation](#installation)
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
    * [JSDoc](#JSDoc) [Quality Assurance](#quality-assurance)
* [Development History](#development-history)
  * [Milestone 1: Mockup development](#milestone-1-mockup-development)
  * [Milestone 2: Data model development](#milestone-2-data-model-development)

  
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
  * Reoccurring (true/false)
  * Date
  * Time
  

### Player Database
  * UserID (Defined by UH)
  * Game ID
  
  ## Installation 
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

  
# Application Design

## Directory structure

The top-level directory structure contains:

```
app/        # holds the Meteor application sources
config/     # holds configuration files, such as settings.development.json
.gitignore  # don't commit IntelliJ project files, node_modules, and settings.production.json
```
The configuration files are seperated in the config/ directory from the actual Meteor application in the app/ directory.

The app/ directory will be discussed in depth upon project completion

## Import conventions

Following the Meteor 1.4 guidlines, all the application codes have been filed in the  imports/ directory, with client/main.js and server/main.js used to import the code for the client and server.

Every imports/ subdirectory containing any Javascript or HTML files has a top-level index.js file that is responsible for importing all files in its associated directory.   

The client/main.js and server/main.js are responsible for importing all the directories containing code they need. An example will be used once the project is complete.

## Naming conventions

This system adopts the following naming conventions:

  * Files and directories are named in all lowercase, with words separated by hyphens. Example: accounts-config.js
  * "Global" Javascript variables (such as collections) are capitalized. Example: Games.
  * Other Javascript variables are camel-case. Example: addGame.
  * Templates representing pages are capitalized, with words separated by underscores. Example: Directory_Page. The files for this template are lower case, with hyphens rather than underscore. Example: directory-page.html, directory-page.js.
  * Routes to pages are named the same as their corresponding page. Example: Directory_Page.

  

## Data Model

The TableTop Manoa data model is implemented by two Javascript classes: [GamesCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/GameCollection.js) and [UsertoGamesCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/UserToGamesCollection.js). Both of these classes use a MongoDB collection with the same name and export a single variable (Games and UsertoGames)that provides access to that collection. 

Any part of the system that manipulates the Tabletop Manoa data model imports the Games or UsertoGames variable, and invokes methods of that class to get or set data.

There are many common operations on MongoDB collections. To simplify the implementation, the GamesCollection and UsertoGamesCollection classes inherit from the [BaseCollection](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/base/BaseCollection.js) class.

Both GamesCollection and UsertoGamesCollection have Mocha unit tests in [GamesCollection.test.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/GameCollection.test.js) and [UsertoGamesCollection.test.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/api/games/UserToGamesCollection.test.js).

## CSS

The application uses the [Semantic UI](http://semantic-ui.com/) CSS framework. 

The Semantic UI theme files are located in [app/client/lib/semantic-ui](https://github.com/ics-software-engineering/meteor-application-template/tree/master/app/client/lib/semantic-ui) directory. Because they are located in the client/ directory and not the imports/ directory, they do not need to be explicitly imported to be loaded. (Meteor automatically loads all files into the client that are located in the client/ directory). 

Note that the user pages contain a menu fixed to the top of the page, and thus the body element needs to have padding attached to it.  However, the landing page does not have a menu, and thus no padding should be attached to the body element on that page. To accomplish this, the [router](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/startup/client/router.js) uses "triggers" to add an remove the appropriate classes from the body element when a page is visited and then left by the user. 

## Routing

For display and navigation among its four pages, the application uses [Flow Router](https://github.com/kadirahq/flow-router).

Routing is defined in [imports/startup/client/router.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/startup/client/router.js).

TableTop Mana defines the following routes:

  * The `/` route goes to the public landing page.
  * The `/directory` route goes to the public directory page.
  * The `/<user>/profile` route goes to the profile page associated with `<user>`, which is the UH account name.
  * The `/<user>/filter` route goes to the filter page associated with `<user>`, which is the UH account name.


## Authentication

For authentication, the application uses the University of Hawaii CAS test server, and follows the approach shown in [meteor-example-uh-cas](http://ics-software-engineering.github.io/meteor-example-uh-cas/).

When the application is run, the CAS configuration information must be present in a configuration file such as  [config/settings.development.json](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/config/settings.development.json). 

Anyone with a UH account can login and use Tabletop Manoa to create a portfolio.  A profile document is created for them if none already exists for that username.

## Authorization

The landing and directory pages are public; anyone can access those pages.

The profile and filter pages require authorization: you must be logged in (i.e. authenticated) through the UH test CAS server, and the authenticated username returned by CAS must match the username specified in the URL.  So, for example, only the authenticated user `koday` can access the pages `http://localhost:3000/koday/browseGames` and  `http://localhost:3000/koday/manage`.

To prevent people from accessing pages they are not authorized to visit, template-based authorization is used following the recommendations in [Implementing Auth Logic and Permissions](https://kadira.io/academy/meteor-routing-guide/content/implementing-auth-logic-and-permissions). 

The application implements template-based authorization using an If_Authorized template, defined in [If_Authorized.html](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/ui/layouts/user/if-authorized.html) and [If_Authorized.js](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/blob/master/app/imports/ui/layouts/user/if-authorized.js).

## Configuration

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

## Development History
The development process for Tabletop Manoa consists of a sequence of Milestones. Milestones consist of issues corresponding to 2-3 day tasks. GitHub projects are used to manage the processing of tasks during a milestone.  

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

## Milestone 2: Data model development

This milestone started on April 13, 2017 and ended April 27, 2017.

The goal of Milestone 2 is to implement the database model: the underlying set of Mongo Collections and the operations upon them that would support the Tabletop Manoa application.  We constructed the data model as a set of Javascript classes. The GamesCollection and CategoryCollection classes provide the persistent data structures useful for Tabletop Manoa. 
 
For this milestone, we also created a set of mocha tests for the data model classes. These tests ensured that we can create, manipulate, and delete the data model documents successfully. The record of this test is documented in the [Data model unit tests](#data-model-unit-tests) section above.

Milestone 2 is implemented as [Tabletop Manoa Milestone M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/issues?q=is%3Aissue+milestone%3AM2+is%3Aclosed)::

![image](https://cloud.githubusercontent.com/assets/17040099/25521495/8b37bf6e-2b9b-11e7-95ef-6e45b4765139.png)

Milestone 2 consists of nine issues, and progress is being managed via the [Tabletop Manoa Project M2](https://github.com/tabletopmanoa/Tabletop-Manoa-Website/projects/2):

![image](https://cloud.githubusercontent.com/assets/17040099/25521464/68319008-2b9b-11e7-9313-a7fea2298224.png)

Each issue was implemented in its own branch, and merged into master when completed:

![image](https://cloud.githubusercontent.com/assets/17040099/25521750/899adc30-2b9c-11e7-9003-0614b1d26aec.png)

Once the database was complete, the program was run through [ESLint](#eslint) to verify that the code conforms to proper formatting standards.

![image](https://cloud.githubusercontent.com/assets/17040099/25522019/48e4d3ac-2b9d-11e7-83c0-bd25c8b74f1a.png)



