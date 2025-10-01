# Requirements

## 1. Functional Requirements

### UC1: Playing the Game

#### High Priority

- The user shall be given a randomly generated pollinator [FR1]
- The user should generate a unique pollinator each time [FR2]
- The user will be able to press a complete button when done with each path step [FR3]
- The user will receive facts about the pollinator after discovering their pollinator [FR4]

#### Medium Priority

- The user will find the game's website using a QR code [FR4]
- The user shall be able to join a session using a session code [FR5]
- The user shall be able to click a back button to go to the previous path location while playing [FR6]

#### Low Priority

- The game should have an option to automatically read text aloud [FR7]
- The game should have an option to click a button to read text aloud [FR8]
- The game should have an option to adjust text size [FR9]
- The game should have an option to adjust the text font [FR10]
- The game should have a high contrast colors mode [FR11]

### UC2: Analyzing Statistics from the Backend About Games Played

#### High Priority

- The system should allow an admin to view all statistics about game sessions previously played [FR12]

#### Medium Priority

- The admin should be able to filter game statistics based on user-provided filter criteria [FR13]
- The system should allow an admin to view an average of all statistics about game sessions previously played [FR14]
- The system should allow an admin to view graphs about game statistics [FR15]

#### Low Priority

- The system should allow website statistics to be exported as a CSV [FR16]
- The system should allow website statistics to be exported as a XCEL file [FR17]
- The system should allow website statistics to be exported as a PNG file with graphs [FR18]


### UC3: Temporarily Enabling/Disabling Path Options for Current Game Session

#### High Priority
- The instructors shall be able to start a temporary session [FR19]
- The instructors shall be able to stop a temporary session that they previously started [FR20]

#### Medium Priority

- A session code should be generated for the instructor after they start a session [FR21]
- The instructor should be able to view their current session code [FR22]
- The instructors shall be able to disable possible in-game paths for their currently running session [FR23]
- The instructors shall be able to enable possible in-game paths for their currently running session [FR24]

#### Low Priority

- Paths that have been disabled by the instructor should not be randomly picked for players in that session [FR25]

### UC4: Permanent Removal/Addition/Editing of Paths for All Future Sessions

#### High Priority
- The systems administrator shall be to add pollinator paths permanently to all future game sessions  [FR26]
- The systems administrator shall be to remove pollinator paths permanently from all future game sessions  [FR27]
- The systems administrator shall be to view all current possible pollinator paths in the game [FR28]

#### Medium Priority

- The systems administrator shall be to view all current facts about pollinators in the game [FR29]
- The systems administrator shall be to add facts about pollinators in the game [FR30]
- The systems administrator shall be to remove facts about pollinators in the game [FR31]


### UC5: Adding, Removing, Viewing Permissions of All Internal Users

#### High Priority
- The systems administrator should be able to add and remove privileges of admins under them [FR32]
- The systems administrator should be able to view permissions of all users [FR33]

#### Medium Priority

- The systems administrator should be able to view a log of all previous edits made by systems administrators [FR34]


## 2. Non-Functional Requirements

### UC1: Playing the Game
 - The game should be accessible to blind and low vision players [Low] [NFR1]
 - The game should be accessible to child players [Low] [NFR2]
 - The game should be accessible to adult players [Low] [NFR3]
 - The game should be accessible to elderly players [Low] [NFR4]
 - The game should be accessible to dislexic players [Low] [NFR5]
 - The game should be accessible to colorblind players [Low] [NFR6]
 - The game should be accessible to deaf players [Low] [NFR7]
 - The game should be accessible to players with autism [Low] [NFR8]
 - The game should be accessible to players with mobility limitations [Low] [NFR9]
 - The game should be accessible to deaf and hard of hearing players [Low] [NFR10]
 - The game should be accessible to players of any phone type [Low] [NFR11]
 - The game should be accessible to players of any screen size/resolution [Low] [NFR12]

### UC3: Temporarily Enabling/Disabling Path Options for Current Game Session
 - The games paths should all be enabled by default [Medium] [NFR13]
