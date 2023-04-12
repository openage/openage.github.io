---
banner: "![[accounts.png]]"
---

# Identity
#identity #portlet

A micro portal that merges all the identities into a unified id.  It would provide centralised authentication for all the applications, including the one which the customer's may be using.

The key responsibilities of this portlet would  be 
- authenticate user and redirect the user to its default application
- Multi Factor Authentication 
	-  email -password, 
	- employee id - password
	- Microsoft AD
	- Google 
- Recover password
- Multi Device Sessions Management

It would have following features
- Login/Signup
- Multi Factor Authentication
- Multi Device Sessions Management
- Login/Signup customisation

https://id.domain.com



## Features
### Sign In

Examples
- Google
- Bitbucket
![[bitbucket-id-portal.png]]

### Profile


### Designers
- User Designer
- Signup Designer
- Role designer
- Organisation Theme

## Library

### Providers
-   Identity - Google, Microsoft, Apple, Facebook, LinkedIn, Whats App, SAML
-   Multi-factor - SMS, Email, OTP, Google Authenticator, Microsoft Authenticator

### Widgets
-   Login
-   Signup

### Library
-   Roles
-   User Attributes
-   Organisation Attributes
-   Signup Forms

### Communication 
- invite email - user should get an email when he is added to the tool
-   Complete Signup ![[mails-otp.png]]
-   Signup Completed
-   Failed Login Attempt
-   Successful Login ![[mails-login.png]]
-   New Joiner to supervisor ![[mail-new-joinee.png]]

## Reports

### User  
-   Failed Attempts
-   My Activities
-   Inactive Sessions

### Lead
-   Active Users
-   User Activities

### Admin
-   Suspicious Activities 
-   Who has access to what

## Roadmap
### Sign in
- [ ] user is able to sign in 
    - [ ] email/password
    - [ ] google auth
    - [ ] active directory authentication
    - [ ] phone/password
    - [ ] employee id/password
    - [ ] email/OTP
    - [ ] WhatsApp
    - [ ] phone/OTP (WhatsApp)
- [ ] user is able to recover the password
    - [ ] phone/OTP
    - [ ] email/OTP
### View Details
- [ ] user is able to view/edit the profile
- [ ] admin is able to view/edit employee
- [ ] sysadmin is able to view/edit system user
- [ ] user is able to view activities
- [ ] user is able to view sessions
### Manage users
- [ ] admin is able to add manage organisation masters
    - [ ] division
    - [ ] department, 
    - [ ] designation
- [ ] admin is able to manage employees
    - [ ] on-board an employee
    - [ ] off-board an employee
- [ ] sysadmin is able to manage system users
    - [ ] on-board an user
    - [ ] off-board an user
- [ ] admin is able to organisation branding, theme and icon groups
### Signup 
- [ ] admin is able to signup his organization - multi-step signup
- [ ] user is able to sign up
- [ ] sysadmin is able to signup his application
- [ ] user is able to set multi-factor authentication
### Manage Process
- [ ] sysadmin is able to configure user/employee life-cycle (create a composer task with inputs for each service)
    - [ ] employee off-boarding process
    - [ ] employee on-boarding process
    - [ ] system user off-boarding process
    - [ ] system user on boarding process
- [ ] sysadmin is able to set identity providers
- [ ] sysadmin is able to set multi-factor mechanisms available
- [ ] sysadmin is able to set User attributes (user designer)
- [ ] sysadmin is able to set post Signup actions (signup designer)
### Manage Application
- [ ] sysadmin is able to manage security
    - [ ] Role Type (role designer) 
    - [ ] Permissions (permission designer)
- [ ] sysadmin is able to manage applications (navigation and access) 
    - [ ] create applications API in the system that gets the application details based on the URL, and code - it would return tenant, organization, services, navigation, theme, etc
    - [ ] replace the tenant fetching mechanism from directory/tenants to system/applications
      - [ ] add applications in the system applications