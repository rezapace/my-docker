# Cara menjalankan docker

### Unduh Docker Image
```bash
wget https://github.com/rezapace/my-docker/releases/download/v1/devreza.tar.xz
```

### cara `import` container 
```bash
docker import devreza.tar devreza
```

### cara `menjalankan`docker nya
```bash
docker run -d -p 3306:3306 -p 8080:80 -p 8000:8000 --name devreza devreza /bin/bash -c "service apache2 restart && service mysql restart && tail -f /dev/null"
```

### cara `memindahkan` docker nya
```bash
docker cp /home/r/github/template-lms/ devreza:/var/www/
```

### cara cepat `menjalankan` composer nya
```bash
docker exec -it devreza bash -c "cd /var/www/template-lms && php artisan serve --host=0.0.0.0"
```

### cara `masuk ke dalam docker`
```bash
docker exec -it devreza bash
```

### cara `menjalankan php artisan serve`
```bash
php artisan serve --host=0.0.0.0
```

### cara `menjalankan kembali` jika docekr terhenti
```bash
docker start devreza
```


## Akses Website 


### website php my admin
*http://localhost:8080/phpmyadmin/*

username : `root`

password : `p`

---

### website localhost
*http://localhost:8000/nama_file*

---

### website laravel
*http://localhost:8000*


<br>

---
# Cara `Export` Container

### cara export container dengan compresi
```bash
docker export devreza | xz > ralpine.tar.xz
```

### cara tanpa kompresi
```bash
docker export devreza > ralpine.tar
```
---

<br>

# Cara `Load`Docker Image

### cara imprt docker berformat tar
```bash
xz -dc devreza.tar.xz | docker import - devreza
```

### cara menjalankan docker berformat tar
```bash
docker devreza ralpine.tar devreza
```


---

<br>
Note:
- jangan lupa ubah env file nya sesuaikan dengan password dan localhost nya
- jangan lupa untuk import database nya 

---

## cara `import database` dengan command 
```bash
docker exec -i devreza mysql -u root -p -e "CREATE DATABASE demo_db;" && docker exec -i devreza mysql -u root -p demo_db < /home/r/github/template-lms/demo_db.sql
```
---
<br>
<br>
<br>
<br>

---

## Deskripsi

Alur singkat untuk menjalankan Docker container berbasis Alpine, mulai dari unduh image hingga konfigurasi dan export container.

---

### 1. Unduh Docker Image
```bash
wget https://github.com/rezapace/my-docker/releases/download/v1.1/ralpine.tar.xz
```

### 2. Cara Melakukan Import
```bash
xz -d ralpine.tar.xz && docker import ralpine.tar ralpine-image && docker run -it -p 3306:3306 -p 8080:80 --name ralpine ralpine-image /root/start_services.sh
```

### 3. Cara Memindahkan File ke `/var/www` atau `htdocs`
```bash
docker cp /home/r/github/westore/ ralpine:/var/www/
```

### 4. Konfigurasi Apache untuk Akses Direktori
```bash
nano /etc/apache2/httpd.conf
```
```apache
Alias /westore /var/www/westore
<Directory "/var/www/westore">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```
```bash
rc-service apache2 restart
```

### 5. Konfigurasi Apache untuk Akses `localhost/app-weding`
```bash
nano /etc/apache2/httpd.conf
```
```apache
Alias /app-weding /var/www/app-weding
<Directory "/var/www/app-weding">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```
```bash
rc-service apache2 restart
chmod -R 755 /var/www/app-weding
```

---

## Bagian Baru

### 1. Cara Mengecek
```bash
docker exec -it ralpine /bin/sh
cd /var/www
```

### 2. Cara Melakukan Export
```bash
docker export ralpine | xz -9e > ralpine.tar.xz
```

### 3. Install PDO untuk PHP
```bash
apk update
apk add php8-pdo php8-pdo_mysql
nano /etc/php8/php.ini
```
```ini
extension=pdo_mysql.so
```
```bash
rc-service apache2 restart
```

---

## Kesimpulan

Proses cepat untuk mengimpor, menjalankan, memindahkan file, mengonfigurasi Apache, dan melakukan export pada Docker container berbasis Alpine.