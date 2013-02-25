## 145 Install PostgreSQL
These instructions are based on [PostgreSQL YUM Installation](http://wiki.postgresql.org/wiki/YUM_Installation)

### Configure your YUM repository

Locate and edit your distributions .repo file:

```console
sudo vi /etc/yum.repos.d/CentOS-Base.repo
```

append this line to BOTH the [base] and [updates] sections:

```
exclude=postgresql*
```

### Download and Install PGDG RPM file

```console
cd ~/code/source/
```

Determine your CentOS version and download appropriate file version.

```console
cat /etc/redhat-release # To find out CentOS version
```

For CentOS 5:

```console
wget http://yum.pgrpms.org/9.1/redhat/rhel-5-x86_64/pgdg-centos91-9.1-4.noarch.rpm
```

For CentOS 6:

```console
wget http://yum.pgrpms.org/9.1/redhat/rhel-6-x86_64/pgdg-centos91-9.1-4.noarch.rpm
```

### Install RPM Distribution:

```console
sudo rpm -ivh pgdg-centos91-9.1-4.noarch.rpm
```

### Install PostgreSQL

```console
sudo yum install postgresql91-devel
```

### Add PostgreSQL to path

```console
vi ~/.bash_profile
```

Add before the `export PATH`

```console
PATH=$PATH:/usr/pgsql-9.1/bin/
```

NOTE: Remember to reload your shell to have changes to PATH take effect

### Verify PostgreSQL Version

```console
psql --version
```

should return

```console
psql (PostgreSQL) 9.1.7
```

### Next Step

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
