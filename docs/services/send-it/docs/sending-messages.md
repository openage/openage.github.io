# Sending a message

## A generic message

Let's say you want to send a welcome email to another user. It would be something like following

subject: Welcome to Mindful Systems and Solutions
body (HTML):

```html
Dear <b>Sunny Parkash</b>, <br>
<br>
<p>Welcome to <b>Mindful Systems and Solutions</b></p>
<br>
<p>We are so excited to have you on board. Other employees are looking forward to helping you find your way in our company and learn more about what we do here.</p>
<br>
Your skills will be put to good use as we move on to the next quarter and we can't wait to see your work and show off some of your amazing skills. We believe that you will be a great asset to our company.</p>
<br>
<p>Let me know if our team can be of any assistance. Please know that many of us moved here in the past few years and we know how hard it can be to grow accustomed to a new environment. We are here to help you out and give you recommendations on neighborhoods, schools, restaurants, gyms, and everything else you might want to know.</p>
<br>
<p>We are like a big family in our company and we look forward to meeting you and your family once you settle in.</p>
<br>
<p>Looking forward to working with you,</p>
<br>
Rupali Seth<br>
HR Manager<br>
<hr>
Mindful Systems and Solutions
```

To do this, you can POST the following payload to `{{api-root-url}}/sendIt/api/messages`

```json
{
    "to": [{
        "profile": {
            "firstName": "Sunny",
            "lastName": "Parkash"
        },
        "email": "sunny.parkash@gmail.com"
    }],
    "subject": "Welcome to Mindful Systems and Solutions",
    "body": "Dear <b>Sunny Parkash</b>, <br> .........<hr>Mindful Systems and Solutions",
    "attachments": [{
        "filename": "New Joiner.pdf",
        "url": "https://assets.mindfulsas.com/policies/new-joinee.pdf",
        "mimeType": "application/pdf"
    }],
    "options": {
        "modes": {
            "email": true
        }
    }
}
```

The API would take the payload and process it something like this

1. Save the message into the database. When the user tries to get his messages `{{api-root-url}}/sendIt/api/messages?to=my`, he would get it there.
2. It would then understand that it needs to send email `options.modes.email`. It will try to get the configured email channel. If none are configured or active, it would ignore the flag, else it would use the channel to send it ( by downloading and attaching any attachment)
3. The from would be the current user, and it will pick it from the context

### More options

The API supports delivering messages via various types of channels. You can specify that using `options.modes`. The supported modes are

```json
{
    "isHidden": false, // skip saving the message to user's inbox
    "delivery": "first", // options "all", "first" (default) - the api will try one by one via configured channels, once delivered it would stop.
    "modes" : {
        "push": true, // push to the registered devices
        "chat": true, // through registered chat bot to the user's chat it
        "email": true, // registered email
        "sms": true // registered mobile number
    }
}
```

### A templated message

The same welcome message can be send via following payload

```JSON
{
    "data": {
        "user": {
            "profile": {
                "firstName": "Sunny",
                "lastName": "Parkash"
            },
            "email": "sunny.parkash@gmail.com",
        },
        "employment": {
            "code": "1004",
            "designation": {
                "name": "Technical Architect"
            },
            "department": {
                "name": "Solution Delivery"
            }
        }
    },
    "template": {
        "code": "welcome-email"
    }
}
```

There are few advantages of sending a message via a template.

1. The verbiage of the message becomes configurable
2. The configurations supported in the template are
   - the handlebars based on subject and body where the `data` can be injected
   - the metadata that defines how the user interacts with the message
   - the mode of delivery
   - the receiver of the message
   - any pre-configured attachments
3. The `subject`, `body`, `meta`, `to`, `from` are all injectable. The fields that are available for injections are 
   - the `data` that is posted to the API
   - the current `context` { user, organization, tenant }

