```mermaid
graph TD
    Client["Client"]
    ServiceFQDN["Service / FQDN"]
    GTM["GTM\n(queries 4 endpoints/IPs, returns healthy one)"]

    subgraph Firewall
        direction TB
        VIP1["VIP 1"]
        VIP2["VIP 2"]
        VIP3["VIP 3"]
        VIP4["VIP 4"]
    end

    WAF1["New WAF Cluster (Primary)"]
    WAF2["Old2 WAFs (Secondary)"]
    WAF3["Old3 WAFs"]
    WAF4["Old4 WAFs"]

    VPC1["New Services"]
    VPC2["Old2 services"]
    VPC3["Old3 Services"]
    VPC4["Old4 Services"]

    Client --> ServiceFQDN
    ServiceFQDN --> GTM
    GTM --> Client

    GTM --> VIP1
    GTM --> VIP2
    GTM --> VIP3
    GTM --> VIP4

    VIP1 --> WAF1
    VIP2 --> WAF2
    VIP3 --> WAF3
    VIP4 --> WAF4

    WAF1 --> VPC1
    WAF2 --> VPC2
    WAF3 --> VPC3
    WAF4 --> VPC4


```
