# Heliactyl 14

Versi Heliactyl 14 ini dibuat agar bersih, cepat, dan stabil.  
Versi ini tidak memiliki fitur yang sangat spesifik seperti Linkvertise dan penagihan Stripe, tetapi tetap mempertahankan semua fungsi dari rilis Heliactyl sebelumnya (v11, v12, v13).  

## Peringatan  
- **Heliactyl 14 tidak kompatibel dengan file `settings.json` dari v13 atau versi sebelumnya.**  
- Anda tetap dapat menggunakan file `database.sqlite` yang sama tanpa masalah.  

## Cara Instalasi  

1. **Clone Repository**  
   ```bash
   git clone https://github.com/mhmmdrierie/Heliactyl-14.git

2. Masuk ke Direktori dan Konfigurasi `settings.json`

- Sebagian besar pengaturan bersifat opsional, kecuali:
- Pterodactyl: Wajib dikonfigurasi.
- OAuth2: Wajib dikonfigurasi.

3. Periksa Konfigurasi
   Pastikan semua pengaturan sudah benar.

4. Atur Sertifikat SSL dan Proxy NGINX
   Buat sertifikat SSL untuk domain Anda, lalu atur proxy terbalik menggunakan NGINX.

## Contoh Konfigurasi NGINX

```
nginx
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;

    location /ws {
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      proxy_pass "http://localhost:<port>/ws";
    }

    server_name <domain>;

    ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## Kredit
Saya hanya meng-unggah ulang dan memperbaiki beberapa code pada Heliactyl 14. Author asli Heliactyl ini adalah Matt James & SRYDEN. Inc.
