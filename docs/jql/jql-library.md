# JQL Library (Jira Ops Lab)

## Service Requests (Kanban)

**All Service Requests**
project = IOL AND labels = service_request ORDER BY created DESC

**Service Requests - In Progress**
project = IOL AND labels = service_request AND status = "In Progress" ORDER BY updated DESC

**Service Requests - To Do**
project = IOL AND labels = service_request AND status = "To Do" ORDER BY created ASC

**Aging Service Requests (not updated in 3 days)**
project = IOL AND labels = service_request AND statusCategory != Done AND updated <= -3d ORDER BY updated ASC


## Delivery Work (Scrum)

**Stories + Bugs**
project = IOL AND issuetype in (Story, Bug) ORDER BY created DESC

**Sprint items (current sprint)**
project = IOL AND Sprint in openSprints() ORDER BY rank ASC

**Bugs only**
project = IOL AND issuetype = Bug ORDER BY created DESC

**Work in progress**
project = IOL AND status = "In Progress" ORDER BY updated DESC


## Program view / hierarchy helpers

**All Epics**
project = IOL AND issuetype = Epic ORDER BY created DESC

**Work linked to the program umbrella Epic (IOL-1)**
issue in linkedIssues("IOL-1") ORDER BY created DESC
