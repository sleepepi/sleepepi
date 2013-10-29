## 145 Install Oracle Instant Client (Optional)
**NOTE:** *This installation is only necessary if an application hosted by the VM requires a connection to an Oracle database.*

### Oracle Instant Client

1. Download Instant Client Basic, Instant Client SDK, and Instant Client SQL*Plus packages from [Oracle](http://www.oracle.com/technetwork/database/features/instant-client/index-100365.html). Linux x86-64 downloads can be found [here](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html).

**NOTE:** *Oracle downloads require a login and cannot be easily obtained on the VM. Downloading to a local machine and then transfering to the VM might be the best option.*

2. Copy rpm files to VM.

```
scp oracle-instantclient12.1-basic-12.1.0.1.0-1.x86_64.rpm user@vm-host:~/code/source
scp oracle-instantclient12.1-devel-12.1.0.1.0-1.x86_64.rpm user@vm-host:~/code/source
scp oracle-instantclient12.1-sqlplus-12.1.0.1.0-1.x86_64.rpm user@vm-host:~/code/source
```

3. Install the packages.
    
```
cd ~/code/source
sudo rpm -i oracle-instantclient12.1-basic-12.1.0.1.0-1.x86_64.rpm 
sudo rpm -i oracle-instantclient12.1-devel-12.1.0.1.0-1.x86_64.rpm
sudo rpm -i oracle-instantclient12.1-sqlplus-12.1.0.1.0-1.x86_64.rpm
```

4. Set required environmental variables.

  a. Create new profile.d file.

  ```
  sudo vim /etc/profile.d/oracle.sh
  ```

  b. Add the following contents to the file:
  
  ```      
  export ORACLE_VERSION="12.1"
  export ORACLE_HOME="/usr/lib/oracle/$ORACLE_VERSION/client64"
  export PATH=$PATH:"$ORACLE_HOME/bin"
  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:"$ORACLE_HOME/lib"
  export NLS_LANG="AMERICAN_AMERICA.WE8MSWIN1252"
  ```

  **NOTE:** *If you do not know your database's NLS_LANG configuration, run:*
  
      `SELECT * FROM V$NLS_PARAMETERS;` 

  *The NLS_LANG value is composed of*
      `[NLS_LANGUAGE]_[NLS_TERRITORY].NLS_CHARACTERSET` 
  *which can be found in the output of the sql statement.* 

5. Restart session to load Environmental Variables.

6. Test the installation.

```
sqlplus db_user/password@host:port/service
```

### ruby-oci8 Gem

1. Install the gem.

```
gem install ruby-oci8
```

2. Test the installation.

```
ruby -r oci8 -e "OCI8.new('user', 'password', '//host:port/service').exec('select * from dual') do |r| puts r.join(','); end"
```

You should get `X` as the output.

### Supporting Information
1. http://ruby-oci8.rubyforge.org/en/file.install-instant-client.html

### Next Step

[150 - Install Rails](https://github.com/sleepepi/sleepepi/tree/master/virtual-machines/150-install-rails.md)
