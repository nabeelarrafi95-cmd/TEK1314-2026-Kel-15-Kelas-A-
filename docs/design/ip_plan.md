# Skema IP dan Arsitektur Jaringan (IP Plan)

**Deskripsi Skenario:**
Simulasi serangan dari jaringan eksternal (Internet/Attacker Zone) menuju server target (DMZ/Lokal Zone) yang menjalankan layanan Web, Database (PostgreSQL), dan integrasi IoT. Seluruh lalu lintas jaringan, termasuk upaya eksploitasi, dipantau secara terpusat menggunakan Security Onion.

## Tabel Alokasi IP Address

| Hostname (Role) | IP Address | Subnet Mask | Default Gateway | OS Direncanakan | Open Ports / Services | 
| ----- | ----- | ----- | ----- | ----- | ----- | 
| **Target-Server** (Korban) | `192.168.15.2` | `255.255.255.248` (/29) | `192.168.15.1` | Debian 13 | 22 (SSH), 80/443 (Web), 5432 (PostgreSQL), 1883 (IoT) | 
| **Monitoring Node** (NIDS) | `192.168.15.3` | `255.255.255.248` (/29) | `192.168.15.1` | Security Onion | \- | 
| **Attacker-PC** (Penyerang) | `10.10.15.254` | `255.255.255.0` (/24) | `10.10.15.1` | Kali Linux | \- (Menjalankan Attacking Tools) | 
| **Router Gateway** | `Gig0/0: 192.168.15.1`  `Gig0/1: 10.10.15.1` | `/29`  `/24` | \- | Cisco IOS | Routing  | 
