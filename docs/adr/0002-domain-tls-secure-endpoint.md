# ADR-0002: Public DNS and TLS Termination with Caddy

## Status
Accepted

## Context
M03 menggunakan public IPv4 dan HTTP.
M04 membutuhkan hostname stabil dan secure endpoint.
VPS memiliki 2 vCPU, 2 GB RAM, Ubuntu Server 24.04.

## Decision
- gunakan subdomain publik sslip.io (`25832072003.103.59.95.198.sslip.io`);
- gunakan A record ke public IPv4 VPS (`103.59.95.198`);
- jangan membuat AAAA tanpa IPv6 yang valid;
- gunakan Caddy sebagai TLS terminator dan reverse proxy;
- pertahankan Gunicorn pada 127.0.0.1:8000;
- buka TCP/80 dan TCP/443;
- gunakan automatic HTTPS Caddy.

## Alternatives Considered
1. NGINX + Certbot
2. Apache + Certbot
3. aplikasi melayani TLS langsung
4. self-signed certificate
5. akses berbasis IP tanpa domain

## Rationale
- Footprint ringan pada VPS.
- Otomatisasi sertifikat HTTPS gratis melalui ACME/Let's Encrypt.
- Kemudahan pemeliharaan dan pemisahan fungsi backend/proxy.

## Consequences
### Positive
- Valid public HTTPS.
- Sertifikat SSL diperbarui otomatis.
- Backend aman di jaringan lokal host.
### Negative
- Tergantung pada ketersediaan CA Let's Encrypt & DNS.

## Risks
- Terkena rate limit Let's Encrypt jika diterbitkan ulang secara berkala dalam rentang pendek.

## Review Trigger
Tinjau jika berpindah provider atau beralih ke container/kubernetes.
