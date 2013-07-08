## 420 Install Task Tracker

### 421 Prerequisites

[Production VM Server Setup](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/100-technology-and-application-routes.md)

### 422 Downloading source from Git

```console
cd /usr/local/production
git clone git://github.com/remomueller/tasktracker.git
```

NOTE: If you get `fatal: could not create work tree dir 'tasktracker'.: Permission denied` that means you forgot to run:

```console
sudo chgrp rvm /usr/local/production
sudo chmod 775 /usr/local/production
```

### 423 Initialize database and files

```console
cd /usr/local/production/tasktracker
```

NOTE: If you get `Do you wish to trust this .rvmrc file? (/usr/local/production/tasktracker/.rvmrc)` then type `yes`

```console
bundle install
```

NOTE: If mysql2 fails to compile, you forgot the step `sudo yum install mysql mysql-devel`

```console
ruby lib/initial_setup.rb

  Database User:      notes
  Database Password:  <not in documentation>
  Database Socket:    <hit enter>
  Database Host:      mysql.dipr.partners.org

  SMTP Address:       rics.bwh.harvard.edu
  SMTP Port:          <hit enter>
  SMTP Domain:        <hit enter>
  SMTP User Name:     sleepepi@rics.bwh.harvard.edu
  SMTP Password:      <not in documentation>

  Default App Name:   <hit enter>
  Site URL:           https://sleepepi.partners.org/tasktracker

bundle exec rake db:migrate RAILS_ENV=production

bundle exec rake assets:precompile

mkdir tmp

touch tmp/restart.txt
```

NOTE: The contents of the following files will need to be copied from *epipro01* since they are not in version control and contain pseudo-randomly generated strings

```
  `-- /usr/local/production/tasktracker/config/initializers/
      |-- devise.rb
      |-- omniauth.rb
      `-- secret_token.rb
```

```console
scp username@epipro01.dipr.partners.org:/usr/local/production/tasktracker/config/initializers/devise.rb /usr/local/production/tasktracker/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/tasktracker/config/initializers/omniauth.rb /usr/local/production/tasktracker/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/tasktracker/config/initializers/secret_token.rb /usr/local/production/tasktracker/config/initializers/secret_token.rb
```

### 424 Update Nginx Configuration

#### Create symbolic link

```console
sudo ln -s /usr/local/production/tasktracker/public /var/www/html/tasktracker
```

#### Update configuration file

Edit `sudo vi /usr/local/nginx/conf/nginx.conf`

Insert the following in below the line that says `passenger_enabled on;`

```console
passenger_base_uri /tasktracker;
```

Restart Nginx

```console
sudo service nginx restart
```

### 425 Update Apache Proxy Balancer on sleepepi

On **sleepepi**

Login in to sleepepi:

```console
ssh username@sleepepi.dipr.partners.org
```

Edit /etc/httpd/conf.d/proxy.conf

Search for the line that says:

```
<Proxy balancer://tasktracker>
  BalancerMember https://epipro01.dipr.partners.org/tasktracker
  BalancerMember https://epipro02.dipr.partners.org/tasktracker
  # ...Add new CentOS VMs here
</Proxy>
```

Add the following line after the last `BalancerMember` and before the closing `</Proxy>` tag:

```
BalancerMember https://epiproXX.dipr.partners.org/tasktracker
```

Restart Apache on sleepepi

```console
sudo service httpd restart
```

### 426 Update to Latest Stable version of Task Tracker

On **epiproXX**

```console
cd /usr/local/production/tasktracker
git pull; bundle update; bundle exec rake db:migrate RAILS_ENV=production; bundle exec rake assets:precompile; touch tmp/restart.txt
```

That's all!
