## 180 Install Node.js and CoffeeScript JavaScript compiler

Tools required by server to compile CoffeeScript files into JavaScript

The following requires that gcc 4.9.4 or higher is installled:

```
sudo yum -y install centos-release-scl
sudo yum -y install devtoolset-4-toolchain
```

`vi ~/.bashrc`
```
# Enable gcc 5.3.1
source /opt/rh/devtoolset-4/enable
```

Restart shell

```
gcc --version
gcc (GCC) 5.3.1 20160406 (Red Hat 5.3.1-6)
```

### 181 Node.js and Node Package Manager

Download and compile node.js and Node Package Manager

```
cd ~/code/source
curl -L https://nodejs.org/dist/v8.9.4/node-v8.9.4.tar.gz | tar xvz
cd node-v8.9.4/
./configure
make
sudo make install
```

Verify Node.js installed by typing `which node` which should return:

```console
/usr/local/bin/node
```

Verify Node.js version by typing `node -v` which should return:

```console
v8.9.4
```

Verify npm installed by typing `which npm` which should return:

```console
/usr/local/bin/npm
```

Verify npm version by typing `npm -v` which should return:

```console
5.6.0
```

Make symbolic links for node and npm

```
sudo ln -s /usr/local/bin/node /usr/bin/node
sudo ln -s /usr/local/bin/npm /usr/bin/npm
```

### 182 CoffeeScript

Download and compile CoffeeScript

```
sudo npm install -g coffee-script
```

Verify CoffeeScript installed by typing `which coffee` which should return:

```console
/usr/local/bin/coffee
```

Make symbolic links for coffee

```
sudo ln -s /usr/local/bin/coffee /usr/bin/coffee
```

Verify CoffeeScript version by typing `coffee -v` which should return:

```console
CoffeeScript version 1.12.7
```

### Next Step

[190 - Install Rails Applications](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/190-install-rails-applications.md)
