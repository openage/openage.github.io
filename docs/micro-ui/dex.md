---
banner: "![[crm.jpg]]"
---
# Dex
#directory #connect #scrapper

## Features
### UI
- Auth - Login/Logout #phase-1
- Time - 
	- Attendance: CheckIn/Break/Resume/Checkout, 
	- Task - start/stop time tracking
- Command Runner #phase-0
- List of Actions ( Tasks - pending/in-process/done)
- Prompts
	- Scrapper Prompt - captcha, login etc #phase-1
	- CheckIn/Resume Prompt
	- Start a Timelog ( assigned to me & is in-progress)
	- Error Prompt #phase-1
	- Notification #phase-1
### Action Handler
- POST at https://127.0.0.1:9090/actions #phase-2
-  cron job to fetch tasks from https://api.domain.com/system/api/tasks?application-code=dex&user-code=abc #phase-1
- task runner (using cli engine) #phase-0
	- file download against a file on web-app: application_code-dex, handler-file, config {url, folder path} #phase-2
	- get rates: application_code-dex, handler-scrapper, config- {} #phase-0
	-	on action completion PUT status at https://api.domain.com/system/api/tasks/xyxyxyxy #phase-1
## Epics

### Auth
- user is able to login #phase-1
	- by creating a session and opening the browser id.domain.con/sessions/xxxx....xxx/activate
	- keeps checking for session to get activated
- integrated CLI

### Hosting
- user is able to download the application #phase-1 
- application updates itself when a new release is made #phase-1
### Scrapping
- 

### Work Management
- check-in
- check-out
- to-do list
- set task in progress to start tracking time
- sync epics as project/folders/index.md - ft/tasks/ft-212/index.md <-has epic details

```
---
code: ft-123
type: epic
status: 'in-progress'
timeStamp: 2023-03-01T12:30
---

# This is the title of the epic

Description goes here

```

- sync stories as files - ft/epics/ft-212/ft-333.md
- add sub-tasks as items inside the file 

```
---
code: ft-123
type: story

children:
 - {code: ft-1234, status: done}
 - {code: ft-1234, status: done}
status: 'in-progress'
timeStamp: 2023-03-01T12:30
---

# This is the title of the story

Description goes here


## Sub-Tasks
- title of sub-task 1
- title of sub-task 2

```

### Offline Documents
- create folder structure in the local drive and ability to browse the folder/file
- download file when the file is opened using the application
- upload the file when the user updates the file
- uploads all the newly added files in a folder
