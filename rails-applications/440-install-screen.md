## 440 Install Screen

### 441 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

### 442 Downloading source from Git

```console
cd /usr/local/production
git clone git://github.com/remomueller/screen.git
```

NOTE: If you get `fatal: could not create work tree dir 'screen'.: Permission denied` that means you forgot to run:

```console
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 443 Initialize database and files

```console
cd /usr/local/production/screen
```

NOTE: If you get `Do you wish to trust this .rvmrc file? (/usr/local/production/screen/.rvmrc)` then type `yes`

```console
bundle install
```

NOTE: If mysql2 fails to compile, you forgot the step `sudo yum install mysql mysql-devel`

```console
ruby lib/initial_setup.rb

  Database User:      screen
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      mysql.dipr.partners.org

  SMTP Address:       rics.bwh.harvard.edu
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/screen

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

mkdir tmp

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro01* since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/screen/config/initializers/
    |-- devise.rb
    |-- omniauth.rb
    `-- secret_token.rb
```

```console
scp username@epipro01.dipr.partners.org:/usr/local/production/screen/config/initializers/devise.rb /usr/local/production/screen/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/screen/config/initializers/omniauth.rb /usr/local/production/screen/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/screen/config/initializers/secret_token.rb /usr/local/production/screen/config/initializers/secret_token.rb
```

### 444 Update Nginx Configuration

#### Create symbolic link

```console
sudo ln -s /usr/local/production/screen/public /var/www/html/screen
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```
passenger_base_uri /screen;
```

Restart Nginx

```console
sudo service nginx restart
```

### 445 Update Apache Proxy Balancer on sleepepi

**Screen is not available through the sleepepi router!**

### 446 Update to Latest Stable version of Screen

On **epiproXX**

```console
cd /usr/local/production/screen
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile; touch tmp/restart.txt
```

That's all!
