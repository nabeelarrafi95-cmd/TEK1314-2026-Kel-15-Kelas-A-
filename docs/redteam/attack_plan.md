# Dokumen Perencanaan Skenario Serangan Red Team

## Informasi Umum
* **Target Utama (IP):** 192.168.15.2
* **Tujuan Dokumen:** Merancang 3 skenario serangan dari kategori yang berbeda (Reconnaissance, Web/API, dan Availability) sesuai dengan ketentuan penugasan Red Team.

---

## Skenario 1: Reconnaissance - Port dan Service Scanning

* **Kategori (Sesuai Ketentuan):** Reconnaissance
* **Target:** Infrastruktur Server (192.168.15.2)
* **Tools yang Digunakan:** **Nmap** (Network Mapper)
* **Deskripsi Skenario:**
  Tahap awal dari operasi Red Team adalah mengumpulkan informasi (information gathering) sebanyak mungkin mengenai target. Skenario ini bertujuan untuk memetakan permukaan serangan (attack surface) dari server target.
* **Tujuan & Metodologi Konseptual:**
  1. Melakukan identifikasi port TCP/UDP yang berstatus *open* pada IP target.
  2. Melakukan enumerasi untuk mengetahui layanan (service) apa saja yang berjalan pada port yang terbuka tersebut (misalnya, apakah port 80 menjalankan Apache atau Nginx).
  3. Mengidentifikasi versi dari layanan yang berjalan dan sistem operasi (OS fingerprinting) untuk mencari potensi kerentanan (CVE) pada tahap eksploitasi selanjutnya.

---

## Skenario 2: Web Application Attack - SQL Injection (SQLi)

* **Kategori (Sesuai Ketentuan):** Web/API/Protokol IoT
* **Target:** Aplikasi Web yang di-host pada Target Server (192.168.15.2)
* **Tools yang Digunakan:** **Burp Suite** (atau OWASP ZAP)
* **Deskripsi Skenario:**
  Setelah mengetahui adanya layanan web yang berjalan dari tahap *Reconnaissance*, skenario ini akan berfokus pada pengujian keamanan di level aplikasi (Layer 7). SQL Injection dipilih untuk menguji mekanisme validasi input pada aplikasi web target.
* **Tujuan & Metodologi Konseptual:**
  1. Menggunakan *proxy* (seperti Burp Suite) untuk mengintersepsi (intercept) trafik HTTP antara *client* (browser penyerang) dan *server* aplikasi web.
  2. Menganalisis parameter input yang dikirim ke server (seperti form login, parameter URL, atau *cookie*).
  3. Menguji parameter tersebut dengan *payload* SQL khusus untuk melihat apakah aplikasi web mengeksekusi input tersebut sebagai perintah basis data, yang berpotensi memungkinkan *bypass* autentikasi atau ekstraksi data sensitif.

---

## Skenario 3: Availability - Denial of Service (DoS) pada Service

* **Kategori (Sesuai Ketentuan):** Availability (Maks. 1 dari 3 skenario)
* **Target:** Service Web Server (misalnya port 80 atau 443) pada Target Server (192.168.15.2)
* **Tools yang Digunakan:** **hping3**
* **Deskripsi Skenario:**
  Skenario ini bertujuan untuk menguji ketahanan (resilience) layanan web target terhadap lalu lintas jaringan yang tinggi atau anomali. Serangan DoS dilakukan dalam skala lab yang terkontrol dan berfokus hanya pada satu layanan spesifik.
* **Tujuan & Metodologi Konseptual:**
  1. Mensimulasikan serangan *SYN Flood* sederhana menggunakan alat pembuatan paket seperti hping3.
  2. Membanjiri port spesifik layanan web (misal TCP port 80) dengan paket permintaan koneksi (SYN) tanpa menyelesaikan proses *three-way handshake*.
  3. Mengamati apakah sumber daya server web (seperti memori atau koneksi tabel) habis, yang mengakibatkan layanan menjadi tidak tersedia (Denial of Service) bagi pengguna yang sah. Pengujian ini juga berguna untuk melihat apakah ada mekanisme deteksi/mitigasi (seperti *rate limiting* atau firewall) yang aktif.