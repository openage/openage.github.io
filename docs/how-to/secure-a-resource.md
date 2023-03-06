# Implementing Authorization
#authentication #authorization #security

The current user's permission need to be checked on the UI as well as on the backend

A permission is a token which gets access to a resource. It is a typically defined as `{{resource-type}}.{{access-type}}`. Here are few examples:
- `documents.update`
- `documents.approve`
- `employee.read`

  These permissions are granted to the user based on his `role-type` or can be directly set on the user's role.  There are also some sudo permissions 
- `role:{{role-type-code}}` 
- `email:user@example.com`
- `email:user@example.com`

The sudo permissions helps pin a resource to a user group or a specific user.

## Checking on the Angular App

When the user [logs in](session-login.md) the session is saved on the browser side session. One of the fieds in the session is `user.role.permissions` which is a list of permissions available with the current user.

[Role Service](/lib/web/auth/role-service.md) encapsulate authentication and authroization. It has a method called `hasPermission()` which takes the list of permissions and returns `true` if the current user's has it. 
- To check if the user has permission `document.create` you can call `hasPermission('document.create')` or you can call `hasPermission(['document.create'])`
- It can also check if the user does not have the permission by adding `!` as prefix to the permission you can call `hasPermission('!document.create')`


## Checking access control on a .NET Api

There are 2 level of security that you can implement - at the API or at the action level.

### Securing an API

```C#
[OaAuthorize]
public class DocumentsController : Controller {
	// ...
}
```

### Securing the Action

```C#
public class DocumentsController : Controller {

	[OaAuthorize(Permissions = "document.create")]
	[HttpPost]
	public ApiResult<Document> Create(Document value)
	{
		// ...
	}
}
```

Here is the sudo code for implementation of the `OaAuthorize`. It reads the header for `x-access-token` 

```C#
public class OaAuthorizeAttribute : AuthorizeAttribute
{
	public string[] Permissions { get; set; }
	
	public override void OnAuthorization(AuthorizationContext filterContext)
	{
		Context.Instance = null;
		var token = filterContext.HttpContext.Request.Headers.GetValues("x-access-token");

	if (!token.HasValue())
	{
		// throw access denied
	}

	// get the claims from the token
	Object claims; 
	HttpContext.Current.Session["permissions"] = claims.permissions;

	if (this.Permissions) 
	{
		// if the requested permissions is not in claims.permissions 
		// throw access denied
	}
}
```

Checkout  how to get [current session](current-session.md) on how to get the claims 

The claims are added to the current session so would be available in the deeper code also.