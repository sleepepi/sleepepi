## 179 Nginx Commands

### Available nginx start and stop commands

```
sudo service nginx stop
sudo service nginx start
sudo service nginx restart
sudo service nginx status
sudo service nginx configtest
```

Note: If Nginx doesn't start, Apache may need to be disabled, see [Pitfall 930](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/900-pitfalls.md#930-nginx-will-not-start-automatically)

### Manual Nginx Start Stop Restart

start

```
sudo /usr/local/nginx/sbin/nginx
```

stop

```
sudo /usr/local/nginx/sbin/nginx -s stop
```

stop alternative (graceful)

```
kill -QUIT $( cat /usr/local/nginx/logs/nginx.pid )
```

restart

```
kill -HUP $( cat /usr/local/nginx/logs/nginx.pid )
```

### Next Step

[180 - Install CoffeeScript](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/180-install-coffeescript.md)
