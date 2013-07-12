## 900 Pitfalls

This set of documents will list known pitfalls during the installation process.

### 910 Shared Rails Secret Tokens and Keys

Similar rails applications that are load balanced across multiple servers require the following files to be identical:

```
<rails_root>/config/initializers/devise.rb

<rails_root>/config/initializers/secret_token.rb

<rails_root>/config/initializers/omniauth.rb
```

If these files are not identical, users will have issues with their cookies being reset during multiple requests to their servers.

You can do a secure copy to copy files from **epipro01.dipr.partners.org**, make sure you change *rails_app* to the correct rails application!

```
scp username@epipro01.dipr.partners.org:/usr/local/production/rails_app/config/initializers/devise.rb /usr/local/production/rails_app/config/initializers/devise.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/rails_app/config/initializers/omniauth.rb /usr/local/production/rails_app/config/initializers/omniauth.rb
scp username@epipro01.dipr.partners.org:/usr/local/production/rails_app/config/initializers/secret_token.rb /usr/local/production/rails_app/config/initializers/secret_token.rb
```

### 920 Problematic Rails Server

Currently if a load-balanced server runs into memory issues, requests to this server may be slow, but won't fail.

Try reboot on the offending server

```
sudo reboot
```

If you are unable to SSH to the server, then another alternative is to temporarily comment out the load-balancer Apache file on **sleepepi.dipr.partners.org**

`sudo vi /etc/httpd/conf.d/proxy.conf`

```
<Proxy balancer://tasktracker>
#  BalancerMember https://epipro01.dipr.partners.org/tasktracker  # Comment out the offending server
  BalancerMember https://epipro02.dipr.partners.org/tasktracker
</Proxy>
```

`sudo service httpd restart`

Remember to uncomment this line and restart the server on **sleepepi.dipr.partners.org** once the server is back up and running!


### 930 Nginx Will Not Start Automatically

Make sure Apache is not running:

```
sudo chkconfig httpd off
sudo service httpd stop
```

Start Nginx Manually

```
sudo service nginx start
```

Make sure Nginx is set to start automatically on restart

  sudo chkconfig nginx on

### 940 Yum Install Issues

If you get `warning: rpmts_HdrFromFdno: Header V3 RSA/SHA256 Signature, key ID 0608b895: NOKEY` when running, then you need to update your GPG keys:

```
sudo rpm --import https://fedoraproject.org/static/0608B895.txt
sudo rpm --import http://packages.atrpms.net/RPM-GPG-KEY.atrpms
```

After this, running the `sudo yum install` should work correctly

### 950 PostgreSQL Gem Compilation Issues

If you get the following error when compiling the pg gem:

```console
Gem::Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.

/usr/local/rvm/rubies/ruby-2.0.0-p0/bin/ruby extconf.rb
checking for pg_config... yes
Using config values from /usr/bin/pg_config
checking for libpq-fe.h... yes
checking for libpq/libpq-fs.h... yes
checking for pg_config_manual.h... yes
checking for PQconnectdb() in -lpq... yes
checking for PQconnectionUsedPassword()... no
Your PostgreSQL is too old. Either install an older version of this gem or upgrade your database.
```

Then make sure PostgreSQL is installed and the version is 8.3 or later:

`psql --version`

If version is too low, run:

`sudo yum erase postgresql*`

And re-install a more recent PostgreSQL version by following [145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

### 960 Ruby Missing psych (libyaml)

If you get the following when attempting to update gem, or installing new gems:

```
It seems your ruby installation is missing psych (for YAML output). To eliminate this warning, please install libyaml and reinstall your ruby
```

Then make sure you reinstall Ruby using RVM since as follows:

```
rvm remove 2.0.0-p0

rvmsudo rvm pkg install libyaml

rvm install ruby-2.0.0-p0 --with-libyaml-dir=/usr/local/rvm/usr
```

Back to [140 - Install Ruby](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/140-install-ruby.md)

This is due to different versions of CentOS (or other operating systems) having default versions of libyaml and libyaml-devel. For this version of Ruby, libyaml 0.1.4 is required, and yum only installs up through 0.1.2 on CentOS 5, and 0.1.3 on CentOS 6. This is fixed by allowing RVM to manage libyaml and specifying the libyaml when installing Ruby.

If you get the error:

```
sudo: rvm: command not found
```

Then you most likely need to export rvm to the PATH

```
  sudo vi /etc/profile

  # Add the following line

  PATH="/usr/local/bin:/usr/local/sbin:$PATH"

  # Before this existing line

  export PATH # ...
```

### 970 FSTAB file Mount not Working

If you get the following when attempting to `sudo mount -a`:

```
mount: wrong fs type, bad option, bad superblock on
```

Then you need to install cifs-utils

```
  sudo yum install cifs-utils
```
