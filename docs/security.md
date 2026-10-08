# Security Baseline — M04

## Identity and Administration
- Non-root SSH user (`cloudstudent`)
- Public key authentication
- Password SSH disabled

## Network Exposure
Public:
- 22/tcp
- 80/tcp
- 443/tcp

Private to host:
- 127.0.0.1:8000

## Transport Security
- Public HTTPS enabled
- Certificates automatically managed by Caddy (Let's Encrypt)
- Automatic HTTP to HTTPS redirect

## HTTP Response Headers
- X-Content-Type-Options: nosniff
- Referrer-Policy: strict-origin-when-cross-origin
- X-Frame-Options: DENY

## Known Limitations
- Single VPS architecture
- No external WAF
- No centralized log aggregator yet
