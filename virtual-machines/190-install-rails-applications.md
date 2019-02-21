## 190 Install Rails Applications


### Initialize Production Directory and Permissions

```
cd /usr/local
sudo mkdir production
sudo chgrp rvm production
sudo chmod 775 production
```

### Installing MySQL Library to allow compilation of mysql2 ruby gem

```
sudo yum install -y mysql mysql-devel
```

### Installing libraries to allow compilation of nokogiri gem

```
sudo yum install -y libxml libxml-devel libxslt libxslt-devel
```

### Installing Automount and CIFS to mount folders from the RFA

```
sudo yum install -y samba-client samba-common cifs-utils autofs
```

Add to bottom of `/etc/auto.master`
Use one of the following depending on which application is installed.
```
/- /etc/auto.altamira
/- /etc/auto.sleepdata
/- /etc/auto.patstrial
```

Create and add to `/etc/auto.secret`, the username and password are for the RFA service account.
```
username=XXXX
password=XXXX
```

Create and add to `/etc/auto.sleepdata`
```
/usr/local/production/www.sleepdata.org/carrierwave -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfa01.research.partners.org/bwh-sleepepi-nsrr/www.sleepdata.org/carrierwave
```

Create and add to `/etc/auto.patstrial`
```
/usr/local/production/patstrial.org/carrierwave -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfa01.research.partners.org/bwh-sleepepi-web/production/patstrial.org/carrierwave
```

Create and add to `/etc/auto.altamira`
```
/usr/local/production/altamira/datasets -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfa01.research.partners.org/bwh-sleepepi-nsrr/www.sleepdata.org/carrierwave/datasets
```


# MyApnea

Edit `/etc/auto.master`

```
+auto.master

/- /etc/auto.myapnea
```

Create and add to `/etc/auto.myapnea`
```
/usr/local/production/myapnea.org/carrierwave -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-web/production/myapnea.org/carrierwave
```


# SleepINNOVATE

Edit `/etc/auto.master`

```
+auto.master

/- /etc/auto.sleepinnovate
/- /etc/auto.admin
/- /etc/auto.brains
```

Create and add to `/etc/auto.sleepinnovate`
```
/usr/local/production/sleepinnovate.org/carrierwave -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-web/production/sleepinnovate.org/carrierwave
```

Create and add to `/etc/auto.admin`
```
/usr/local/production/sleepinnovate.org/admin -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-r35/Data/sleepinnovate.org
```

Create and add to `/etc/auto.brains`
```
/usr/local/production/sleepinnovate.org/brains -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-r35/Data/TMB
```


# Slice

Edit `/etc/auto.master`

```
+auto.master

/- /etc/auto.slice
/- /etc/auto.patstrial
```


Create and add to `/etc/auto.slice`
```
/usr/local/production/tryslice.io/carrierwave -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-web/production/slice/carrierwave
```

Create and add to `/etc/auto.patstrial`
```
/usr/local/production/tryslice.io/pats -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-web/production/patstrial.org/carrierwave
```

# Train Tracks

Edit `/etc/auto.master`

```
+auto.master

/- /etc/auto.traintracks
```

Create and add to `/etc/auto.traintracks`
```
/usr/local/production/traintracks/public/uploads -fstype=cifs,uid=3051303,gid=100001,file_mode=0775,dir_mode=0775,credentials=/etc/auto.secret ://rfawin.partners.org/bwh-sleepepi-web/production/traintracks/uploads
```


# For all applications

After adding the folders, restart Automount

```
sudo service autofs restart
```

You can also assure autofs loads after a reboot by doing:

```
sudo chkconfig autofs on
```

### Install individual Ruby on Rails Applications

* [Sleep Portal](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/410-install-sleep-portal.md)
* [Task Tracker](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/420-install-task-tracker.md)
* [CHAT Publications](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/430-install-chat-publications.md)
* [Screen](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/440-install-screen.md)
* [Slice](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/450-install-slice.md)
* [Training Grant](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/460-install-training-grant.md)
* [Rely](https://github.com/sleepepi/sleepepi/tree/master/rails-applications/470-install-rely.md)
