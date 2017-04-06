Tabletop Manoa is an application designed to allow those in the UH community to coordinate and join in various tabletop games. The ability to do this will enable students to get together in a safe environment for fun and socialization as they play in games ranging from Monopoly and Spades to WarMachine and Pathfinder.

# Table of Contents
* [Project Goals](#project-goals)
* [Database](#database)
* [Mockup Pages](#mockup-pages)
* [Installation](#installation-notes)

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

## Mockup Pages
These pages are the basis of our starting point for our project. There will be a lot of cleanup involved in the pages (remove image on menu bar, change background, remove colored padding around cards) which will be updated as progress occures.

### Landing Platform
Login required
![image](https://cloud.githubusercontent.com/assets/17040099/24745623/0995be52-1a52-11e7-8e0d-1ca74b6664b0.png)


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
