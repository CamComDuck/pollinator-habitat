# User Acceptance Testing (UAT)

## Last Updated: 3/17/2026

---

# 1. Feature Overview

| Feature | Priority | Iteration | Client Facing (Y/N) |
|---------|----------|-----------|---------------------|
|Repeatable Route Play|High|1|Y|
|Pollinator Collection|High|3|Y|
|Repeatable Route Play|High|4|Y|
|High Contrast Mode|Low|3|Y|
|Survey Data Search|High|4|Y|
|Route Data Search|High|5|Y|
|Quick Export Tool|High|5|Y| 
---

# 2. Acceptance Scenarios

## Feature:  Pollinator Habitat Activity should be repeatable 

### Scenario 1: Happy Path
**Given:**
User is a part of an active Pollinator Habitat activity session

**When:**
When the route is completed and the final fact is displayed to the user

**Then:**
A button displays to the user that allows for a new route activity to be completed

**Status:** (Not Tested / Internal Passed / Client Accepted)
Client Accepted

**Evidence:** (link to PR, **test file**, video, screenshot)
Test file: frontend/testing/UATs/RepeatbleRoutePlay.test.tsx

### Scenario 2: Error Handling
**Given:**
The user just completed a route and is fetching a new route

**When:**
The user loses connection to the Wi-Fi, and the fetch route fails

**Then:**
A basic error message is given to the players and redirects them to a previous page

**Status:**
Implemented

**Evidence:**


## Feature: Pollinator Collection Event and Page
### Scenario 1: Happy Path
**Given:**
A user has completed a route

**When:**
When navigating to the collection page

**Then:**
Completed routes are shown as collected pollinators with filled in sprites

**Status:** (Not Tested / Internal Passed / Client Accepted)
Client Accepted

**Evidence:** (link to PR, **test file**, video, screenshot)
Test file: frontend/testing/UATs/PollinatorCollection.test.tsx

### Scenario 2: Error Handling
**Given:**
User completes the route
**When:**

**Then:**

**Status:**

**Evidence:**

## Feature: One-time Optional Survey
### Scenario 1: Happy Path
**Given:**
User is a part of valid session

**When:**
Last fact node is reached

**Then:**
A small one time, optional survey should appear, asking about the party size by age category. 

**Status:** (Not Tested / Internal Passed / Client Accepted)
Client Accepted

**Evidence:** (link to PR, **test file**, video, screenshot)
Test file: frontend/testing/UATs/OneTimeSurveyPopUp.test.tsx

### Scenario 2: Error Handling
**Given:**

**When:**

**Then:**

**Status:**

**Evidence:**

## Feature: Survey Data Search Tool 
### Scenario 1: Happy Path
**Given:**
Portal service is started and accessed

**When:**
Proper search criteria is provided

**Then:**
Admin can view sessionIDs and survey responses

**Status:** (Not Tested / Internal Passed / Client Accepted)
Client Accepted

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**
Portal service is started and accessed

**When:**
Improper search criteria is provided

**Then:**
Search button is disabled

**Status:**
Implemented

**Evidence:**

## Feature: Route Data Search Tool 
### Scenario 1: Happy Path
**Given:**
Portal service is started and accessed

**When:**
Proper search criteria is provided

**Then:**
Admin can view aggregated route data  for criteria

**Status:** (Not Tested / Internal Passed / Client Accepted)
Internal Passed

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**
Portal service is started and accessed

**When:**
Improper search criteria is provided

**Then:**
Search button is disabled

**Status:**
Implemented

**Evidence:**

## Feature: Quick Export Tool 
### Scenario 1: Happy Path
**Given:**
Portal service is started and accessed

**When:**
A timeframe and report type are checked

**Then:**
Admin can quickly export reports with 3 clicks

**Status:** (Not Tested / Internal Passed / Client Accepted)
Internal Passed

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**
Portal service is started and accessed

**When:**
Only 1 or 0 selections are made for timespan and report type

**Then:**
Export button is disabled

**Status:**
Implemented

**Evidence:**

# 3. Client UAT Log

These tests are validated by the client.

| Date | Feature | Client Feedback | Action Required | Resolved (Y/N) |
|------|---------|-----------------|-----------------|----------------|
|03-13-2026|Repeatable Route Play|Approved for unique and random|None|Y|
|03-13-2026|Pollinator Collection|Likes silouttes in collection page|None|Y|
|03-13-2026|Optional survey|Wants New Route button to appear before survey|None|Y|
|04-16-2026|High Contrast Mode|Appreciates accessibility measures|None|Y|
|04-16-2026|Survey Data Search|Likes data search, likely won't use sessionID search|None|Y|
|04-16-2026|Route Data Search|Needs export|Add export option|Y|
|04-16-2026|Quick Export Tool|Would like ability to view both reports at once|Add both option for quick export page|N| 
