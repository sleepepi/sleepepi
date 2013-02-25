## 140 Install Ruby

Prerequisite: LibYAML may need to be installed, see [Pitfall 960](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/900-pitfalls.md#960-ruby-missing-psych-libyaml)

```console
rvm pkg install libyaml
```

### 141 Install Ruby using RVM

```console
rvm install 2.0.0-p0 --with-libyaml-dir=/usr/local/rvm/usr
```

Activate Ruby 2.0.0-p0

```console
rvm 2.0.0-p0
```

Verify Ruby version

```console
ruby -v

ruby 2.0.0p0 (2013-02-24 revision 39474) [x86_64-linux]
```

Set default Ruby

```console
rvm alias create default ruby-2.0.0-p0
```

### 142 Update Ruby Gems

```console
gem update --system
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.rdoc)
