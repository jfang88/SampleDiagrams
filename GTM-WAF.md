graph TD
    Client["Client"]
    ServiceFQDN["Service / FQDN"]
    GTM["GTM\n(queries 4 endpoints/IPs, returns healthy one)"]

    FW["Firewall"]
    VIP1["VIP 1"]
    VIP2["VIP 2"]
    VIP3["VIP 3"]
    VIP4["VIP 4"]

    WAF1["New OCP WAF Cluster (Primary)"]
    WAF2["CCASS WAFs (Secondary)"]
    WAF3["OCASS WAFs"]
    WAF4["HKATS WAFs"]

    Client --> ServiceFQDN
    ServiceFQDN --> GTM
    GTM --> VIP1
    GTM --> VIP2
    GTM --> VIP3
    GTM --> VIP4

    VIP1 --> FW
    VIP2 --> FW
    VIP3 --> FW
    VIP4 --> FW

    FW --> WAF1
    FW --> WAF2
    FW --> WAF3
    FW --> WAF4
