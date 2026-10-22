# Logbook PBL Keamanan Siber - Kelompok 15

**TEK1314 Keamanan Siber** | Kelas A | Skenario Remote Access Security

## Anggota & Peran

| Nama | NIM | Peran | 
| ----- | ----- | ----- | 
| Muhammad Nabeel Ar'Rafi | J0404241028 | Lead | 
| Christian Leonardo Setiawan | J0404241084 | Red Team | 
| Muhammad Ilham Firdaus | J0404241092 | Blue Team | 
| Tia Nurhasanah | J0404241035 | Blue Team | 

## Log Mingguan

**Minggu 1-3, setup.** Instalasi CyberOps VM dan Security Onion di laptop utama (Nabeel). Sempat terkendala resource berat, diselesaikan dengan menggunakan Security Onion versi Netacad (2026-09-10). Instalasi VM backup di laptop Christian dengan penyesuaian alokasi RAM diturunkan menjadi 4GB (2026-09-29). Bukti di `docs/laptop_utama/` dan `docs/laptop_backup/`.

**Minggu 4, topologi dan IP.** Perancangan arsitektur jaringan memisahkan zona Attacker (Internet/WAN), Target, dan Monitoring. Skema IP Address disusun efisien menggunakan metode VLSM (Subnet /24, /29, dan /30). Pemilihan OS & Service menggunakan Kali Linux (Attacker), Security Onion (Monitoring Node), dan Debian 13 Server CLI (Target Server: Port 22, 80/443, 5432, 1883) (2026-09-13). Bukti di [`docs/design/`](docs/design/).

**Minggu 5-6, praktikum.** Belum ada tambahan.

**Minggu 7-8, UTS.** UTS praktikum dan UTS, tanpa deliverable proyek.

**Minggu 9, checkpoint.** 9 kontrol hardening dieksekusi dengan bukti, deklarasi tech stack, attack plan 3 skenario

## Status Deliverable

| Deliverable | Status | 
| ----- | ----- | 
| Topologi dan IP plan | selesai | 
| Deklarasi tech stack | selesai | 
| Slide presentasi (`slides.pdf`) | belum | 
| Hardening checklist dan bukti | Selesai 7, on going 2, pending 3 | 
| Attack plan Fase 2 | selesai, 3 skenario | 
| Purple team log | kerangka, diisi Minggu 10-11 | 
| Vulnerability Assessment Report | belum, Minggu 11 | 

## Isi Repositori

`docs/design/` topologi dan IP plan | `docs/laptop_utama/` & `docs/laptop_backup/` bukti setup VM | `docs/presentation-minggu9/` tech stack dan slide | `docs/blueteam/` checklist hardening dan bukti | `docs/redteam/` attack plan dan bukti serangan | `docs/purple-team-log.md` log 5 tahap