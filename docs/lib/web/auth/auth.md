

### Session 

```ts
class Session {
    id: string;
    app: string;
    status: string;
    role: Role;
    expiresOn: Date;
}
```

### Role 

```ts
class Role {
  id: string;
  key: string;
  code: string;
  status: string;
  type: string;
  profile: Profile;
  meta: Object;
  organization?: Organization;
  permissions: string[] = [];
}
```

### Profile
```ts
class Profile {
  firstName: string;
  lastName: string;
  pic: {
    url?: string,
    data?: string
  };

  dob: Date;
  fatherName: string;
  bloodGroup: string;
  gender: string;
}
```

## Base Components

### Password based login
```ts
class LoginPasswordBaseComponent {

    email: string;
    mobile: string;
    password: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

```ts
class LoginPasswordResetBaseComponent {

    email: string;
    mobile: string;
    password: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

### OTP based login
```ts
class LoginOtpBaseComponent {

    email: string;
    mobile: string;
    otp = {
        char_1: '',
        char_2: '',
        char_3: '',
        char_4: '',
        char_5: '',
        char_6: ''
    }

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

### OAuth based login
```ts
class LoginFacebookBaseComponent {

    facebookId: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

```ts
class LoginTwitterBaseComponent {

    twitterId: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

```ts
class LoginGoogleBaseComponent {

    googleId: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

```ts
class LoginLinkedInBaseComponent {

    linkedIn: string;

    @Output()
    success: EventEmitter<Role>;

    confirm(){
    }
}
```

### Logout
```ts
class LogoutBaseComponent {

    @Output()
    success: EventEmitter<void>;

    logout(){
    }
}
```


### Current Role
```ts
class CurrentRoleBaseComponent {
    role: Role
}
```

## Components

### Login Controls














