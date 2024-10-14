## Understanding User Requests with express-api

This blog post dives into how express-api, an API wrapper for Express.js, handles the flow of user requests. Let's break down the process step-by-step:

**1. The Request Arrives**

A user interacts with your application, triggering a request. This request lands in the `bin/api.js` file, which serves as the entry point for booting up the API.

**2. Permission Check**

Before granting access to the requested functionality, express-api utilizes the context to verify the user's permissions. If the user lacks the necessary permissions, access is denied.

**3. Routing and API Call**

Assuming the user has the green light, express-api directs the request through the defined routes. Once the appropriate route is identified, the corresponding API function is called.

**4. Delegation to api-base.js**

The API function then delegates the task to the `api-base.js` file. This file acts as the central hub, coordinating interactions with services and mappers.

**5. Services Take Action**

`api-base.js` interacts with the services layer. This layer offers essential functionalities like data retrieval (get), searching, data creation, updates, and deletions.

**6. Formatting the Response with Mappers**

Finally, the request reaches the mappers layer. Mappers play a crucial role in transforming raw data retrieved from the services into a user-friendly format suitable for the response.

**7. Sending the Response Back**

Express-api then constructs a well-formatted response using the processed data from mappers and delivers it back to the user's application.

**In essence, express-api acts as a conductor, orchestrating the flow of requests, permission checks, routing, service calls, data formatting, and ultimately, delivering a tailored response to the user.**

	Request ----> bin/api.js  ---> Express API ---> Routes ---> api-base.js file ---> services ---> mappers.

- A user makes a request. The request goes to bin/api.js file for booting purpose.
- Next , before calling the api context is used to check if the user has permissions. It denies in case the user has no permission. 
- If the user has permissions, the api is called. The api then goes to the routes. After creating routes it calls the api-base.js file.
- The api-base.js file mainly uses the services and mappers files.  
- So, next call is made to services. The services mainly provided includes get, search, create, update and delete
- After that mappers is called. The mapper is used to give formatted result to the user.
