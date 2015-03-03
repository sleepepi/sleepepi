## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.2.1
```

Activate Ruby 2.2.1

```
rvm 2.2.1
```

**NOTE** You may need to create a gemset to switch to 2.2.1 if it failed during the install.

```
rvm 2.2.1 --create
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.2.1p85 (2015-02-26 revision 49769) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.2.1
```

### 142 Update Ruby Gems

```
gem update --system
```

for a specific version of gem

```
gem update --system 2.2.2 --no-ri --no-rdoc
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

or skip database (PostgreSQL and Oracle) installations

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
