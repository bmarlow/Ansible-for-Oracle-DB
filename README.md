# Ansible-for-Oracle-DB
This repo gives the tools for deploying an Oracle Express database on Linux for the express purposes of using ansible to manage said database

The user creation below is so that the oracle_user module can be used for changing passwords



## Directions
### Download and pre-install tools
    curl -o oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm https://yum.oracle.com/repo/OracleLinux/OL7/latest/x86_64/getPackage/oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm

    yum -y localinstall oracle-database-preinstall-18c-1.0-1.el7.x86_64.rpm

### Install Oracle database (must be downloaded prior from oracle)
    yum -y localinstall oracle-database-xe-18c-1.0-1.x86_64.rpm

### Unzip and install Instant client (must be downloaded prior from oracle)
    unzip instantclient-basic-linux.x64-18.3.0.0.0dbru.zip

### Update instant client conf
    echo /opt/oracle/instantclient_18_3 > /etc/ld.so.conf.d/oracle-instantclient.conf
    ldconfig

### Get pip installer
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

### Run pip installer
    python get-pip.py

### Install cx_Oracle python module for connecting to DBs
    pip install cx_Oracle

### Run confugiration
    /etc/init.d/oracle-xe-18c configure

### Make sure enviornmental variables are set correctly (add to .bash_profile)

    PATH=$PATH:$HOME/bin
    PATH=$ORACLE_HOME/bin:$PATH
    export PATH

    ORACLE_HOME=/opt/oracle/product/18c/dbhomeXE
    export ORACLE_HOME

    ORACLE_SID=XE
    export ORACLE_SID

    ORAENV_ASK=NO
    export ORAENV_ASK

    LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib:/usr/local/lib
    export LD_LIBRARY_PATH

### Connect to database
    sqlplus system/password@localhost as dba

### Go to edit mode
    alter session set "_ORACLE_SCRIPT"=true;

### Create a user
    create user mytestuser identified by changeme;
    GRANT CONNECT, RESOURCE, DBA TO mytestuser;

### Log on as user
    sqlplus mytestuser/changeme@localhost

