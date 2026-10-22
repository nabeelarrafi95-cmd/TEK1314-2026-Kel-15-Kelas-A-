# Deklarasi Tech Stack — Sistem MUSH (Keamanan Siber)

**Kelompok:** Kelompok 15 / Kelas A (Teknologi Rekayasa Komputer)

**Sistem Acuan:** MUSH (Monitoring Fermentasi Berbasis IoT)

## 1. Ringkasan Sistem & Arsitektur Keamanan

Sistem MUSH pada praktikum Keamanan Siber berfokus pada pengamanan infrastruktur *backend*, basis data, dan jalur komunikasi IoT. Server Target (`192.168.15.2`) difungsikan sebagai node utama yang menyediakan beberapa layanan terbuka (*attack surface*) untuk simulasi pengujian keamanan.

Lalu lintas data dari *Attacker Zone* (`10.10.15.0/24`) menuju *Target Zone* (`192.168.15.0/29`) dihubungkan melalui **MikroTik CHR** sebagai *router gateway*. Seluruh aktivitas sistem dan log kejadian pada Target Server dipantau secara terpusat menggunakan layanan **Syslog**.

## 2. Pemetaan Tech Stack

| Komponen | Implementasi (Asli & Replika) | Port / Parameter | Function / Security Focus | 
| ----- | ----- | ----- | ----- | 
| **Sistem Operasi** | Debian 13 | Host (`192.168.15.2/29`) | Server *backend* & target simulasi | 
|  | 
| **Akses Server** | ssh key-based auth | Port `22` | Akses administrasi (*password auth* nonaktif) | 
| **Web Server** | Nginx | Port `80` / `443` | Web server & jalur API / *Reverse Proxy* | 
| **Dashboard** | React.JS | Disajikan via Web Server | Antarmuka pengguna (*Frontend*) | 
| **Database** | PostgreSQL | Port `5432` | Penyimpanan data *telemetry* & autentikasi | 
| **Protokol Komunikasi IoT** | MQTT | Port `1883` | Jalur penerimaan data sensor dari *gateway* | 
|  | 

## 3. Batasan Implementasi & Vektor Keamanan

* **Vektor Serangan (*Attack Surface*):**

  * Port `22` (SSH): Pengujian konfigurasi autentikasi berbasis *ssh key*.

  * Port `80/443` (Nginx & React.JS): Pengujian celah keamanan pada aplikasi web, *dashboard frontend*, dan konfigurasi server.

  * Port `5432` (PostgreSQL): Pengujian keamanan akses dan kredensial basis data.

  * Port `1883` (MQTT): Pengujian otentikasi *broker* dan interseptikasi pesan IoT.

* **Penyesuaian Simulasi Lab:**

  * **Penyederhanaan IoT:** Data sensor dikirimkan menggunakan skrip sintetis (*publisher* MQTT) menuju port 1883 untuk mensimulasikan trafik *telemetry*.

  * **Pengawasan:** Seluruh *event log* dari autentikasi SSH, basis data, dan *web server* dikirimkan secara langsung ke SIEM via **Syslog**.