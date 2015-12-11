## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvmsudo rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.3.0-preview2
```

Activate Ruby 2.3.0-preview2

```
rvm 2.3.0-preview2
```

**NOTE** You may need to create a gemset to switch to 2.3.0-preview2 if it failed during the install.

```
rvm 2.3.0-preview2 --create
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.3.0preview2 (2015-12-11 trunk 53028) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.3.0-preview2
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
