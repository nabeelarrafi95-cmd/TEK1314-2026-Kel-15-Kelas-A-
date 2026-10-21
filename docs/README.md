# Logbook Proyek PBL Keamanan Siber - Kelompok 15 Kelas A
**Skenario:** Remote Access Security
**Anggota:**
1. Muhammad Nabeel Ar'Rafi(J0404241028) - Lead Analyst
2. Christian Leonardo Setiawan(J0404241084) - Security Engineer
3. Muhammad Ilham Firdaus(J0404241092) - Security Analyst
4. Tia Nurhasanah(J0404241035) - Security Analyst
---
## Log Aktivitas Mingguan

### Minggu 1-3: Fase Setup & Perancangan Arsitektur
- **Target:** Perancangan Arsitektur Jaringan, Skema IP, serta Instalasi CyberOps VM & Security Onion.

- **Update [10 September 2026]:** 
  - **Aktivitas:** Berhasil instalasi VM utama di Laptop Nabeel.
  - **Kendala:** menginstall security onion secara keseluruhan, memerlukan resource yang besar
  - **Solusi:** menginstall security onion yang ada pada netacad
  - **Artefak:** `docs/laptop_utama/`

- **Update [13 September 2026]:**
  - **Aktivitas:** Melakukan perancangan arsitektur jaringan (Network Diagram) dengan memisahkan zona Attacker (Internet/WAN), Target, dan Monitoring.
  - **Perancangan IP:** Menyusun skema IP Address yang efisien menggunakan metode VLSM (Subnet /24, /29, dan /30).
  - **Pemilihan OS & Service:** Disepakati menggunakan Kali Linux (Attacker), Security Onion (Monitoring Node), dan Debian 13 Server CLI (Target Server) yang akan menjalankan layanan SSH (Port 22), Web (Port 80/443), PostgreSQL (Port 5432), dan IoT/MQTT (Port 1883).
  - **Artefak:** Dokumen `topology.png` dan `ip_plan.md` siap diunggah ke direktori `docs/design/` di GitHub.

- **Update [29 September 2026]:** 
  - **Aktivitas:** Berhasil instalasi VM backup di Laptop Christian.
  - **Kendala:** RAM tidak cukup.
  - **Solusi:** Alokasi RAM diperkecil ke 4GB.
  - **Artefak:** `docs/laptop_backup/`

### Minggu 4-7: Fase Hardening & Baseline
- **Target:** Penguatan OS & Dokumentasi kondisi normal.
- **Update [Tanggal]:**