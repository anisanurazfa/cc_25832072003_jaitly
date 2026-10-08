# Cloud Computing Assignment — Module 04

## Production-like Development Endpoint
- URL: `https://25832072003.103.59.95.198.sslip.io/`
- Health Endpoint: `https://25832072003.103.59.95.198.sslip.io/health`

## Network Architecture
Public entry points:
- TCP/80 → Caddy HTTP redirect / ACME challenge
- TCP/443 → Caddy HTTPS

Internal application:
- `127.0.0.1:8000` → Gunicorn (Flask App)

## DNS
`25832072003.103.59.95.198.sslip.io` resolves via A Record to `103.59.95.198`.

## Security Baseline
- SSH Key authentication
- Active UFW (Ports 22, 80, 443)
- Loopback-only Flask/Gunicorn backend
- Caddy Automatic HTTPS
