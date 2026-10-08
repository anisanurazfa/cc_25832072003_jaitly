# Network & Deployment Architecture v0.2

## Deployment View v0.2
```mermaid
flowchart TB
    U[User Device]
    DNS[DNS Resolver]
    AUTH[Authoritative DNS]
    FW1[Provider Firewall]
    UFW[UFW]
    C[Caddy :80/:443]
    G[Gunicorn 127.0.0.1:8000]
    A[Flask]

    U -->|DNS query| DNS
    DNS --> AUTH
    U -->|HTTPS :443| FW1
    FW1 --> UFW
    UFW --> C
    C -->|HTTP loopback| G
    G --> A
Public DNS
25832072003.103.59.95.198.sslip.io A 103.59.95.198

Public Ports
22/tcp — SSH administration

80/tcp — HTTP redirect / ACME challenge

443/tcp — HTTPS

Private Host Port
127.0.0.1:8000 — Gunicorn

TLS
Managed automatically by Caddy through Let's Encrypt / ACME CA.

Data Flow
Browser
  │
  │ DNS Query
  ▼
25832072003.103.59.95.198.sslip.io → 103.59.95.198
  │
  │ TCP/443 + TLS
  ▼
Caddy (Reverse Proxy)
  │
  │ local HTTP (127.0.0.1:8000)
  ▼
Gunicorn
  │
  ▼
Flask Application
