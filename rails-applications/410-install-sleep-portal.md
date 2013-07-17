## 410 Install Sleep Portal

### 411 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

### 412 Downloading source from Git

```
cd /usr/local/production
git clone https://github.com/sleepepi/sleepportal.git
```

NOTE: If you get `fatal: could not create work tree dir 'sleepportal'.: Permission denied` that means you forgot to run:

```
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 413 Initialize database and files

```
cd /usr/local/production/sleepportal
```

```
bundle install
```

NOTE: If mysql2 fails to compile, you forgot the step `sudo yum install mysql mysql-devel`

```
ruby lib/initial_setup.rb

  Database User:      sleepportal
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      pgsql.dipr.partners.org

  SMTP Address:       <not in documentation>
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/sleepportal

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile RAILS_ENV=production

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from **epipro01** since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/sleepportal/config/initializers/
    |-- devise.rb
    |-- omniauth.rb
    `-- secret_token.rb
```

```
scp username@epipro01.dipr.partners.org:/usr/local/production/sleepportal/config/initializers/devise.rb /usr/local/production/sleepportal/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/sleepportal/config/initializers/omniauth.rb /usr/local/production/sleepportal/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/sleepportal/config/initializers/secret_token.rb /usr/local/production/sleepportal/config/initializers/secret_token.rb
```

#### Setup Shared RFA folder for uploads

```
cd /usr/local/production/sleepportal/public
mkdir forms
```

Edit `sudo vi /etc/fstab`

```
//rfa01.research.partners.org/bwh-sleepepi/projects/informatics/sleepportal/forms /usr/local/production/sleepportal/public/forms cifs noexec      0 0
```

Remount Directory

```
sudo umount -a
sudo mount -a
```

This loads the RFA space `/projects/informatics/sleepportal/forms`

### 414 Update Nginx Configuration

#### Create symbolic link

```
sudo ln -s /usr/local/production/sleepportal/public /var/www/html/sleepportal
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```
passenger_base_uri /sleepportal;
```

Restart Nginx

```
sudo service nginx restart
```

### 415 Update Apache Proxy Balancer on sleepepi

On **sleepepi**

Login in to sleepepi:

```
ssh username@sleepepi.dipr.partners.org
```

Edit `sudo vi /etc/httpd/conf.d/proxy.conf`

Search for the line that says:

```
<Proxy balancer://sleepportal>
  BalancerMember https://epipro01.dipr.partners.org/sleepportal
  BalancerMember https://epipro02.dipr.partners.org/sleepportal
  # ...Add new CentOS VMs here
</Proxy>
```

Add the following line after the last `BalancerMember` and before the closing `</Proxy>` tag:

```
BalancerMember https://epiproXX.dipr.partners.org/sleepportal
```

Restart Apache on sleepepi

```
sudo service httpd restart
```

### 416 Update to Latest Stable version of Sleep Portal

On **epiproXX**

```
cd /usr/local/production/sleepportal
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile RAILS_ENV=production; touch tmp/restart.txt
```

That's all!
