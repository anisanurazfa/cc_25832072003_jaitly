# Networking — M04

## VPS
Public IPv4: `103.59.95.198`

## Interface
Main interface: `ens3`

## Default Route
`default via 105.54.147.1 dev ens3`

## DNS
Domain: `25832072003.103.59.95.198.sslip.io`
Record: A → `103.59.95.198`
AAAA: Not configured

## Public Ports
| Port | Protocol | Purpose |
|---:|---|---|
| 22 | TCP | SSH administration |
| 80 | TCP | HTTP redirect / ACME HTTP-01 |
| 443 | TCP | HTTPS |

## Internal Ports
| Address | Port | Service |
|---|---:|---|
| 127.0.0.1 | 8000 | Gunicorn |

## Firewalls
- IDCloudHost Provider Security Group
- UFW Host Firewall
