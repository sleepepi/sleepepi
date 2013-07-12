## 500 Front End Server Configuration

Front end servers act as web traffic routers and load balancers to back end servers. Front end servers can specify which back end servers they are using in order to be able to do zero-downtime updates to the back end servers and Ruby on Rails applications.

### sleepclinic.dipr.partners.org

The following is the Nginx routing setup for **sleepclinic.dipr.partners.org**. The important sections for load balancing across the **epiproXX** backend servers are `upstream {}` and `proxy_pass` for specific locations.

```
sudo vi /usr/local/nginx/conf/nginx.conf
```

```
http {

  # ... other configuration here, see https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/173-nginx-configuration.md

  upstream epipros {
    server epipro03.dipr.partners.org;
    server epipro04.dipr.partners.org;
  }

  server {
    listen       80;
    server_name  _;
    rewrite      ^(.*)   https://sleepclinic.dipr.partners.org$1 permanent;
  }

  # HTTPS server
  server {
    listen       443;
    server_name  _;

    ssl                  on;
    ssl_certificate      cert.pem;
    ssl_certificate_key  cert.key;

    ssl_session_timeout  5m;

    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers   on;

    location /slice {
      proxy_pass https://epipros;
    }

  }

}
```
