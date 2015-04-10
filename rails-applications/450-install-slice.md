## 450 Install Slice

### 451 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

[LaTeX Installation](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/800-extra-dependencies.md)

### 452 Downloading source from Git

```
cd /usr/local/production
git clone git://github.com/remomueller/slice.git
```

NOTE: If you get `fatal: could not create work tree dir 'slice'.: Permission denied` that means you forgot to run:

```
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 453 Initialize database and files

```
cd /usr/local/production/slice
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

  SMTP Address:       rics.bwh.harvard.edu
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/slice

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

mkdir tmp

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro01* since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/slice/config/initializers/
    |-- devise.rb
    |-- omniauth.rb
    `-- secret_token.rb
```

```
scp username@epipro01.dipr.partners.org:/usr/local/production/slice/config/initializers/devise.rb /usr/local/production/slice/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/slice/config/initializers/omniauth.rb /usr/local/production/slice/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/slice/config/initializers/secret_token.rb /usr/local/production/slice/config/initializers/secret_token.rb
```

#### Setup Shared RFA folder for uploads

Follow the [Automount Installation Instructions](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/190-install-rails-applications.md#installing-automount-and-cifs-to-mount-folders-from-the-rfa) that are provided if you haven't installed the required automount libraries.

Slice requires the following in `auto.master`:

```
/- /etc/auto.slice
```

Slice also requires the additional file `auto.slice`:

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

Restart Nginx

```
sudo service nginx restart
```

### 455 Update Apache Proxy Balancer on sleepepi

On **sleepepi**

Login in to sleepepi:

```
ssh username@sleepepi.dipr.partners.org
```

Edit proxy configuration file

```
sudo vi /etc/httpd/conf.d/proxy.conf
```

Search for the line that says:

```
<Proxy balancer://slice>
  BalancerMember https://epipro01.dipr.partners.org/slice
  BalancerMember https://epipro02.dipr.partners.org/slice
  # ...Add new CentOS VMs here
</Proxy>
```

Add the following line after the last `BalancerMember` and before the closing `</Proxy>` tag:

```
BalancerMember https://epiproXX.dipr.partners.org/slice
```

Restart Apache on sleepepi

```
sudo service httpd restart
```

### 456 Update to Latest Stable version of Slice

On **epiproXX**

```
cd /usr/local/production/slice
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile RAILS_ENV=production; touch tmp/restart.txt
```

That's all!
