

Connect API

ove rview





What IS Connect

API

• **Connect is basically use for connect anything to everything. We**

**can Integrate One API to Another API with Some End Points.**

**The End points should be authenticated.We can clear a**

**Configuration and pass a Configuration and we can access the**

**any API to GET, POST,UPDATE and DELETE Anything.**





nnect api and





Job Scheduling

• **Job Scheduling:- Yo u can schedule any Job through Connect. In job**

**scheduling job configuration to give cron expression can be schedule you can**

**create an expression firstly you pass the Configuration. In connect it create a**

**providers in which user can convert data array to object or you can deep code**

**any data and transform you can perform Configurable operation.**





Data ba se of connect

• **Major Database Collection:- The major database collection are lookups, Jobs,**

**Integration, Task and Provider.**

• **In Authentication User and Task are kept.**





Fetching api

• **Fetching API:- The Fetch API provides a JavaScript interface for accessing and manipulating parts of**

**the protocol, such as requests and responses. It also provides a global** fetch()**method that**

**provides an easy, logical way to fetch resources asynchronously across the network. We Can get any API**

**through Third Party**

**Syntax:-**

fetch(url)

• .then(response => {

• // Do something with the response here

• });





Posting on any api

• **Posting On Any API:- To make a POST request to an API endpoint, you need to send an HTTP POST request to the server and**

**specify a Content-Type request header that specifies the data media type in the body of the POST API request. It is used to send**

**data to a server to create/update a resource.**





Uploading sheets

• **Uploading Sheets:- In Our Project we use uploader in any particular area then we can use Upload using Connect. It has basically Two Feature**

**(i). It is work on One by One Pushing a object at a time. And it is not a Bulk operation to give 10 or more entities to a one API to Update.**

**(ii). Connect will help us on it to Hold the entities and give One by One to API to Update**





Token Generation

• **Token Authentication:-Token-based authentication for web APIs is the**

**process of authenticatingusers or processes for applications in the cloud.**

**The user's application sends a request to the authenticationservice, which**

**confirms the user's identity and issues a token. The user is then able to**

**access the application. And we can also perform Authenticationaction**

**Using Connect.**





Authentication

**Authentication:- It is a pipeline Structure firstly they**

**check authentication**

**If it is fitted or not, if it is fitted then Provider will check the**

**configuration if it is connected, if it finds anything, it will**

**generate the token for authentication.**





Lookups service

• **Lookup Service:-Lookup create a Generic Api. It is very useful in this**

**lookup service you have no need to Write a code for CRUD operation. In**

**this lookup CRUD is On it you can Perform CRUD operation in any**

**Services. You can Import this Lookup service in your component where**

**you want to do CRUD operation.**





Multiple

integration

• **Multiple integration:-With the help of waterfall model you can Perform multiple**

**operation.**

**For Example:- I need to tell three services to perform an one operation. For Example I am**

**wanted to create a user. First maper will create a user and maper create user successfully**

**then they move to next step to create a order otherwise they will run with error. Similary**

**create a Task when the second step Should be positive.**

**Through Connect we can Perform:-**

**(i). Map.**

**(ii). Decoder.**

**(iii). Task.**





Multiple

int egration

• **Multiple integration:- When open one integration to show the pipeline structure. In the integration there are different**

**kind of pipelines like Maper, Decoder, Transform**





Create Integration

**Map:-In showing image defining the map "code":{{ Handler Bar}}**

**For Example:- In sheet:-**

**"code":{{${key data}.Your choice which field you want to convert into code}}",.**

**In sheet name is a field i want to code that body design next to which i hit api**

**which rather than Json where data is coming in a sheet I am taking Json data as I**

**am making array of object, array of Json and mapping this object again on single**

**entity.**

**We can map different fields**

**You want to create an array or object and I can put any detail on it . And you can**

**design object in your choice.**





Workflow





Two Major pa rt of connect:-

\1. Creat e Provider.

2.Creat e Integration

• **Create Provider:- In Provider "Config" you can put Base details on it like base Url,**

**Header in similar way Authentication details and multi-integration. Provider is a single**

**Entity which can have multiple integration.Provider can also relate with Micro Service**

**Which provide a different-different Service like google they have multiple integration like**

**google sheet, google photos when user can login with their gmail all the contact**

**photos etc all are sync .**





• **You can create a provider you can give a Code and Name**

• **Example:- "url":"base url"**

Create Provider.





Create

Integration

• **Create Integration:- A Provider is a single Entity which can**

**have multiple integration but Integration can have only single source**

**which means will be integrated from one place to target provider data**

**can be host and post are different. There is a configuration inside the**

**Integration, which you request and tell inside what you have to do.**





Create

Integration

• **Integration are start after the base url and**

**then Integration url**

**For Example:- xyz/search**

**xyz:-Denote the base url.**

**search:-Denote the integration.**





• **Pipeline And Their Handler:-The handler configuration are get in the database. In Handler there are many**

**Option to handle Csv-Transform, excelhandler, file-to-json, object-to-array and many more.**

**in the under of response decoder name array there is array named decoder but you can put insert multiple**

**decoder.**

Pipeline and their

handler





Description about the

handler and decoder

HttpAction

• **Description:-**

• **In HttpAction you can perform which operation GET, POST, you will define here.**

• **In the under of response decoder name array there is array named decoder but you can put insert**

**multiple decoder.**

• **In handler which you want to handle to csv-transform, excelhandler, file-to-Json, object-to-array**

**and many more.**

• **In script you will give the script path. And pass the data in Source. And then target to where they**

**print and which command(cmd) they run.**

• **And we can add more Decoder on it. And they run till all the the decoder are completed.**

• **Transform will also same as to give a response key to change the transform handler option object-**

**to-array convert.**





Example of major

Paths

• **Description:-**

• **These all are Interrelated one task is performed then another will performed.**

• **Example:-**

• **In Images [http://localhost:3061/api**](http://localhost:3061/api)[ ](http://localhost:3061/api)are base url.**

•

**And [http://localhost:3061/api/data**](http://localhost:3061/api/data)[ ](http://localhost:3061/api/data)is Data service.**

• **And then [http://localhost:3061/api/data/upload**](http://localhost:3061/api/data/upload)[ ](http://localhost:3061/api/data/upload)are action i have perform.**

• **And [http://localhost:3061/api/data/upload/ydff-sales-api**](http://localhost:3061/api/data/upload/ydff-sales-api)[ ](http://localhost:3061/api/data/upload/ydff-sales-api)are the Provider Code.**

• **And [http://localhost:3061/api/data/upload/ydff-sales-api/shipment-tasks.csv**](http://localhost:3061/api/data/upload/ydff-sales-api/shipment-tasks.csv)[ ](http://localhost:3061/api/data/upload/ydff-sales-api/shipment-tasks.csv)are the Integration Code.**

• **These all are interrelated.**





Uploaded sheet

• **Description:- this images shows that the sheet data**

**convert into under the Code All rows and columns**

**are made into a single Json object. and Now one by**

**one inline operation will be run on them.**





Transform and

Map images





Uploaded sheet

• **Description:- If there is a transformation in your array, then it will be transformed, if there is a modification, then the modification**

**will happen, otherwise it will return to map. And whatever details I would have given, whatever URL would have been given, Put,**

**Push and Get it, it will be done and the task will be generated. If you want to show the process on the UI**





Task Generate

• **Description:- After the transformed or modification Task will**

**be Generated. Tasks are under processed Sheet length of**

**updated rows From here we show progress, but if you want to**

**show what**

**percentage is complete after every positive or negative**

**approach Task updates after positive and negative operations are**

**performed on any entity**

