## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.1.3
```

Activate Ruby 2.1.3

```
rvm 2.1.3
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.1.3p242 (2014-09-19 revision 47630) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.1.3
```

### 142 Update Ruby Gems

```
gem update --system
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

or skip database (PostgreSQL and Oracle) installations

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
