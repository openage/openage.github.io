# Application Context

An application lives under the context of a `tenant`, `organization` and the `user`

## Tenant

Here is what a tenant looks like

```json
{
    "id": "5bc85dab51c9192adbe45808",
    "code": "app-code",
    "host": "app.domain.com",
    "name": "My App",
    "logo": {
      "url": "{{api-root-url}}/drive/files/logo.jpg"
    },
    "styles": "...",
    "config": {},
    "navs": [...],
    "services": [...],
    "social": [...]
  }
```

It serves the following purposes

1. Branding
   1. name
   2. logo
   3. social links (`social`)
2. Application customization
   1. internationalization  (`meta.i18n`)
   2. taxonomy (`meta.taxonomy`)
3. Look and feel
   1. styles
4. Feature Management
   1. navigation (`navs`)
5. Service Discovery (`services`)

You can GET the details from the following URL `{{api-root-url}}/directory/api/tenants/:identifier`, There are 3 primary identifier in this : `id`, `code`, host:`host`.

In addition, you can get the tenant by specifying it at **header** ( as `x-tenant-code`) or in **query string** ( as `tenant-code`). `{{api-root-url}}/directory/api/tenants/my?tenant-code=:code` fetches you same object

If you specify organization at **header** ( as `x-organization-code`) or in **query string** ( as `organization-code`). The API would override the sections of the object with **the organization specific** values

For example `{{api-root-url}}/directory/api/tenants/my?tenant-code=aqua&organization-code:company` would give you the context which is organization specific


## Organization


## Role


## Owner

TODO
