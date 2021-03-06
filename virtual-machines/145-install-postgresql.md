## 145a Install PostgreSQL - For CentOS 7

These instructions are for CentOS 7+. For prior versions, scroll down

```
sudo yum -y install postgresql-libs postgresql-devel
```

### Verify PostgreSQL Version

```
psql --version
```

should return

```console
psql (PostgreSQL) 9.2.13
```

## 145b Install PostgreSQL - For CentOS 5/6
These instructions are based on [PostgreSQL YUM Installation](http://wiki.postgresql.org/wiki/YUM_Installation)

### Configure your YUM repository

Locate and edit your distributions .repo file:

```
sudo vi /etc/yum.repos.d/CentOS-Base.repo
```

append this line to BOTH the `[base]` and `[updates]` sections:

```
exclude=postgresql*
```

### Download and Install PGDG RPM file

```
cd ~/code/source/
```

Determine your CentOS version and download appropriate file version.

```
cat /etc/redhat-release # To find out CentOS version
```

For CentOS 5:

```
wget http://yum.pgrpms.org/9.1/redhat/rhel-5-x86_64/pgdg-centos91-9.1-4.noarch.rpm
```

For CentOS 6:

```
wget http://yum.pgrpms.org/9.1/redhat/rhel-6-x86_64/pgdg-centos91-9.1-4.noarch.rpm
```

### Install RPM Distribution:

```
sudo rpm -ivh pgdg-centos91-9.1-4.noarch.rpm
```

### Install PostgreSQL

```
sudo yum install postgresql91-devel
```

### Add PostgreSQL to path

```
vi ~/.bash_profile
```

Add before the `export PATH`

```
PATH=$PATH:/usr/pgsql-9.1/bin/
```

NOTE: Remember to reload your shell to have changes to PATH take effect

### Verify PostgreSQL Version

```
psql --version
```

should return

```console
psql (PostgreSQL) 9.1.9
```

### Next Step

[146 - Install Oracle Instant Client](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/146-install-oracle-instant-client.md)
