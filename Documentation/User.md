# User Documentation

## Overview

This application is designed to be your virtual fact sheet for **Conner Prairie's: *Pollinator Habitat*** Activity. When you begin, you will secretly be assigned a random pollinator. The purpose of the activity is to use **science** to figure out what polliator *you* are. 

This is completed by going through a small series of prompts ("I have 2 legs", "I have 4 wings") that you will follow along with by matching it with the clues on your screen (ex: 6 legs or elytra wings) 

At every prompt, you will use your pollinators physical characteristics to narrow down what type of pollinator you were secretly assigned (ex: "Bee", "Hummingbird").

Once you have ruled out any other type of pollinator, you will discover which one you were secretly assigned. You will then be presented unique facts about that particular pollinator, and its benefit to the ecosystem!

**Fun fact: The activity's series of questions are called a dichotomous key.**

You can learn more about dichotomous keys here: [biologydicionary.net](https://biologydicionary.net)

## Usage Guide: 

**Note:** Let the application load completely. You will know it is ready to use when you see the prompt *Enter your session id* in the center. 

Click the **'Enter'** Button to go to the main menu. 

Once in the Main Menu, you should see two buttons:
1. Start New Pollinator Path
2. Accessibility Settings

## Start New Pollinator Path 

To play the Pollinator Habitat Activity, press the 'Start New Pollinator Path' button.

When you see the word "Start" on your screen, you have successfully joined the activity and been assigned a secret pollinator. An example of this screen is shown in the picture below:

### 1: With Start on your screen, move to the Start Card along the ground. 

![Starting Screen](pics/StartScreenNew.png)

### 2: Once at the Start location, press the "Next" button to get your first pollinator clue. Then, move to the spot that matches your pollinator's clue. 
#### You can move back a step with the "Previous" button

![Directional Buttons for Previous and Next](pics/DirectionBar.png)

#### Example: If your screen displays the clue "worker with no wings" move to the spot that has the "worker with no wings" marker. 


![Pollinator Clue example of a worker with no wings](pics/RouteImageWorkers.png)

### 3: Once you arrive to the marked spot, press the "Next" button to move get your next fact so you can figure out where to go next. 

### 4: Follow along until you figure out your unique pollinator. You will then get to view several different facts about the pollinator. 

### 5: Once you have reach the final fact about about your pollinator, you can either restart the activity by pressing the "Start New Route" or return to the main menu by pressing "Home'.

### 6: When a pollinator's route is completed, it is added to the user's Collection. Total pollinators can be seen in the main menu as seen below. 
![Collection count showing 3/11 pollinators collected](pics/CollectionCount.png)

### 7: Facts are then displayed for the pollinator

### 8: When the final fact is displayed, the "next" button will disappear. This indicates Route conclusion. 

### 9: To restart the game, press the "Start New Route" button. 

![Screen showing last fact with start new route button](pics/RestartPrompt.png)

### If playing the activity again, start again at step 1. 

### At any point in the game, the user can go back to the home menu with "Home" button. 

## Accessibility Menu

### Within the accessibility settings menu, there are a menu of settings that will facilitate user accessibility 
#### From the main menu, tap "Accessibility Settings"
#### Steps to enable:
##### 1: Click the checkbox next to "High Color Contrast"
- While checked, the applications visual representation will utilize high contrast colors
- The setting can be reverted by simply unchecking the box
##### 2: Click the checkbox next to "Text-to-Speech" 
- While checked, the TTS button will be available to during the accessibility page. 
- Later, this will be expanded to route page and pollinator collection page for actual usage. 
    - Functionality to be added in future iteration. 

![Accessibility Settings Page](pics/AccessibilitySettingsMenu.png)

## Pollinator Collection 
### To access, click the "Pollinator Collection" button from the home menu. 
### When the user finishes a polllinator's route and gets to the fact section:
- Pollinator is stored to users random playerId via JWT
- The pollinator is added to the "Discovered" section of the collection page
- The pollinator's image transforms from a silouette to a full color sprite
- The back button takes you back the home menu

![Pollinator Collection Page](pics/CollectionPage.png)

## Pollinator Habitat Admin Portal 
### Overview
This application is designed to be a quick search tool to retreive party size survey responses and results from the database. With the ability to search by date, date range, or session ID number, the portal provides various ways to access survey response data. 

This data will later also be able exported to CSV (at the request of our client) so that it can shared with stakeholders or archived for collection purposes. 

### Usage Guide: 

The portal page is a single page application designed to allow the access and export of survey data based on the search criteria. 
Data is grouped by SessionID within the database. 

#### Search by Date

#### 1: Enter in the desired search date in the "Start Date" textbox. 
![Start Date textbox](pics/StartDate.png)

#### 2: Click the 'Search' button to obtain results pertaining to the entered date value.
![Search Button](pics/SearchButton.png)

![Date Search results](pics/SearchByDate.png)

#### Search by Date Range

#### 1: Click the "Date Range" checkbox so it fills in orange. This activates the second search box. 
![Disabled End Date textbox](pics/EndDateNotActivated.png)
![Enabled End date textbox](pics/EndDateActivated.png)

#### 2: Search by date: Enter in the desired search dates in the "Start Date" and "End Date" textboxes. 
![Filled in Start and End date textboxes](pics/DateRangeTextboxes.png)

#### 3: Click the 'Search' button to obtain results pertaining to the entered date range values.
![Search Button](pics/SearchButton.png)

![Search results based on date range](pics/SearchByDateRangeResults.png)

#### Search by SessionId (Single result table row)

#### 1: Enter in the desired search date in the "Start Date" textbox. 
![Session ID search textbox](pics/SessionIdBox.png)

#### 2: Click the 'Search' button to obtain results pertaining to the entered SessionId value. 
![Search Button](pics/SearchButton.png)

![Search results based on session ID](pics/SearchBySessionIdResults.png)