## 140 Install Ruby

Prerequisite: Install may require certain requirements to be installed.

```
rvmsudo rvm requirements
```

[Install GCC 4.9.2 or higher](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/910-gcc.md)

### 141 Install Ruby using RVM

```
rvm install 3.1.2
```

Activate Ruby 3.1.2

```
rvm 3.1.2
```

**NOTE** You may need to create a gemset to switch to 3.1.2 if it failed during the install.

```
rvm 3.1.2 --create
```

Verify Ruby version

```
ruby -v
```

```console
ruby 3.1.2p20 (2022-04-12 revision 4491bb740a) [x86_64-linux]
```

Set default Ruby

```
rvm alias create default ruby-3.1.2
```

Remove default alias (in case default alias interferes with system tasks that require the default system Ruby)

```
rvm alias delete default
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
gem update --system 3.0.1 --no-document
```

### Next Step

[145 - Install PostgreSQL](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/145-install-postgresql.md)

or skip database (PostgreSQL and Oracle) installations

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
