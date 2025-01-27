# Upgrade to Percona Server for MongoDB Pro

Are you a Percona Customer already and are you ready to enjoy all the [benefits of Percona Server for MongoDB Pro](../psmdb-pro.md)? 

This document provides instructions how you can upgrade from Percona Server for MongoDB to Percona Server for MongoDB Pro .

--8<-- "token.md"

## Procedure {.power-number}

1. Stop the `mongod` service

    ```{.bash data-prompt="$"}
    $ sudo systemctl stop mongod
    ```

2. Configure the repository

    === ":material-debian: On Debian and Ubuntu"

        1. Create the `/etc/apt/sources.list.d/psmdb-pro.list` configuration file with the following contents

            ```ini title="/etc/apt/sources.list.d/psmdb-pro.list"
            deb http://repo.percona.com/private/[TOKENID]-[TOKEN]/psmdb-70-pro/apt/ OPERATING_SYSTEM main
            ```

        2. Update the local cache

            ```{.bash .data-prompt="$"}
            $ sudo apt update
            ```

    === ":material-redhat: On RHEL and derivatives"

        Create the `/etc/yum.repos.d/psmdb-pro.repo` configuration file with the following contents

        ```ini title="/etc/yum.repos.d/psmdb-pro.repo"
        [psmdb-7.0-pro]
        name=PSMDB_7.0_PRO
        baseurl=http://repo.percona.com/private/[TOKENID]-[TOKEN]/psmdb-70-pro/yum/main/$releasever/RPMS/x86_64
        enabled=1
        gpgkey = https://repo.percona.com/yum/PERCONA-PACKAGING-KEY
        ```

3. Install Percona Server for MongoDB Pro packages

    === ":material-debian: On Debian and Ubuntu"

        ```{.bash .data-prompt="$"}
        $ sudo apt install -y percona-server-mongodb-pro
        ```

    === ":material-redhat: On RHEL 8+ and derivatives"

        ```{.bash .data-prompt="$"}
        $ sudo yum install -y percona-server-mongodb-pro
        ```

    === ":material-redhat:  On RHEL 7 and derivatives"

        1. Back up the `/etc/mongod.conf` configuration file
       
            ```{.bash .data-prompt="$"}
            $ sudo cp /etc/mongod.conf /etc/mongod.conf.bkp
            ```

        2. Remove basic packages of Percona Server for MongoDB 

            ```{.bash .data-prompt="$"}
            $ sudo yum remove percona-server-mongodb*
            ```

        3. Install Percona Server for MongoDB Pro packages

            ```{.bash .data-prompt="$"}
            $ sudo yum install -y percona-server-mongodb-pro
            ```

        4. Restore the configuration file from the backup

            ```{.bash .data-prompt="$"}
            $ sudo cp /etc/mongod.conf.bkp /etc/mongod.conf
            ```

4. Start the server

    ```{.bash .data-prompt="$"}
    $ sudo systemct start mongod
    ```

## Downgrade considerations on RHEL and derivatives

The downgrade to the basic build of Percona Server for MongoDB of version **7.0.4 and higher** is done automatically by [installing the basic build packages](yum.md#install-percona-server-for-mongodb-packages). 

If you wish to downgrade from Percona Server for MongoDB Pro to the basic build of Percona Server for MongoDB version **lower than 7.0.4**, do the following:
{.power-number }

1. Remove the Pro packages

    ```{.bash .data-prompt="$"}
    $ sudo yum remove percona-server-mongodb-pro*
    ```

2. [Install Percona Server for MongoDB basic packages of the desired version](yum.md#install-percona-server-for-mongodb-packages)

        