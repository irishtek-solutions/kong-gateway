# Kong API Gateway Resources

![Kong Images](./images/Kong-Gateway-Banner.png)

## Basic Configuration


Kong API GAteway provides a comprehensive set of core main entities for managing and securing APIs and microservices. Here is a summary of these core entities:

- **Service:** A "Service" in Kong Konnect represents an API or microservice that you want to manage. It defines the backend API you want to expose, including the URL, name, and other related information.

- **Route:** A "Route" is used to define how requests to a particular Service should be processed. It specifies rules for routing incoming requests to the appropriate Service, including path matching, hostnames, and other criteria. Regex pattern matching is also supported.

- **Consumer:** A "Consumer" represents an entity or application that consumes your APIs. It can be an end-user, application, or system that interacts with your APIs. Consumers can be authenticated and authorized to access specific Services.

- **Plugins:** "Plugins" are extensions that enhance the functionality of Kong Konnect. They can be applied at different levels, such as globally, for specific Services, or for individual Routes. Plugins enable features like authentication, rate limiting, logging, and more.

- **Upstream and Targets:** "Upstream" refers to the backend servers that provide the actual implementation of a Service. "Targets" are specific instances of these backend servers. Kong Konnect can be configured to load balance and distribute incoming requests across these Targets, improving scalability and fault tolerance.

- **Certificates:** "Certificates" are used to secure the communication between clients and Kong Konnect by enabling HTTPS. You can associate SSL/TLS certificates with Services and Routes to ensure data encryption and secure API access.

These core entities in Kong Konnect allow you to effectively manage, secure, and control the flow of API traffic within your organization, making it a powerful tool for API gateway and microservices management.

| Topic           | Content       |  Videos         | Status         |
|-----------------|---------------|-----------------|----------------|
| [Service and Routes](./config/services-and-routes/) | <ul><li>  [ ]  </li>     | <ul><li>  [ ]  </li>     |  Not started
| [Upstreams and targets](./config/upstreams-targets/) | <ul><li>  []  </li>    | <ul><li>  [ ]  </li>   |  Not started
| [Consumers](./config/consumers/) | <ul><li>  [ ]  </li>     | <ul><li>  [ ]  </li>   |  Not started


## Plugins

Plugins extend the functionality of the Kong Gateway. Plugins allow you to easily add new features and functionality to your API. They offer the ability to do things like: 

- Authentication
- Rate Limiting
- Security
- Transformations
- And more…

Plugins can be applied globally or scoped to specific services, consumers or routes. This section gives a breakdown of plugins and how to configure them. 

- Here is a link to our [plugin hub](https://docs.konghq.com/hub/) which has documentation for all available plugins.

#### Authentication plugins

| Topic           | Content       | Videos         | KIC           | Deck           |Status         |
|-----------------|---------------|----------------|---------------|----------------|---------------|
| [Key Authentication](./plugins/authentication/key-authentication/) | <ul><li>  []  </li>  |  <ul><li>  []  </li>  | <ul><li>  []  </li>     | <ul><li>  []  </li>     |<ul><li>  []  </li>    | Not started

#### Security

| Topic           | Content       | Videos         | KIC           | Deck           |Status         |
|-----------------|---------------|----------------|----------------|---------------|----------------|
| [IP Restriction](./plugins/security/ip-restriction/) | <ul><li>  []  </li>  |  <ul><li>  []  </li>  | <ul><li>  []  </li>     | <ul><li>  []  </li>     |<ul><li>  []  </li>    | Not started
| [Rate Limiting Advanced](./plugins/security/rate-limiting-adv/) | <ul><li>  []  </li>  |  <ul><li>  []  </li>  | <ul><li>  []  </li>     | <ul><li>  []  </li>     |<ul><li>  []  </li>    | Not started

#### Transformation

| Topic           | Content       | Videos         | KIC           | Deck           |Status         |
|-----------------|---------------|----------------|---------------|----------------|---------------|
| [Exit Transformer](./plugins/transformation/exit-transformer/) | <ul><li>  []  </li>  |  <ul><li>  []  </li>  | <ul><li>  []  </li>     | <ul><li>  []  </li>     |<ul><li>  []  </li>    | Not started