```mermaid
sequenceDiagram

    actor Client
    participant Server
    participant Database

    Client->>Server: Login (Username, Password)
    activate Server
    Server->>Database: Select User Info
    note over Database: Password is not stored
    Database-->>Server: Salt & Hash
    deactivate Database
    Server-->>Client: 200 OK & JWT


```
