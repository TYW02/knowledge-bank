

| Feature     | 2-Tier                        | 3-Tier                              |
| ----------- | ----------------------------- | ----------------------------------- |
| Layers      | Client & Server               | Client, Application, Server         |
| App Logic   | Resides on Client             | Resides in middle Application Layer |
| Scalability | Limited by direct connections | Higher scalability via middle layer |

> In 2-Tier the client directly calls the server via an API call.
> Client -> API Call -> Server

> In 3-Tier the client connects to the application layer which talks to the server
> Client -> Connect -> Application Layer -> Server














