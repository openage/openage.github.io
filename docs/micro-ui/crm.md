---
banner: "![[crm.jpg]]"
---
# CRM
#sales-engine #directory #send-it #billing #insight #console #discovery 

Sales team should be able to  manage business relationships by managing their contacts and  delegating the office work to their team members

The tool would enable them to 
- manage company's relationships and interactions with customers and potential customers. 
- streamline the process of customer engagement 
- track and improve profitability

## Entities

### Agency
- attributes
	- Name, Type, Address,
	- Organization
		- Units/Divisions
		- Departments/Business Unit, Designations
		- Employees, Role
	- contacts, 
	- customers etc

### Contact 
- attributes
	- Personal - Name, Email, Phone, Designation, Picture
	- Company - Name, Logo, Industry, Company Type, Address
	- Address - Geo-location, Line 1, Line 2, City, State, Country, Code
- can belong to sales person
- has a task to convert it to customer

### Customer
- attributes
	- Company - Name, Logo, Industry, Company Type, Address
	- Tags: Category, Rating
	- Contacts - Role,  Contact
	- Documents
	- Preferences
		- Notification - subscriptions, communication channel
		- Services
	- Units/Billing
	- Finance
	- Team - Relationship Manager, Operations
- has a task to activate the customer

### Lead
- attributes
	- Scope Of Work - list of services,
	- Customer
	- Sales Person

### Campaign
- attributes
	- Title, code, description
	- Views/Likes/Enrolled
	- Period: Start Date, End Date
	- Visibility: Private, Internal, Public
	- Type: referral, promotion, greetings

## Users
- Customer Support
- Sales Person
- Sales Head
- Admin

## Workflows

Contact 
- New
- Hot
- Converted (final)
- Cold
- Not-Interested

Customer 
- Draft
- New
- Active (final)
- In-active
- Blocked 

Calling Task
- New
- Scheduled
- Re-Scheduled
- Done
- Aborted

Campaign
- Draft
- New
- Active (final)
- In-active
- Discarded 

## Roadmap

### Dashboards & Reports
- sales person dashboard
- pipeline report for sales head
- revenue by salesperson
- Quotas/Targets
-  Sales goals
-  Percent contributed to team revenue
-  closed/lost leads
- customer support dashboard
- sysadmin dashboard

### Contact/Customer Management
- sales person is able to manage contacts
	- contact editor
	- contact viewer
	- contact  importer - excel, scan visiting card
- sales person is able to manage customer
- admin is able to manage all the customers in the agency

### Pipeline
- sales head is able to set and track the sales target
- when a contact is added, task is created for customer support
- ability to convert contact to customer
	- customer support views pipeline of contacts
	- customer support schedules a meeting with contact
	- customer support converts a contract to customer
- sales is able to meet a contact
	- send out his available time slots via notification

### Campaign
- sales is able to convert referral code based signup form into campaign and share it 
	- via configured notification
	- embeddable signup widget
- admin creates and share  promotion campaign
	- campaign creator 
	- select a list of customers/contacts and share campaign via notification
- user is able to view list of campaigns
- campaign owner get notifications 
	- when the campaign becomes Active/In-active
	- when a user view/likes/enrols for his campaign
	- daily summary at end of day

### Notification and Actionable
- admin creates a greetings message and schedule to send it to target customers/contacts on a given date time.
- customer unsubscribes from the message
- sales person manages what kind of messages the customer receives
- admin manages the content of the message

### System Administration
-   sysadmin tweaks  Flows
	- Customer On-boarding
	- Contact Conversion
-   sysadmin manages Customer Attributes
-   Message Templates