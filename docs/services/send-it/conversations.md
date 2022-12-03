# Conversations

## The message threads

Message can be grouped by few attributes. The supported grouping attributes are `conversation` and `entity`

When sending a message you can add a conversation object to the payload. You can then get the messages by that conversion `{{api-root-url}}/sendIt/api/messages?conversation-id=5eae92f22e77d50ac2770017`

```json
{
    ...
    "conversation": {
        "id": "5eae92f22e77d50ac2770017"
    }
    ...
}
```

The conversation has a list of `participants`. When a message is added to it, the API

- adds it the conversation
- adds it as the last conversation
- if the conversation has any publish mechanism configured (external chat platforms), it sends the message to that platform
- in case there are mentions or to in the messages, a notification is sent to that user. It would take the mentions and convert them to `a` tags with `role-id`. The supported mentions are
  - everyone  `@everyone`
  - by user code `@1004`
  - by role id `@5eae92f22e77d50ac2770017` or `<a href="@r5eae92f22e77d50ac2770017">Sunny Parkash</a>`

You can have a `direct` conversation between 2 users, or create a `group` conversation with a custom name and pic. You can even have `entity` level conversations

## Entity level conversations

The conversations are designed to be used as plugins. All they need is the entity to which they can be attached.

Here are some recommendations

- Get a conversation by entity GET `{{api-root-url}}/sendIt/api/conversations/entity?entity-id=123&entity-type=task`. The backend would create the conversation if it does not exist and return you always the same

- Create a control/component/fragment that has a list of messages with an input to add a new one. Take `entity` as the input parameter for that control. Then design the page that joins the entity detail control and conversation control.
  
- To be able to add a message to this conversation, just POST to `{{api-root-url}}/sendIt/api/messages` a message with conversation

```json
{
    "subject": "the task was rejected",
    "body": "the work is not complete",
    "conversation": {
        "entity": {
            "id": "123",
            "type": "task"
        }
    }
}
```
This message would automatically be added to the conversation
