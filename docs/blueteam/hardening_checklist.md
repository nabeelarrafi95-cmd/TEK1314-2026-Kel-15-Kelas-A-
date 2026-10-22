# Hardening Checklist — Target Node (Sistem MUSH)

**Target:** `192.168.15.2` (`target-kel15` / `target-mush`)

**OS:** Debian 13

**Gateway Router:** MikroTik CHR (`192.168.15.1` / `10.10.15.1`)

**Standar Minimal:** Minimal 8 kontrol, dengan minimal 2 kontrol di setiap kategori A, B, dan C. Setiap kontrol dilengkapi bukti sebelum dan sesudah konfigurasi.

Seluruh bukti tersimpan di folder `evidence/`. File dengan awalan `before` berisi kondisi awal, sedangkan file dengan awalan `after` berisi hasil setelah hardening.

## Ringkasan Status

| Kategori | Selesai | Sebagian | Belum | Total | 
| ----- | ----- | ----- | ----- | ----- | 
| **A. Access & Authentication** | 4 | 1 | 0 | 5 | 
| **B. Service & Attack Surface** | 3 | 1 | 0 | 4 | 
| **C. Data & Application** | 0 | 0 | 3 | 3 | 
| **Total** | **7** | **2** | **3** | **12** | 

## A. Access & Authentication

| Kontrol | Target Konfigurasi / Parameter | Status | Bukti | 
| ----- | ----- | ----- | ----- | 
| **A.1** Menonaktifkan SSH Root Login | Set `PermitRootLogin no` pada konfigurasi SSH | Selesai | Before konfigurasi: [before menonaktifkan ssh root login.png](evidence/before%20menonaktifkan%20ssh%20root%20login.png) · After konfigurasi: [after menonaktifkan ssh root login.png](evidence/after%20menonaktifkan%20ssh%20root%20login.png) | 
| **A.2** Membuat SSH Key based auth | Set `PubkeyAuthentication yes` | Selesai | Before konfigurasi: [before ssh key-based auth.png](evidence/before%20ssh%20key-based%20auth.png) · After konfigurasi: [after ssh key-based auth.png](evidence/after%20ssh%20key-based%20auth.png) | 
| **A.3** Menonaktifkan Password Auth | Set `PasswordAuthentication no` | Selesai | Before konfigurasi: [before password auth disbale.png](evidence/before%20password%20auth%20disbale.png) · After konfigurasi: [after ssh password auth disable.png](evidence/after%20ssh%20password%20auth%20disable.png) | 
| **A.4** Membatasi Percobaan Login SSH | Set `MaxAuthTries 3` | Selesai | Before konfigurasi: [before membantasi percobaan login ssh.png](evidence/before%20membantasi%20percobaan%20login%20ssh.png) · After konfigurasi: [after membatasi percobaan login ssh.png](evidence/after%20membatasi%20percobaan%20login%20ssh.png) | 
| **A.5** Mengaktifkan Fail2ban | Proteksi dari percobaan *brute force* | Sebagian | Sebelum · Status Fail2ban · IP Banned | 

## B. Service & Attack Surface

| Kontrol | Target Konfigurasi / Parameter | Status | Bukti | 
| ----- | ----- | ----- | ----- | 
| **B.1** Mengaktifkan Firewall (UFW) Default Deny | Kebijakan default `default deny incoming`, `default allow outgoing` | Selesai | Before konfigurasi: [before ufw aktif.png](evidence/before%20ufw%20aktif.png) · After konfigurasi: [after ufw aktif.png](evidence/after%20ufw%20aktif.png) | 
| **B.2** Membatasi Port Akses Layanan Utama | Hanya membuka Port 22 (SSH), 80/443 (Web), 1883 (MQTT), dan 5432 (PostgreSQL) | Selesai | Before konfigurasi: [before ufw aktif.png](evidence/before%20ufw%20aktif.png) · After konfigurasi: [after membatasi open port.png](evidence/after%20membatasi%20open%20port.png) | 
| **B.3** Pembaruan Sistem Operasi & Paket Debian 13 | Memastikan update dan upgrade paket sistem dilakukan serta pembersihan paket tidak terpakai | Selesai | Before konfigurasi: [before update & upgrade sistem.png](evidence/before%20update%20%26%20upgrade%20sistem.png) · After konfigurasi: [after update & upgrade sistem.png](evidence/after%20update%20%26%20upgrade%20sistem.png) | 
| **B.4** Centralized log monitoring | Mengonfigurasi service syslog untuk mengirimkan log audit ke Centralized Syslog Collector | Sebagian | Sebelum · Konfigurasi Forwarder · Log Diterima Collector | 

## C. Data & Application

| Kontrol | Target Konfigurasi / Parameter | Status | Bukti | 
| ----- | ----- | ----- | ----- | 
| **C.1** Membatasi Hak Akses (*Permission*) File Konfigurasi | Set permission `600` / `640` pada file konfigurasi sensitif (MQTT, basis data, dan environment Web) | Belum | Sebelum · Sesudah | 
| **C.2** Menghapus Default User & Password PostgreSQL | Menghapus akun default `postgres` beserta password standarnya, serta mewajibkan penggunaan user khusus aplikasi | Belum | Sebelum · Konfigurasi DB · Bukti Kredensial Default Dihapus | 
| **C.3** Rate Limiting pada Akses Website | Membatasi *request rate* (misal max 10-20 req/menit per IP) saat mengakses halaman website MUSH | Belum | Uji Rate Limit HTTP | 
