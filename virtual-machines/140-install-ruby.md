## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvmsudo rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.3.1
```

Activate Ruby 2.3.1

```
rvm 2.3.1
```

**NOTE** You may need to create a gemset to switch to 2.3.1 if it failed during the install.

```
rvm 2.3.1 --create
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.3.1
```

### 142 Update Ruby Gems

```
gem update --system --no-document
```

for a specific version of gem

```
gem update --system 2.2.2 --no-document
```

or

```
gem update --system 2.6.3 --no-document
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

or skip database (PostgreSQL and Oracle) installations

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
