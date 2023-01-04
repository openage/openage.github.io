[link to api](https://api.application.com/directory)

You will find data about Employees/Users in this api  

# Directory Api
It is the Authentication and Authorization service.

User, once he logs in, gets one or more roles - Each role has 
- a key ( the secret)
- a code ( the human readable text to identify the user)
- set of permission(s).
- an organization (if role is of employment level)

In context of Axon (a tenant in the system) the organization is hospital/clinic.

For example:

A partner can be Admin cum Doctor in Fortis and a simple Doctor in Apollo - so he gets multiple roles.
A patient app user can have multiple roles (without organization) each corresponding to a family member.

The Apps at any point works under one role and uses the set of permissions in that role to show hide features.


## Models

```ts
export class Organization {
  id: string;
  code: string;
  name: string;
  type: string;
  logo: string;
  services?: Service[];
```


## Base Components

### Organization Create

### Organization Signup
```ts
class SignupBaseComponent {

    user: User;

    /*
      creates organization if it does not exist  
    */
    @Input()
    organization: Organization;

    @Output()
    success: EventEmitter<Role>;

    signup(){
    }
}
```

### Employee List
```ts
class EmployeeListBaseComponent {

    @Input()
    readonly: boolean;

    @Input()
    sort: string; 

    @Output()
    created: EventEmitter<Employee>;

    @Output()
    selected: EventEmitter<Employee>;

    items: Employee[];
}
```

## Components

### Organization Signup
```html
<directory-organization-signup></directory-organization-signup>
```

### Employee List
```html
<directory-employee-list></directory-employee-list>
```
