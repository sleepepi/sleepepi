## 120 Install Git

Git is required for checking out projects from version control.

```
sudo yum -y install zlib-devel openssl-devel cpio expat-devel gettext-devel perl-devel curl-devel
```

Install from source

```
cd ~/code/source
curl https://git-core.googlecode.com/files/git-1.8.1.1.tar.gz | tar xvz
cd git-*
./configure
make
sudo make install
```

**Important! Logout and login again to reload bash shell!**

Verify Git version

```
git --version

git version 1.8.1.1
```

### Next Step

[130 - Install Ruby Version Manager](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/130-install-rvm.md)
