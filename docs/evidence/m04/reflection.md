# Refleksi Individu — Modul 04

## 1. Layer yang Paling Sulit Dipahami
Layer yang paling memerlukan perhatian adalah integrasi antara DNS Resolution dan Automatic HTTPS pada Caddy. Memahami bagaimana Caddy melakukan mekanisme ACME HTTP-01 challenge secara otomatis dengan memanfaatkan Port 80 sebelum mengaktifkan Port 443 membutuhkan pemahaman alur jaringan yang runtut.

## 2. Perbedaan Akses IP dan Domain
Akses berbasis IP hanya mengarahkan trafik langsung ke antarmuka host tanpa identitas nama dan tidak dapat menggunakan sertifikat TLS publik yang valid secara standar. Sementara akses domain memberikan abstraksi hostname yang stabil, memungkinkan penggunaan Virtual Host/Routing berbasis Server Name Indication (SNI), serta memungkinkan penerbitan sertifikat SSL/TLS publik gratis melalui CA seperti Let's Encrypt.

## 3. Bukti DNS Benar
DNS terbukti benar ketika query seperti `dig +short 25832072003.103.59.95.198.sslip.io A` atau `Resolve-DnsName` konsisten mengembalikan IP publik VPS (`103.59.95.198`) dari berbagai resolver.

## 4. Bukti TLS Benar
TLS terbukti benar ketika pengujian `openssl s_client -connect 25832072003.103.59.95.198.sslip.io:443 -servername 25832072003.103.59.95.198.sslip.io` mengembalikan rantai sertifikat valid yang diterbitkan oleh Let's Encrypt tanpa ada peringatan keamanan (warning) pada browser.

## 5. Bukti Backend Tidak Public
Backend terbukti tidak terekspos secara publik karena Gunicorn hanya melakukan binding pada socket loopback `127.0.0.1:8000` (`sudo ss -lntp`), dan Port 8000 tidak dibuka pada UFW maupun Security Group provider. Akses ke backend hanya bisa dilakukan secara internal melalui Caddy sebagai reverse proxy.

## 6. Urutan Diagnosis Jika Endpoint Gagal
Jika endpoint mengalami kegagalan, urutan diagnosis berbasis layer yang digunakan adalah:
1. **DNS**: Memastikan domain resolve ke IP VPS (`dig`).
2. **Network & Firewall**: Memastikan Port 80 dan 443 terbuka dan reachable (`nc` / `Test-NetConnection`).
3. **TLS**: Memastikan sertifikat aktif dan tidak expired (`openssl` / `journalctl -u caddy`).
4. **Reverse Proxy & Backend**: Memastikan service Caddy dan cc-m03 aktif, serta backend lokal mengembalikan response 200 OK (`curl http://127.0.0.1:8000/health`).
