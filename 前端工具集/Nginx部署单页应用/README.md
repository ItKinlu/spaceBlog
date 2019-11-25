# Nginx 部署单页应用

## 多个单页应用部署

```conf
server {
  listen 80;
  server_name localhost;
  index index.html index.htm index.ngingx-debian.html;
  root /home/publish;

  location /manage {
    try_files $uri $uri/ /manage/index.html;
  }

  location /pht{
    try_files  $uri /pht/index.html;
  }

  location / {
    root /home/publish/manage;
    try_files $uri $uri/ /index.html;
  }

  error_page 404 /404.html;
    location = /40x.html {
  }

  error_page 500 502 503 504 /50x.html;
    location = /50x.html {
  }
}
```

## 单页面应用部署

```conf
server {
  listen 2000;
  server_name location;
  root D:\html\dashboard;
  location /{
    try_files $uri $uri/ /index.html;
  }
}
```
