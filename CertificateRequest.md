~~~

sequenceDiagram
    participant Developer
    participant ServiceNow
    participant Manager
    participant PIM
    participant TargetSystem
    participant OA_Network
    participant CertPortal
    participant CA

    Developer->>ServiceNow: Log in
    Developer->>ServiceNow: Raise CSR generation request with metadata (target system, hostname, servername)
    ServiceNow->>Manager: Lookup manager and send notification
    Manager->>ServiceNow: Log in and approve production access

    Developer->>PIM: Log in
    Developer->>TargetSystem: Log in
    Developer->>TargetSystem: Run commands to generate CSR
    TargetSystem->>Developer: Provide CSR
    Developer->>OA_Network: Copy CSR out of production environment

    Developer->>CertPortal: Authenticate and log in
    Developer->>CertPortal: Raise certificate request with CSR and metadata (device name, hostname)
    CertPortal->>Manager: Lookup manager and send certificate request
    Manager->>CertPortal: Log in and approve certificate request
    CertPortal->>CA: Send CSR for signing
    CA->>CertPortal: Return signed CRT
    CertPortal->>Developer: Notify CRT ready
    Developer->>OA_Network: Download CRT

    CertPortal->>CertPortal: Log certificate generation and store serial number

    Developer->>ServiceNow: Raise CSR generation request again with metadata
    ServiceNow->>Manager: Lookup manager and send notification
    Manager->>ServiceNow: Approve access

    Developer->>OA_Network: Copy CRT file into production environment
    Developer->>PIM: Log in
    Developer->>TargetSystem: Log in
    Developer->>TargetSystem: Copy CRT to target system
    Developer->>TargetSystem: Install CRT on production system

~~~
