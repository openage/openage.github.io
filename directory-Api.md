`            `**Document About Directory-Api**

- ***Importance of Directory-Api*** 
- **Directory-Api plays an important role in open-age framework**
- **Open-age framework is based on Micro-services Architecture**
- **Micro-services architechture are two types**








- **In directory-Api we divided services into different different Micro-services**
- **Each Micro-Services are independent**
- **In directory-Api we always do Authentication & Authorization** 


***Directory Schemas :***


`           `***1st  entry Point is Tenants***

- *Tenants is just like a Head of Organization for example: AQUA is a tenant inside it we have (Method Hub, Jindal) tenants may be one or more*




*2. /**division***


*Division is like but we can say it’s a dividing for example* 

*If we have MAX Hospital in Chandigarh and second hospital is in Delhi so it’s a division* 





*3. **/user***

- *We can create user According to requirements* 
- *After tenants user is a most important* 
- *We can create user we can change password for user according to our requirements*
- *We can create different different  type of user*
- *For example: we have 1 user who has a level of tenants*  

`          `*AQUA users they have a right to create any organization, they can edit any organization they have a level of (tenants' user)*


*4./employee*

- *The user who only access single organization is called employee*

*I**N USER SCHEMAS***

- *Basics  Details* 
- *Like  Phone,Email,Socialmedia ID,facebook ID, Google ID, Last seen*


**Inside Profile:**

- First name, Last Name, Father Name, Title, DOB, PIC, Gender, Location, Address, Status,
- Status is define a user access
- User is a Tenants level Entity
- If we want to give user only access to a single organization is called employee

**4./employee**

- Details same as user but some extra information
- Like Designation, Supervisor
- One user has a Multiple role
- Employee (Department, division, contractor, DOJ, DOL)
- Contractor is an entity inside organization













**5.role**

- Role is a base of directory-Api
- In any microservices we never use user, Developer, Employee
- Always give the 1st preference to the (role) inside role all the information is save
- Inside role we have (code) in each role code is unique for example: in our organization we have 1000 role, so each role is unique (CODE)
- In each role we have Email, phone Number, we can skip any one but one of them is Compulsory 
- If there is no email or no Phone Number, then User will not create 


**/type:**

- Inside type we define role permission 

**/Permission:**

- If we want to give any permission for a specific Engineer so we can give here in this section 
- We can give a permission for entity for a specific Engineer
- Permission we can give always in role not (role-type)
- User and Employee both are the part of role
- If any person not an employee only a user, then we can create simple user role
- Role for everyone (user, Employee, Student)

6**.Role-type:**

- Roles are different for example: one is Supervisor another one is Engineer so in this Supervisor role is Supervisor
- Engineer role is Engineer
- Engineer has some specific permission for example: if there is Api or Web Page so these are only access by supervisor not Engineer 
- These things we can define in role

**/role-key:**

- So key is a GUID it’s a unique for each role
- We always create new GUID
- Two same GUID never created 
- Always created GUID by GUID Generator
- If we want to create role manually then always create GUID by GUID Generator


7.**/Session:**

- When user login or sign up after that always create a session 
- When person login its always login on directory it will get a one Session 
- After that by this session person will Access any Api through this session 
- Session Token, session status, session expiry time, user detail, role detail, 
- If we want to get profile of any user for different micro-services
- So best practice is to get this by role 

**Session-token:**

- This is a JWT token when user login after that JWT token will be created 
- Always JWT token use for every session validation 

**8./user Service Basic Function:** 

- When we give** a new Access to anyone then we must start it
- When you take directory URL you will get the same page after that all the Api and specs you'll get 


- For example, if you want to create a user Phone Number, Email, Password
- If this user is temporary use either (false) or (True)
- We can set limited time for temporary user 
- Check existing email is used or not or email is used by any user 
- If user already exists, then we must delete it or update it 
- For Status =>> Active or Inactive

**/Sign in**

- We have to sign in multiple ways  
- Basics is using password
- If we want to match our password this algorithm, we use Bcrypt uses a 128-bit salt and encrypt a 192-bit magic value

**Second way to sign in:**

- ` `Second way to sign in OTP 
- 1st we have to use (resend) for sending OTP

- After that use confirm  Function for giving OTP and send it if OTP match then you will login 


**3rd Third way of login is social media:**

- Use this (user/auth/provider)
- In single tenant you store multiple Google Account




- After that use this [POST] /users/auth/{provider}/success


- Here we can pass ID send it by Google
- In this already inside tenant having a ID so it will Match it and check it will validate or not 
- If its valid or within it email or phone Number attach and within this email or phone Number You can login 

**In case USER Doesn’t exist:**

- Then** it will check “auto create “Api check outo-create
- If auto created is (true) then who so login by Google first create user after that create role for it after login and you will get token 
- This is in case of auto-create (true)


**If auto-create (False):**

- If email having no user, then you can't login 
- In config we define and Expiration of token 
- When directory-Api Micro-service we create Employee or DB Micro service then How it will go another Micro-Service 

**/Hooks:**

- You can define Hooks in config file
- It's not important that hooks are in config file
- Maybe it will in organization or tenants 
- Whenever action perform
- As you see when any organization is update then Hook will trigger

- Suppose this hook is in division 
- So, whenever this division update then Hook will Trigger

- If hook in organization and inside organization division will be update, then Hook will trigger
- We can set different different Hooks for different different organization 

**For example:** if you have 3rd party Api where we can store data of division, user, so if we want to create new user so 3rd party Api our data will be push 

- We can give URL Also

- If we want to pass JWT token so, pass it in Header
- We also use Mapper
- For example: so, our hook is organization 
- Mapper will go in organization directory and pass entity

- Mapper always use (to Modal) function and pass entity whatever (to modal) function detect and send it URL As Above mention in Screen shot


- If it is put then put request if it is post then it will set post request
- Every Modal and tenant has a Hook 
- We can put Hook in organization and tenants
- 1st entity
- 2nd action
- 3rd when
- These are 3 responsible for trigger a Hook 




**When :**

- When is before or after when you want to Hook trigger a Hook before update or After Update 


**Action:**

- Is http
- POST, PUT, Update, Delete
- If you are using action out of them then your data will not store in Api






- When you perform Any Action always remember directory-Api support only Get, Put, Delete, Post, http
