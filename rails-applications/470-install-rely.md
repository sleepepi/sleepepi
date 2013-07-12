## 470 Install Rely

### 471 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)
### 472 Downloading source from Git

```console
cd /usr/local/production
git clone git://github.com/pmanko/rely.git
```

NOTE: If you get `fatal: could not create work tree dir 'rely'.: Permission denied` that means you forgot to run:

```console
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 473 Initialize database and files

```console
cd /usr/local/production/rely
```

NOTE: If you get `Do you wish to trust this .rvmrc file? (/usr/local/production/rely/.rvmrc)` then type `yes`

```console
bundle install
```

NOTE: If pg fails to compile, see [PostGreSQL Installation Guide](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

```console
ruby lib/initial_setup.rb

  Database User:      rely
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      pgsql.dipr.partners.org

  SMTP Address:       rics.bwh.harvard.edu
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/rely

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

mkdir tmp

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro01* since they are not in version control and contain pseudo-randomly generated strings

```
`-- /usr/local/production/rely/config/initializers/
    |-- devise.rb
    |-- omniauth.rb
    `-- secret_token.rb
```

```console
scp username@epipro01.dipr.partners.org:/usr/local/production/rely/config/initializers/devise.rb /usr/local/production/rely/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/rely/config/initializers/omniauth.rb /usr/local/production/rely/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/rely/config/initializers/secret_token.rb /usr/local/production/rely/config/initializers/secret_token.rb
```

#### Setup Shared RFA folder for uploads

```console
cd /usr/local/production/rely
mkdir uploads
```

Edit `sudo vi /etc/fstab`

```
//rfa01.research.partners.org/bwh-sleepepi/projects/informatics/rely/uploads /usr/local/production/rely/uploads cifs noexec      0 0
```

Remount Directory

```console
sudo umount -a
sudo mount -a
```

Note: If you can't mount you may need to install `cifs-utils`, see [Pitfall 970](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/900-pitfalls.md#970-fstab-file-mount-not-working)

This loads the RFA space `/projects/informatics/rely/uploads`

### 474 Update Nginx Configuration

#### Create symbolic link

```console
sudo ln -s /usr/local/production/rely/public /var/www/html/rely
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```
passenger_base_uri /rely;
```

Restart Nginx

```console
sudo service nginx restart
```

### 475 Update Apache Proxy Balancer on sleepepi

On **sleepepi**

Login in to sleepepi:

```console
ssh username@sleepepi.dipr.partners.org
```

Edit proxy configuration file

```console
sudo vi /etc/httpd/conf.d/proxy.conf
```

Search for the line that says:

```
<Proxy balancer://rely>
  BalancerMember https://epipro01.dipr.partners.org/rely
  BalancerMember https://epipro02.dipr.partners.org/rely
  # ...Add new CentOS VMs here
</Proxy>
```

Add the following line after the last `BalancerMember` and before the closing `</Proxy>` tag:

```
BalancerMember https://epiproXX.dipr.partners.org/rely
```

Restart Apache on sleepepi

```console
sudo service httpd restart
```

### 476 Update to Latest Stable version of Rely

On **epiproXX**

```console
cd /usr/local/production/rely
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile RAILS_ENV=production; touch tmp/restart.txt
```

That's all!

