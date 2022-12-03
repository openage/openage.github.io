# Sending an email from the report

---

## Overview
You can use a combine insight and send-it to do a mail merge. 

Here are the steps

1. Create a report in `insight`
2. Create an email template in `send-it`
3. Configure the `insight` report to use the template to send the email at regular intervals

At the given time an insight job would fetch the data and then for each row of data it would use send that data to send-it for merging and delivering the content.

---
## Lets Get Started
For this purpose we will send an email to all the supervisors with list of team members who have not logged-in in last 7 days

---
### Create a report to fetch list of users who have not logged in.
Lets use `not-active-users`. This report gives a list of user who have not logged in since last 7 days.  

This report would have the following columns
1. First Name `profile-firstName`
2. Last Name `profile-lastName`
3. Email `email`
4. Code `role-code`
5. Role `role-name`
6. Role `last-seen`
7. Supervisor First Name `supervisor-profile-firstName`
6. Supervisor Last Name `supervisor-profile-lastName`
7. Supervisor Email `supervisor-email`

Checkout [how to create](insight-report.md) a report for more details.

![[fix-me.jpg]]
TODO: insert image - console>data>report-types

### Next let's create an email template 
Create an email template (code: `inactive-team-members`) with the following body

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

{{data.group.supervisor-profile-firstName}} {{supervisor-profile-lastName}},

<h2>Login Report</h2>
<div style="overflow-x:auto; -webkit-overflow-scrolling: touch;">
    <table cellspacing="0" cellpadding="5px" width="100%">
        <tr>
            <th>S. No.</th>
            <th>Last Logged</th>
            <th>Name</th>
            <th>Email</th>
            <th>Role</th>
        </tr> 
        {{#each group.data}}
        <tr>
            <td>{{sum @index 1}}</td>
            <td>{{lastSeen}}</td>
            <td>{{firstName lastName}}</td>
            <td><a src="{{aka user-profile role-code}}"></a>{{email}}</td>
            <td>{{role-name}}</td>
        </tr> 
        {{/each}}
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


![[fix-me.jpg]]
TODO: insert image - console>templates>emails

Checkout [how to create](templated-message.md) a template message for more details.

### Finally create a job to run the report and send the email

1. Select Time - a [cron expression](https://www.freeformatter.com/cron-expression-generator-quartz.html)
2. Select Email as the  Job Type
3. Select the email template
4. Select the report
5. Add config to group the rows by `supervisor-email` 

![[fix-me.jpg]]
TODO: insert image - console>jobs>insight>new

You can also do this from the report's plugin. See [[report-plugins]] for details.

![[fix-me.jpg]]
TODO: insert image - web-app>report>more>schedule>message 

[[simple-report]]
[[templated-message]]

