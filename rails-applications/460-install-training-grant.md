## 460 Install Training Grant

### 461 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

### 462 Downloading source from Git

```console
cd /usr/local/production
git clone git://github.com/remomueller/training_grant.git
```

NOTE: If you get `fatal: could not create work tree dir 'training_grant'.: Permission denied` that means you forgot to run:

```console
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 463 Initialize database and files

```console
cd /usr/local/production/training_grant
```

NOTE: If you get `Do you wish to trust this .rvmrc file? (/usr/local/production/training_grant/.rvmrc)` then type `yes`

```console
bundle install
```

NOTE: If mysql2 fails to compile, you forgot the step `sudo yum install mysql mysql-devel`

```console
ruby lib/initial_setup.rb

  Database User:      training_grant
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      mysql.dipr.partners.org

  SMTP Address:       rics.bwh.harvard.edu
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/training_grant

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

mkdir tmp

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro01* since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/training_grant/config/initializers/
    |-- devise.rb
    |-- omniauth.rb
    `-- secret_token.rb
```

```console
scp username@epipro01.dipr.partners.org:/usr/local/production/training_grant/config/initializers/devise.rb /usr/local/production/training_grant/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/training_grant/config/initializers/omniauth.rb /usr/local/production/training_grant/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/training_grant/config/initializers/secret_token.rb /usr/local/production/training_grant/config/initializers/secret_token.rb
```

#### Setup Shared RFA folder for uploads

```console
cd /usr/local/production/training_grant/public
mkdir uploads
```

Edit `sudo vi /etc/fstab`

```
//rfa01.research.partners.org/bwh-sleepepi/projects/informatics/training_grant/uploads /usr/local/production/training_grant/public/uploads cifs noexec      0 0
```

Remount Directory

```console
sudo umount -a
sudo mount -a
```

This loads the RFA space `/projects/informatics/training_grant/uploads`

### 464 Update Nginx Configuration

#### Create symbolic link

```console
sudo ln -s /usr/local/production/training_grant/public /var/www/html/training_grant
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```
passenger_base_uri /training_grant;
```

Restart Nginx

```console
sudo service nginx restart
```

### 465 Update Apache Proxy Balancer on sleepepi

On **sleepepi**

Login in to sleepepi:

```console
ssh username@sleepepi.dipr.partners.org
```

Edit /etc/httpd/conf.d/proxy.conf

Search for the line that says:

```
<Proxy balancer://training_grant>
  BalancerMember https://epipro01.dipr.partners.org/training_grant
  BalancerMember https://epipro02.dipr.partners.org/training_grant
  # ...Add new CentOS VMs here
</Proxy>
```

Add the following line after the last `BalancerMember` and before the closing `</Proxy>` tag:

```
BalancerMember https://epiproXX.dipr.partners.org/training_grant
```

Restart Apache on sleepepi

```console
sudo service httpd restart
```

### 466 Update to Latest Stable version of Training Grant

On **epiproXX**

```console
cd /usr/local/production/training_grant
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile RAILS_ENV=production; touch tmp/restart.txt
```

That's all!
