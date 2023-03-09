# Sending a templated notification


As our goal is to make an email template we should select sendit templates

Click the new button to create a new template

Enter the required details and Save it
- Name - A name that matches the purpose of email
- Code - should be unique as well as in lowercase
- Category - to which category the required email falls to
- Subscribe - When enabled will send emails to all customers
- Status - For making template active/inactive
- Subject - purpose of email

 Body is same as body of our normal gmail , the place were we write our requirements of email , but here there is a slight difference form our normal email and that is we should write the contents using building blocks of web that is using html , css and js .

In content update we can write our content , in update we can see the code for the same and in preview we can see preview of our content .

There are 4 modes 
- Email - Should enable this if we want to sent an email
- Sms - Should enable for Sms
- Push - Should enable for firebase notifications
- None - If enabled message will not be send

In from enter the mail id of the sender and in to keep the mail id of receiver
In cc enter the details to whom and all you should need to send the copy of the same email

In Data Source we should mention the details of data feteching like key , type , connectionString , headers , feild etc

In actions , it should be mentioned the operations should be performed like put , post , get etc and then details like  handler , title , id also should be defined

Data is patched from the suitable report types

In Console --> System --> Report Types 

## Example
Consider an example to send the login status of Agents

##### Code : agent|tracking
##### Name : Agent Tracking
##### Category : Tracking
##### Subject : Login status of Agents
##### Subscribe : Enable
##### Status : Enable

### Body



```html
<head>
    <style>
        table {
            border: 1px solid #C7C7C7;
            border-radius: 6px;
            padding: 10px;
        }

        th {
            border: 0px;
            text-align: left;
            vertical-align: top;
        }

        td {
            border-width: 1px 0 0 0;
            border-color: #C7C7C7;
            border-style: solid;
            text-align: left;
            vertical-align: top;
        }
    </style>
</head>

{{supervisor.profile.firstName}} {{supervisor.profile.lastName}}

Greetings from Application

{{#with user.profile}}

<h2>Login Report</h2>
<div style="overflow-x:auto; -webkit-overflow-scrolling: touch;">
    <table cellspacing="0" cellpadding="5px" width="100%">
        <tr>
            <th>S. No.</th>
            <th>Last Logged</th>
            <th>Name</th>
            <th>Email</th>
            <th>Role</th>

        </tr> {{#each group.data}}
        <tr>
            <td>{{sum @index 1}}</td>
            <td>{{lastSeen}}</td>
            <td>{{firstName lastName}}</td>
            <td>{{email}}</td>
            <td>{{role}}</td>
        </tr> {{/each}}
    </table>
</div>

{{/with}} 

Best Regards,
{{#if context.user.profile}}
{{context.user.profile.firstName}} {{context.user.profile.lastName}}
{{/if}}
Email: {{context.user.email}}
</html>
```

##### Modes : Email
##### From : context.user.email
##### To : profile.email
##### cc : group.email
### Data Source : 
```json
[
  {
    "key": "agents",
    "provider": "http", 
    "config": {
      "url": "https://insight-api/api/agents?lastSeen=last-week",
      "headers": {
        "x-role-key": "{{context.user.role.key}}"
      }
    },
    "field": "items"
  }
]
```


[[sending-messages]]
