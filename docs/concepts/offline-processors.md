# Event-Driven Architecture

## Overview

The Event-Driven Architecture (EDA) is designed to handle events, such as user creation or updates, which can initiate a series of actions within a microservices ecosystem. EDA provides a robust framework for managing these events and their corresponding actions.

### Step 1: Initiating Events

Events are captured and queued with specific attributes:

1. **Entity Type**: Defines the entity associated with the event.
2. **Event Type**: Describes the event’s nature.
3. **Entity Data**: Carries the details of the entity involved.
4. **Context**: Holds the metadata about the current event.

For instance, to enqueue an event for a new user creation:

JavaScript

```JavaScript
const offlineProcessor = require('@open-age/offline-processor');
...
...
async function createUser(model, context) {
    ...
    await model.save();
    ...
    await offlineProcessor.enqueue('user', 'created', model, context);
    ...
    return model;
}
```

AI-generated code. Review and use carefully. .

### Step 2: Processing Events

The EDA locates the appropriate event handler using conventions, searching paths like:

- For JavaScript files: `{app-root}/handlers/{entity-type}/{event-type}.js`
- For directories: `{app-root}/handlers/{entity-type}/{event-type}`

Or by setting up a `queueProcessor` configuration:

JSON

```JSON
{
    "queueServer": {
        "handlers": {
            "default": {
                "directory": "defaults",
                "handlerFile": "default-handler.js"
            }
        },
        ...
    }
}
```

AI-generated code. Review and use carefully. .

Upon locating the handler, the `offline-processor` invokes its `process` function:

JavaScript

```JavaScript
exports.handle = async (data, context) => {
    // Define the action to be taken
    ...
}
```

AI-generated code. Review and use carefully. .

Or it may trigger a workflow using a composer:

JavaScript

```JavaScript
const workflowComposer = require('@open-age/composer-client');

exports.handle = async (data, context) => {
    await workflowComposer.createTask({
        taskType: 'userCreation',
        payload: { userId: data.id }
    }, context);
}
```

AI-generated code. Review and use carefully. .

### Step 3: Responding to Events

The response to an event can vary. Here’s how to trigger a webhook:

JavaScript

```JavaScript
const webhookHelper = require('../../utilities/webhook-helper');

exports.handle = async (data, context) => {
    // Execute the desired action
    await webhookHelper.trigger({
        targetEntity: 'user',
        operation: 'created',
        timing: 'post'
    }, data, context);
}
```

AI-generated code. Review and use carefully. .

The webhook configuration might look like this:

JSON

```JSON
{
    "webhookTrigger": {
        "targetEntity": "user",
        "operation": "created"
    },
    "webhookActions": []
}
```

AI-generated code. Review and use carefully. .

Based on this configuration, the handler can execute a series of actions.

## Action Types

### Web Service Call

JSON

```JSON
{
    "actionType": "webService",
    "serviceHandler": "userManagementBackend",
    "identifier": "syncUserToService",
    "serviceConfig": {
        "endpointURL": "http://localhost:9001/api/users",
        "method": "POST",
        "headers": {
            "Content-Type": "application/json",
            "Authorization": "Bearer ${context.token}"
        },
        "dataMapper": {
            "userId": "user.id"
        }
    }
}
```

AI-generated code. Review and use carefully. .

This revised document aims to provide clarity and practical examples to help developers understand and implement the `offline-processor` in their event-driven systems