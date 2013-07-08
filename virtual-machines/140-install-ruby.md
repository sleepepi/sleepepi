## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.0.0-p247
```

Activate Ruby 2.0.0-p247

```
rvm 2.0.0-p247
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.0.0-p247
```

### 142 Update Ruby Gems

```
gem update --system
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)
