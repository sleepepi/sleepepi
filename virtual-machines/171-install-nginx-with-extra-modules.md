## 171 Install Nginx with Extra Modules

This document describes how to install nginx with extra modules in case the simple approach outlined in [170 - Install Nginx](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/170-install-nginx.md) is not sufficient.

Specifically, `headers-more-nginx-module` will be installed in order to remove server and x-powered-by headers for better security using `more_clear_headers`.

### Make sure development headers are installed to be able to compile nginx

```
sudo yum -y install curl-devel
sudo yum -y install wget
# Optional in case PCRE fails to download or if you get "The PCRE checksum could not be verified" during following passenger installation.
sudo yum -y install pcre-devel
```

\* Note: If compiling nginx fails, make sure to rerun the full yum install mentioned in [130 - Install Ruby Version Manager](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/130-install-rvm.md)

### Download nginx source code

```
cd /tmp
mkdir nginxplus
cd /tmp/nginxplus
wget https://www.openssl.org/source/openssl-1.0.2l.tar.gz
tar xzvf openssl-1.0.2l.tar.gz
rm openssl-1.0.2l.tar.gz
curl -L http://www.nginx.org/download/nginx-1.12.1.tar.gz | tar xvz
curl -L https://github.com/agentzh/headers-more-nginx-module/archive/v0.32.tar.gz --insecure | tar xvz
```

### Start the Passenger Installer

```
rvmsudo passenger-install-nginx-module --auto --prefix=/usr/local/nginx --nginx-source-dir=/tmp/nginxplus/nginx-1.12.1 --extra-configure-flags="--with-openssl=/tmp/nginxplus/openssl-1.0.2l --add-module=/tmp/nginxplus/headers-more-nginx-module-0.32" --languages ruby
```

or manually

```
rvmsudo passenger-install-nginx-module
```

Type `<enter>`

```
Which languages are you interested in?

Use <space> to select.

 ‣ ⬢  Ruby
   ⬡  Python
   ⬡  Node.js
   ⬡  Meteor
```

Deselect Python and Node.js using the `<space>` then type `<enter>`

```console
2. No: I want to customize my Nginx installation. (for advanced users)

Enter your choice (1 or 2) or press Ctrl-C to abort:
```

Type `2`

```console
Where is your Nginx source code located?

Please specify the directory:
```

Type `/tmp/nginxplus/nginx-1.12.1`

```console
Where do you want to install Nginx to?

Please specify a prefix directory [/opt/nginx]:
```

Type `/usr/local/nginx`

```console
Extra Nginx configure options

If you want to pass extra arguments to the Nginx 'configure' script, then
please specify them. If not, then specify nothing and press Enter.

If you specify nothing then the 'configure' script will be run as follows:

  sh ./configure ...

Extra arguments to pass to configure script:
```

Type
```
--with-openssl=/tmp/nginxplus/openssl-1.0.2l --add-module=/tmp/nginxplus/headers-more-nginx-module-0.32
```

```console
Confirm configure flags

The Nginx configure script will be run as follows:

  sh ./configure ...

Is this what you want? (yes/no) [default=yes]:
```

Type `<enter>`


### Next Step

[173 - Nginx Configuration](https://github.com/sleepepi/sleepepi/blob/master/virtual-machines/173-nginx-configuration.md)
