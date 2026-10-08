# Deployment Guidelines — M04

## M04 Secure Endpoint

### DNS
`25832072003.103.59.95.198.sslip.io A 103.59.95.198`

### Firewall
Public TCP:
- 22 (SSH)
- 80 (HTTP / ACME Challenge)
- 443 (HTTPS)

### Reverse Proxy
Caddy terminates TLS and proxies to `127.0.0.1:8000`.

### Validation
```bash
dig +short 25832072003.103.59.95.198.sslip.io A
curl -IL [http://25832072003.103.59.95.198.sslip.io/](http://25832072003.103.59.95.198.sslip.io/)
curl -I [https://25832072003.103.59.95.198.sslip.io/](https://25832072003.103.59.95.198.sslip.io/)
curl [https://25832072003.103.59.95.198.sslip.io/health](https://25832072003.103.59.95.198.sslip.io/health)
