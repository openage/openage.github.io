# Hooks

## Trigger

- Hooks are grouped by trigger - after- employee- update
- The web-hook.send needs to be called in the processors for the triggers to fire

## Action

- The action has a code; for an organization to override the tenant setting, you should used the same code within the  trigger
- First pref would be given to organization action followed by tenant and then the one in the config file
- There can be multiple types  of action handlers  in backend
- The handler looks at config and tries to understand what it needs to do
- The url can use the configured service by using its code. So for the code running on the stage - you can make the directory push to organization specific ams

Points to note

- Hooks are independent of services
- For the mechanism to work you need to have a hooks section in config file or tenant object or organization object