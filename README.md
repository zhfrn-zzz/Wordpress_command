# Hai
## Langkah-langkah di bawah di jalankan berurutan.

### 1. Install LAMP + WordPress (satu blok, jalankan satu per satu)

Install semua dependency
```bash
apt install -y apache2 mysql-server php php-mysql php-curl php-gd php-mbstring php-xml php-zip libapache2-mod-php
```

Buat database
```bash
sudo mysql -e "CREATE DATABASE wordpress; CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'P@ssw0rd123'; GRANT ALL ON wordpress.* TO 'wpuser'@'localhost'; FLUSH PRIVILEGES;"
```

Download & pindahkan WordPress
```bash
cd /tmp
```
```bash
wget -q https://wordpress.org/latest.tar.gz
```
```bash
tar -xzf latest.tar.gz
```
```bash
mv wordpress /var/www/html/
```
```bash
chown -R www-data:www-data /var/www/html/wordpress
```

Aktifkan mod rewrite
```bash
a2enmod rewrite && systemctl restart apache2
```

Konfigurasi wp-config
```bash
cd /var/www/html/wordpress
```
```bash
cp wp-config-sample.php wp-config.php
```
```bash
sed -i "s/database_name_here/wordpress/" wp-config.php
```
```bash
sed -i "s/username_here/wpuser/" wp-config.php
```
```bash
sed -i "s/password_here/P@ssw0rd123/" wp-config.php
```

---

### 2. Selesaikan di Browser

Buka → `http://192.168.10.3/wordpress` → isi wizard → selesai.

---

## Troubleshooting

| Masalah | Solusi |
|---|---|
| SSH gagal | Cek username yang dibuat saat install, bukan asumsi `user`/`root` |
| Root login ditolak | Ubuntu 24.04 default block root SSH — buat user biasa + tambah ke sudo |
| Copy-paste dari browser | Selalu ketik manual atau paste ke notepad dulu — hyperlink merusak command |
