## 450 Install Slice

### 451 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

[LaTeX Installation](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/800-extra-dependencies.md)

### 452 Downloading source from Git

```
cd /usr/local/production
git clone git://github.com/remomueller/slice.git www.tryslice.io
```

NOTE: If you get `fatal: could not create work tree dir 'www.tryslice.io'.: Permission denied` that means you forgot to run:

```
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 453 Initialize database and files

```
cd /usr/local/production/www.tryslice.io
```

```
bundle install
```

```
ruby lib/initial_setup.rb

  Database User:      slice
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      pgsql.dipr.partners.org

  SMTP Address:       mail.hover.com
  SMTP Port:          587
  SMTP User Name:     support@tryslice.io
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://tryslice.io

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro03* since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/www.tryslice.io/config/
    |-- application.yml
    `-- database.yml
```

```
scp username@epipro03.dipr.partners.org:/usr/local/production/www.tryslice.io/config/application.yml /usr/local/production/www.tryslice.io/config/application.yml
scp username@epipro03.dipr.partners.org:/usr/local/production/www.tryslice.io/config/database.yml /usr/local/production/www.tryslice.io/config/database.yml
```

#### Setup Shared RFA folder for uploads

Follow the [Automount Installation Instructions](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/190-install-rails-applications.md#installing-automount-and-cifs-to-mount-folders-from-the-rfa) that are provided if you haven't installed the required automount libraries.

Slice requires the following in `/etc/auto.master`:

```
/- /etc/auto.slice
```

Slice also requires the additional file `/etc/auto.slice`:

```
/usr/local/production/slice/carrierwave -fstype=cifs,uid=3051303,gid=100001,credentials=/etc/auto.secret ://rfa01.research.partners.org/bwh-sleepepi-web/production/slice/carrierwave
```

Run the following to activate the new mount:

```
sudo service autofs restart
```

### 454 Update Nginx Configuration

#### Create symbolic link

```
sudo ln -s /usr/local/production/slice/public /var/www/html/slice
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```
passenger_base_uri /slice;
```

Restart nginx

```
sudo service nginx restart
```

### 455 Update nginx Configuration on slice

On **slice**

Login in to slice:

```
ssh username@slice.dipr.partners.org
```

Edit nginx configuration file

```
sudo vi /usr/local/nginx/conf/nginx.conf
```

Search for the line that says:

```
upstream epipros {
  server epipro03.dipr.partners.org:443;
  server epipro04.dipr.partners.org:443;
  # Add new CentOS VMs here
}
```

Add the following line after the last `server` and before the closing `}`:

```
  server epiproXX.dipr.partners.org:443;
```

Restart nginx on slice

```
sudo service nginx restart
```

### 456 Update to Latest Stable version of Slice

On **epiproXX**

```
cd /usr/local/production/slice
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile RAILS_ENV=production; touch tmp/restart.txt
```

That's all!
