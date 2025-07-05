# server-seminar
멋쟁이사자처럼 13기 백엔드 세미나를 위한 API

## NGINX 파일 (퍼가요~^^)
***주의사항: [내이름]은 꼼꼼히 잘 채우기!!! (총 4군데 있습니다)***
```nginx
server {
    listen 80;
    server_name babylion-[내이름(1)].duckdns.org;
    
    # HTTP를 HTTPS로 리다이렉트
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name babylion-[내이름(2)].duckdns.org;
    
    # SSL 인증서 경로 (이미 발급됨)
    ssl_certificate /etc/letsencrypt/live/babylion-[내이름(3)].duckdns.org/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/babylion-[내이름(4)].duckdns.org/privkey.pem;
    
    # Django 애플리케이션으로 요청 전달
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
