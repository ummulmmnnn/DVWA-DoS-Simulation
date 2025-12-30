# Dokumentasi Praktikum: Instalasi DVWA & Simulasi Serangan DoS (Hping3)

## Pendahuluan
Praktikum ini bertujuan untuk membangun lingkungan web server yang rentan menggunakan **DVWA (Damn Vulnerable Web Application)** dan menguji ketahanan server tersebut terhadap berbagai jenis serangan *Denial of Service* (DoS) menggunakan alat **Hping3** dan **Nmap**.

---

## 1. Instalasi & Konfigurasi Sistem
Tahap ini mencakup penyiapan infrastruktur server agar aplikasi dapat berjalan dengan benar.

* **Konfigurasi Database**: Menyiapkan MariaDB untuk penyimpanan data aplikasi DVWA.
* **Sinkronisasi Kredensial**: Mengatur file `config.inc.php` agar aplikasi dapat terhubung ke database menggunakan user dan password yang sesuai.
* **Optimasi PHP**: Mengaktifkan fungsi `allow_url_include` dan `allow_url_fopen` pada file `php.ini` untuk mendukung simulasi kerentanan tertentu.
* **Restart Service**: Menjalankan perintah `service apache2 restart` untuk memuat ulang konfigurasi dan mengaktifkan web server.

---

## 2. Pemeriksaan Sistem (Reconnaissance)
Sebelum serangan dilakukan, dilakukan verifikasi status sistem melalui interface web dan alat pemindaian port.

* **Setup Check**: Memastikan seluruh prasyarat sistem berstatus 'Enabled' atau hijau pada halaman setup DVWA.
* **Login**: Masuk ke dasbor utama menggunakan kredensial standar (admin/password).
* **Nmap Scanning**: Melakukan pemindaian port menggunakan `nmap -p 1-100 127.0.0.1` untuk memastikan port 80 (HTTP) berstatus *open*.

---

## 3. Simulasi Serangan DoS (Hping3)
Pengujian ketahanan server dilakukan dengan berbagai metode pengiriman paket masif.

* **SYN Flood Attack**: Menggunakan mode flood (`--flood`) ke port 80. Hasil statistik menunjukkan pengiriman lebih dari 11 juta paket yang mengakibatkan **100% packet loss**.
* **ICMP Flood**: Membanjiri jalur komunikasi ICMP dengan interval ultra-cepat (`-i u10`) untuk menguji respons dasar jaringan.
* **ICMP Smurf Attack**: Melakukan serangan refleksi melalui alamat broadcast (`.255`) yang menyebabkan lonjakan latensi (RTT) hingga **1003.0 ms**, menandakan kongesti jaringan yang parah.

---

## Kesimpulan
Berdasarkan hasil praktikum, dapat disimpulkan bahwa:
1. Konfigurasi parameter PHP dan database yang tepat sangat krusial bagi fungsionalitas aplikasi web.
2. Server tanpa proteksi keamanan (seperti firewall atau rate limiting) sangat rentan terhadap serangan DoS.
3. Serangan SYN Flood terbukti paling efektif melumpuhkan layanan web server secara total (100% packet loss) dibandingkan metode lainnya dalam skenario ini.

---
## Link Video
https://youtu.be/mR_0F09cbL8?si=NkOOlUOLkqQbsWwp



*Dokumentasi ini dibuat untuk tujuan edukasi dalam lingkup praktikum keamanan jaringan.*
