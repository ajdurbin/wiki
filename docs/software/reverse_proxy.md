//**__Did not finish - not wanting to expose network to WAN__**//

### Installation 

Following `https://www.htpcguides.com/secure-nginx-reverse-proxy-with-lets-encrypt-on-ubuntu-16-04-lts/` and `https://calvin.me/port-forward-web-servers-in-pfsense-2/` and port forwarding 80, 443 in pfsense while also changing web GUI port to not expose it on WAN. 

```
apt-get update
apt-get install nginx -y
unlink /etc/nginx/sites-enabled/default
```

And fill it with 

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name ajdurbin2.ddns.net 192.168.1.207;
    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    
    location ~ /.well-known {
        allow all;
    }
}
```