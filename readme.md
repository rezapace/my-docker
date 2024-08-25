# Cara menjalankan docker

### cara import container 
```bash
docker import devreza.tar devreza
```

### cara menjalankan docker nya
```bash
docker run -d -p 3306:3306 -p 8080:80 -p 8000:8000 --name devreza devreza /bin/bash -c "service apache2 restart && service mysql restart && tail -f /dev/null"
```

### cara memindahkan docker nya
```bash
docker cp /home/r/github/template-lms/ devreza:/var/www/
```

### cara cepat menjalankan composer nya
```bash
docker exec -it devreza bash -c "cd /var/www/template-lms && php artisan serve --host=0.0.0.0"
```

### cara masuk ke dalam docker
```bash
docker exec -it devreza bash
```

### cara menjalankan php artisan serve
```bash
php artisan serve --host=0.0.0.0
```

### cara menjalankan kemabli jika docekr terhenti
```bash
docker start devreza
```


## Akses Website 


### website php my admin
*http://localhost:8080/phpmyadmin/*

username : <a href="#" onclick="navigator.clipboard.writeText('root')">root</a>

password : <a href="#" onclick="navigator.clipboard.writeText('p')">p</a>

---

### website localhost
*http://localhost:8000/nama_file*

---

### website laravel
*http://localhost:8000*


---

# Cara Export Container

### cara export container dengan compresi
```bash
docker export devreza | xz > ralpine.tar.xz
```

### cara tanpa kompresi
```bash
docker export devreza > ralpine.tar
```

---
Note:
- jangan lupa ubah env file nya sesuaikan dengan password dan localhost nya
- jangan lupa untuk import database nya 

---

### cara import database dengan command 
```bash
docker exec -i devreza mysql -u root -p -e "CREATE DATABASE demo_db;" && docker exec -i devreza mysql -u root -p demo_db < /home/r/github/template-lms/demo_db.sql
```
