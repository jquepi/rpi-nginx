# rpi-nginx

## Custom Nginx Configuration
Running behind [rpi-nginx-proxy](https://github.com/lroguet/rpi-nginx-proxy)? Here's a Nginx configuration for the default site.

```
# /etc/nginx/sites-enabled/default
server {

  listen 80 default_server;
  listen [::]:80 default_server;

  root /var/www/html;

  # Add index.php to the list if you are using PHP
  index index.html index.htm index.nginx-debian.html;

  server_name _;

  # Headers from the proxy
  real_ip_header X-Forwarded-For;
  set_real_ip_from 172.17.0.0/16;

  location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404.
    try_files $uri $uri/ =404;
  }

}
```

## Resources
* [Docker Hub](https://hub.docker.com/r/lroguet/rpi-nginx/)
* [In action](http://lab.fourteenislands.io/nginx-reverse-proxy-docker-and-a-raspberry-pi/)