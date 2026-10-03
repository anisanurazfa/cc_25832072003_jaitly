# Architecture v0.1

## Deployment View
```mermaid
flowchart TB
    I[Internet]
    F[UFW]
    C[Caddy :80]
    G[Gunicorn 127.0.0.1:8000]
    A[Flask]
    I --> F --> C --> G --> A
Resource Constraints
1 vCPU

1 GB RAM

20 GB disk

Security Decisions
non-root administration

SSH key authentication

password SSH disabled

UFW enabled

backend loopback-only

Current Limitations
HTTP only

single VPS

no database

no container

no CI/CD

Planned Evolution
M04 DNS + HTTPS

M05 persistent data

M06 container

M07 IaC

M09 CI/CD
