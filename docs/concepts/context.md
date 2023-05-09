## What is context and why is it required?
	
- Context is a rich and highly capable object that is created as soon as a user makes a request to the server.
- For creating the context some permissions (i.e., Role-key, Token-key, session id etc) are required.
- The server first checks the user information from the directory using the role- key provided.
- The directory along with the user information, gives us the information of organisation and tenant. If the tenant doesn’t exist it will create one.
- Other functions from folder node_modules/@open-age/express-api/middlewares/request.js are also added to the context that may be required for the proper functioning of the APIs.
•	Thus, the context is a highly efficient object containing numerous functions.


