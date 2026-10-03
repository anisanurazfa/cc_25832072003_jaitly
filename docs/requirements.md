# Requirements

## Problem Statement
Aplikasi backend Flask membutuhkan infrastruktur deployment yang stabil, aman, dan efisien pada lingkungan VPS dengan sumber daya terbatas.

## Target Users
Pengguna umum dan sistem eksternal yang mengakses endpoint REST API / web application.

## Functional Requirements
- FR-01 Aplikasi menyediakan halaman utama (root `/`).
- FR-02 Aplikasi menyediakan endpoint kesehatan sistem (`/health`).
- FR-03 Aplikasi menyediakan endpoint informasi proyek (`/api/info`).

## Non-Functional Requirements
- NFR-01 Backend loopback-only (Gunicorn hanya bind ke 127.0.0.1:8000).
- NFR-02 Application managed by systemd (layanan otomatis berjalan via cc-m03.service).
- NFR-03 Public request through reverse proxy (Caddy menangani port 80 publik).
- NFR-04 No secret in repository.

## Constraints
- 1 vCPU
- 1 GB RAM
- 20 GB disk
- Ubuntu Server 24.04
- Public IPv4

## Acceptance Criteria M03
- [x] First deployment accessible
- [x] Health endpoint works
