## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed

```
rvm requirements
```

### 141 Install Ruby using RVM

```
rvm install 2.1.2
```

Activate Ruby 2.1.2

```
rvm 2.1.2
```

Verify Ruby version

```
ruby -v
```

```console
ruby 2.1.2p95 (2014-05-08 revision 45877) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-2.1.2
```

### 142 Update Ruby Gems

```
gem update --system
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)
