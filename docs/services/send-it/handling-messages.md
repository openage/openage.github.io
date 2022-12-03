# Handling a message

## Receiving the message

## Parsing the message meta

A message can have a meta that take properties like

- entity,
- actions,
- conversation-id
- dp,
- category etc

The purpose of this meta is that UI gets this extra information and know-how to react to the notification. Here are some use cases

- on notification click, the UI, from the `entity.type`, can interpret if it has a handler for it and then opens the page/fragment with the details of `entity.id`
- when rendering the notification a list of buttons can be built based on the content of the `actions`
- if there is `conversationId` the user can be taken to the conversation page.
- the notifications can be grouped by `category`
- the notification icon be set to `dp`

The meta can be added to the message in different ways

- adding the meta to the message object
- inheriting the meta from the message template
- 
- 

## Act on message

- Goto entity page
- Inline actions

