# sturdy-guide

## はじめに

### docker-compose入れる
```Bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### pem作成
```Bash
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

### certbot最初
```Bash
docker-compose run --rm certbot certonly --webroot -w /var/www/html -d {hostname} 
```

### 設定フォルダ設定
```Bash
ln -s {PreferencesFolder} ./preferences
```

### 実行できるように
```Bash
sudo chmod a+x reload-nginx.sh
sudo chmod a+x renew-certbot.sh
```

### cronに設定
```crontab
0 0 5,20 * 1 {directory}/reload-nginx.sh
0 0 28 * 1 {directory}/renew-certbot.sh
```


## つかう

### 実行
```Bash
docker-compose up -d FrontNginx
```

### おわる
```Bash
docker-compose down
```

### nginxリロード
```Bash
docker-compose exec -T FrontNginx nginx -s reload
```

### certbot renew
```Bash
docker-compose run --rm certbot renew
```
