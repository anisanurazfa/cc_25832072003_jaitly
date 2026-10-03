# CC M03 - First VPS Deployment

Cloud Computing — PTI 2802  
Pertemuan 3 — Project Inception

## Author
Nama: Anisa Nur Azfa  
NIM: 25832072003  
Kelas: 2A  

## Problem
Membutuhkan infrastruktur deployment Flask yang stabil, aman, dan efisien pada VPS beresource terbatas.

## Target Users
Pengguna umum dan sistem eksternal yang mengakses REST API / Web.

## Features M03
- baseline application
- health endpoint
- VPS deployment

## Architecture

```mermaid
flowchart LR
    U[User] --> C[Caddy]
    C --> G[Gunicorn]
    G --> F[Flask]
Infrastructure
Ubuntu Server 24.04

1 vCPU

1 GB RAM

20 GB disk

Caddy

Gunicorn

Public Endpoint
http://103.59.95.198/

Health Check
GET /health

Deployment
See docs/deployment.md.

Security
key-only SSH

root SSH disabled

UFW enabled

backend loopback-only

Current Limitations
HTTP only

no persistent database

no container

manual deployment
