## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed.

```
rvmsudo rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.4.2
```

Activate Ruby 2.4.2

```
rvm 2.4.2
```

**NOTE** You may need to create a gemset to switch to 2.4.2 if it failed during the install.

```
rvm 2.4.2 --create
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.4.2p198 (2017-09-14 revision 59899) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.4.2
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
