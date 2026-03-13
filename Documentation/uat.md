# User Acceptance Testing (UAT)

## Last Updated: 2/24/2026

---

# 1. Feature Overview

| Feature | Priority | Iteration | Client Facing (Y/N) |
|---------|----------|-----------|---------------------|
|Repeatable Route Play|High|1|Y|
|Pollinator Collection|High|3|Y|
|Statistic Pull|High|4|Y|

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
Internal Passed

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**
The user just completed a route and is fetching a new route

**When:**
The user loses connection to the Wi-Fi, and the fetch route fails

**Then:**
A basic error message is given to the players and redirects them to a previous page

**Status:**
Unknown if implemented ( should check )
**Evidence:**

### Scenario 3: Edge Case
...

---

## Feature: Pollinator Collection Page
### Scenario 1: Happy Path
**Given:**
A user has completed a route

**When:**
When navigating to the collection page

**Then:**
Completed routes are shown as collection pollinators with sprites

**Status:** (Not Tested / Internal Passed / Client Accepted)
Internal Passed

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**

**When:**

**Then:**

**Status:**

**Evidence:**

### Scenario 3: Edge Case
...

---

## Feature: Read From Route Database
### Scenario 1: Happy Path
**Given:**
Admin service is started

**When:**
Admin accesses the service

**Then:**
Then the admin can read the files and statistics on the routes within the database

**Status:** (Not Tested / Internal Passed / Client Accepted)
Not Tested

**Evidence:** (link to PR, test file, video, screenshot)

### Scenario 2: Error Handling
**Given:**

**When:**

**Then:**

**Status:**

**Evidence:**

### Scenario 3: Edge Case
...

---

# 3. Client UAT Log

These tests are validated by the client.

| Date | Feature | Client Feedback | Action Required | Resolved (Y/N) |
|------|---------|-----------------|-----------------|----------------|
||Feature1||||

---

# 4. Open Acceptance Risks

## Risk1
- Risk:
- Mitigation Plan:

## Risk2
