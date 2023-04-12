---
banner: "![[recuritments.jpg]]"
---

# Talent
#recruitment #discovery #talent
https://talent.domain.com
https://www.domain.com/talent


## Overview

### Flow

![[recruitment-flow.jpeg]]

## Features

- Job Management
- Applicant Management
- Interview Process
- Offer letter Management

Refer recruitment  [[entities]] for the attributes

Job Creation Wizard
- Select a template or start from scratch
- Edit title, type (full-time, consultant), description
- Add keywords, and salary range
- Add list of skills, Minimum Qualifications
- Add  rounds (pick from screenings)

## Epics
- ability to add masters #phase-0 
	- [ ] skills api -  CRUD
	- [ ] rounds api -  CRUD
- ability to add jobs #phase-0
	- [ ] jobs api -  CRUD
- ability to create candidate #phase-0
	- [ ] candidates api - CRUD
- ability to add applicants in a  job #phase-0 
	- [ ] applicants api - CRUD
- candidate creates his profile #phase-1
	- [ ] signup with email (using identity.domain.com #identity #portlet  )
	- [ ] updates demographics in #recruitment #candidate
- candidates sees top 5 jobs based on relevance - location, skills #phase-1
	- [ ] when candidate searches (in #discovery) based on his profile (preferences) relevant jobs  should show up.
- hr creates a job using wizard #phase-1
- ability to conduct interview #phase-2

