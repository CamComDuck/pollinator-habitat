# Use Cases

## Actors
Actors are specific definitions of users who will use the Pollinator Habitat system in a certain way to fit their  needs and requirements.

### 1. Children
Young users who interact with the game through the web application for educational or entertainment purposes. They represent the primary users who will be playing the game and navigating through various paths within the game.

### 2. Adults
Adult users who play the game through the web application, potentially including parents, educators, or general users. They might be more knowledgeable than the children who will be playing the game. They have the same interaction capabilities as children, but may be running the application for a group of children.

### 3. Disabled Children
Young users who suffer from being colorblind, deaf, or blind who require accessible gaming features and accommodations. The system must provide inclusive design elements to ensure equal access to gaming functionality.

### 4. Disabled Adults
Adult users who suffer from being colorblind, deaf, or blind who require accessible gaming features and accommodations. The system should accommodate various disability types.

### 5. System Administrator
Internal system users with the highest level of privileges who manage the overall system configuration, user permissions, and system maintenance. They have full access to all administrative functions and can modify system-wide settings.

### 6. Activity Lead
Internal users responsible for managing game sessions and path configurations during active gameplay periods. They have operational control over temporary game settings and can enable/disable paths for specific sessions.

### 7. Business Analysts
Internal users who need access to system analytics and performance data to make business decisions.

## Use Cases

### UC1: Playing the Game

#### Explanation
This is the core functionality of the project where external users interact with the game through the web application. Players navigate through different paths and engage with the content, learning about various pollinators. The system will track which paths they have done and give them a new path they have not done before in a single game session.

#### Actors
Children, Adults, Disabled Children, and Disabled Adults

#### Flow
  1. User accesses the game through a QR code that brings them to the web application
  2. The system displays available game paths and a menu for the accessibility settings
  3. The user can select paths they want enabled/disabled, change accessibility settings, or press start to put them on a randomized path
  4. The user will start the game
  5. Users follow a path, given randomly by the system
  6. The system will collect statistics
  7. The system records completion when the user completes the path
  8. The user will be able to read facts about the pollinators that the paths lead them to
  9. The user will be returned to the starting screen, where they can repeat the game

#### Business Requirement
BR1: Simplify, digitize, and improve an existing educational activity about pollinators and their habitats, serving all age ranges and accessiblity levels

### UC2: Analyzing Statistics from the Backend About Games Played

#### Explanation
This use case enables the business analysts to monitor system usage, user engagement, and game performance through the system-collected analytics. The data will be used for business decision-making, identifying usage patterns, getting grants, enhancing the game, and measuring the success of the game through the web application.

#### Actors
Business Analyst

#### Flow
  1. Internal user accesses the administrative portal
  2. System verifies user permissions and grants appropriate access
  3. User navigates to the statistics dashboard
  4. System displays an overview of multiple statistics (total users, total time spent, routes completed, etc.)
  5. The user can view individual statistics in detail
  6. The user can export data to CSV format for external analysis
  7. System maintains access control throughout the session
  8. The user can reset access control settings if needed

#### Business Requirement
BR2: Collect, aggregate, and provide access to data about activity use, to provide valuable insight about activity participant trends

### UC3: Temporarily Enabling/Disabling Path Options for Current Game Session

#### Explanation
This use case provides optional flexibility by allowing activity leads to dynamically control which game paths are available during specific sessions. This functionality is important for managing special events, testing new features, or accommodating specific group needs without making permanent system changes. Paths may be closed for maintenance, construction, or other real-world problems. 

#### Actors
Activity Lead 

#### Flow

  1. Activity Lead accesses the session management interface
  2. System displays current session status and available paths
  3. User starts a new game session or selects an existing active session
  4. The activity Lead gives the players in the group a code to join a specific session.
  5. User selects specific paths to disable for the current session
  6. System temporarily removes selected paths from the player interface
  7. User can re-enable paths during the session as needed
  8. System maintains all paths enabled by default
  9. User stops the session when activities are complete
  10. System restores all paths to the default enabled state

#### Business Requirement
BR2: Collect, aggregate, and provide access to data about activity use, to provide valuable insight about activity participant trends

### UC4: Permanent Removal/Addition/Editing of Paths for All Future Sessions

#### Explanation
This use case enables administrators to make changes to the game structure by permanently modifying available paths. This functionality is essential for system maintenance, content updates, and long-term game evolution. It allows the platform to grow and adapt while maintaining consistency across all future gaming sessions.

#### Actors
System Administrator

#### Flow

  1. Administrator accesses the admin dashboard interface
  2. System displays all current paths with editing options
  3. Administrator selects action (add, remove, or edit paths)
  4. For adding: Administrator defines new path parameters and content
  5. For removing: Administrator confirms permanent deletion of selected paths
  6. For editing: Administrator modifies existing path properties and content
  7. System Admin will hit an approve button that will tell the system to update the changes.
  8. System validates changes and updates the path configuration
  9. System applies changes to all future gaming sessions
  10. Administrator confirms successful implementation

#### Business Requirement
BR2: Collect, aggregate, and provide access to data about activity use, to provide valuable insight about activity participant trends

### UC5: Adding, Removing, Viewing Permissions of All Internal Users

#### Explanation
This use case manages user access control and security by allowing administrators to control who has access to various system functions. It's critical for maintaining system security, ensuring appropriate access levels, and managing the internal user base. Proper permission management protects sensitive data and maintains operational integrity. Activity leads could be temporary hires who will only need access to specific abilities for a certain time. The Administrator would be able to give them the access they need to do their job, and remove it when they are no longer needed to work. 

#### Actors
System Administrator

#### Flow
  1. Administrator accesses the user management interface
  2. System displays a list of all internal users with current permission levels
  3. Administrator selects a user to modify or views all user permissions
  4. For adding privileges: Administrator assigns new permissions to selected users
  5. For removing privileges: Administrator revokes specific permissions from users
  6. System validates permission changes and updates user access levels
  7. System logs all permission modifications for audit purposes
  8. Administrator confirms changes are applied successfully
  9. Affected users receive updated access rights immediately

#### Business Requirement
BR2: Collect, aggregate, and provide access to data about activity use, to provide valuable insight about activity participant trends