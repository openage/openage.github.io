# Service Discovery

The system is distributed by nature. You can use the following deployment architecture

1. Open Age Cloud
2. Self-hosted
   - on a popular cloud provider like AWS, GCP, Azure, etc
   - on-premiss servers
3. Hybrid - a combination of Open Age Cloud services and self-hosted services are used

It is suggested, you use the `tenant.services` to discover the services in the **backend** as well as the **frontend** projects

A service can be defined as follows

```js
{
    code: "sensitive-api",
    name: "Sensitive Api",
    url: "https://api.self-hosting.com/api", // default url
    overrides: [{
        provider: "ipAddress",
        config: {
            ipv4: "49.36.150.44"
        },
        url: "https://10.0.0.11:8080/api"
    }, {
        provider: "location",
        config: {
            country: "india"
        },
        url: "https://api-india.self-hosting.com/api"
    }]
    hooks: []
}
```

You can manage this at `https://console.openage.in/system/services`

Here are few use cases

## Completely hosting the service

Use cases:

- there are some sensitive data, for which the system admin needs complete control
- one of the services need to be hosted in LAN for faster access

Steps:

1. Self-host the sensitive service
2. Add the service to the `tenant.services` section
3. Configure your service to use a central auth mechanism

## Separating hosting of service for a specific organization

Use Cases:

- some of the organizations have larger loads and needs separation

Steps:

1. Self-host the sensitive service
2. Add the service to the `tenant.services` section
3. Configure your service to use a central auth mechanism