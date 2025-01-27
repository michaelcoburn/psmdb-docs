# Install Percona Server for MongoDB on Red Hat Enterprise Linux and derivatives

This document describes how to install Percona Server for MongoDB on RPM-based distributions such as Red Hat Enterprise Linux and compatible derivatives. We gather [Telemetry data](../telemetry.md) to understand the use of the software and improve our products.

!!! note

    Percona Server for MongoDB should work on other RPM-based distributions (for example, Amazon Linux AMI and Oracle Linux), but it is tested only on platforms listed on the [Percona Software and Platform Lifecycle](https://www.percona.com/services/policies/percona-software-platform-lifecycle#mongodb) page. 

??? admonition "Package contents"

   | Package                 | Contains                                 |
   | ----------------------- | -----------------------------------------|
   | `percona-server-mongodb`| The `mongosh` shell, import/export tools, other client utilities, server software, default configuration, and `init.d` scripts. |
   | `percona-server-mongodb-server`| The `mongod` server, default configuration files, and `init.d` scripts|
   | `percona-server-mongodb-shell` | The `mongosh` shell |
   | `percona-server-mongodb-mongos`| The `mongos` sharded cluster query router |
   | `percona-server-mongodb-tools` | Mongo tools for high-performance MongoDB fork from Percona|
   | `percona-server-mongodb-dbg`   | Debug symbols for the server  |

## Procedure

Before you start, check the [system requirements](../system-requirements.md).

### Configure Percona repository

Percona provides the [`percona-release`](https://docs.percona.com/percona-software-repositories/index.html) configuration tool that simplifies operating repositories and enables to install and update both Percona Server for MongoDB packages and required dependencies smoothly.    

1. Install **percona-release**:     

    ```{.bash data-prompt="$"}
    $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
    ```
         
    ??? example "Example output"

        ```{.bash .no-copy }
        Retrieving https://repo.percona.com/yum/percona-release-latest.noarch.rpm
        Preparing...                ########################################### [100%]
        1:percona-release        ########################################### [100%]
        ```     

2. Enable the repository: 
        
    ```{.bash data-prompt="$"}
    $ sudo percona-release enable psmdb-70 release
    ```

### Install Percona Server for MongoDB packages

=== ":material-run-fast: Install the latest version"

      To install the latest version of *Percona Server for MongoDB*, use the following command:

      ```{.bash data-prompt="$"}
      $ sudo yum install percona-server-mongodb
      ```

=== ":octicons-number-16: Install a specific version"

     To install a specific version of *Percona Server for MongoDB*, do the following:

     1. List available versions:

         ```{.bash data-prompt="$"}
         $ sudo yum list percona-server-mongodb --showduplicates
         ```

        Sample output:

         ```{.bash .no-copy}
             Available Packages
         
         percona-server-mongodb.x86_64    7.0.2-1.el9       psmdb-70-release-x86_64
         ```

     2. Install a specific version packages. For example, to install *Percona Server for MongoDB* 7.0.2-1, run the following command:

        ```{.bash data-prompt="$"}
        $ sudo yum install percona-server-mongodb-7.0.2-1.el9
        ```

By default, Percona Server for MongoDB stores data files in `/var/lib/mongodb/`
and configuration parameters in `/etc/mongod.conf`.

## Run Percona Server for MongoDB

!!! note

    If you use SELinux in enforcing mode, you must customize your SELinux user policies to allow access to certain `/sys` and `/proc` files for OS-level statistics. Also, you must customize directory and port access policies if you are using non-default locations.

    Please refer to [Configure SELinux](https://docs.mongodb.com/v6.0/tutorial/install-mongodb-on-red-hat/#configure-selinux) section of MongoDB Documentation for policy configuration guidelines.

By default, Percona Server for MongoDB stores data files in `/var/lib/mongodb/`
and configuration parameters in `/etc/mongod.conf`.

**Start the service**

Percona Server for MongoDB is not started automatically after installation.
Start it manually using the following command:

```{.bash data-prompt="$"}
$ sudo systemctl start mongod
```

**Confirm that service is running**

Check the service status using the following command: `service mongod status`

```{.bash data-prompt="$"}
$ sudo systemctl status mongod
```

**Stop the service**

Stop the service using the following command: `service mongod stop`

```{.bash data-prompt="$"}
$ sudo systemctl stop mongod
```

**Restart the service**

Restart the service using the following command: `service mongod restart`

```{.bash data-prompt="$"}
$ sudo systemctl restart mongod
```

### Run after reboot

The `mongod` service is not automatically started
after you reboot the system.

To make it start automatically after reboot, enable it using the systemctl utility:

```{.bash data-prompt="$"}
$ sudo systemctl enable mongod
```

Then start the `mongod` service:

```{.bash data-prompt="$"}
$ sudo systemctl start mongod
```

## Next steps

[Connect to MongoDB :material-arrow-right:](../connect.md){.md-button}

