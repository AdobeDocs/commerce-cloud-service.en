---
title: Set up MySQL service
description: Learn how to manage the MySQL service for persistent data storage with Adobe Commerce on cloud infrastructure.
feature: Cloud, Services, Storage
exl-id: 70820d00-8b82-4b60-87e4-ea98fd7ffcb2
---
# Set up MySQL service

The `mysql` service provides persistent data storage based on [MariaDB](https://mariadb.com/) versions 10.2 to 10.4, supporting the [XtraDB](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) storage engine and reimplemented features from MySQL 5.6 and 5.7.

Reindexing on MariaDB 10.4 takes more time compared to other MariaDB or MySQL versions. See [Indexers](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers) in the _Performance Best Practices_ guide.

>[!WARNING]
>
>Be careful when upgrading MariaDB from version 10.1 to 10.2. MariaDB 10.1 is the last version that supports _XtraDB_ as the storage engine. MariaDB 10.2 uses _InnoDB_ for the storage engine. After you upgrade from 10.1 to 10.2, you cannot roll back the change. Adobe Commerce supports both storage engines; however, you must check extensions and other systems used by your project to make sure they are compatible with MariaDB 10.2. See [Incompatible Changes Between 10.1 and 10.2](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**To enable MySQL**:

1. Add the required name, type, and disk value (in MB) to the `.magento/services.yaml` file.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >MySQL errors, such as `PDO Exception: MySQL server has gone away`, can occur as a result of insufficient disk space. Verify that you have allocated sufficient disk space to the service in the [`.magento/services.yaml`](services-yaml.md#disk) file.

1. Configure the relationships in the `.magento.app.yaml` file.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. Add, commit, and push your code changes.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [Verify the service relationships](services-yaml.md#service-relationships).

{{service-change-tip}}

## Configure MySQL database

You have the following options when configuring the MySQL database:

- **`schemas`**—A schema defines a database. The default schema is the `main` database.
- **`endpoints`**—Each endpoint represents a credential with specific privileges. The default endpoint is `mysql`, which has `admin` access to the `main` database.
- **`properties`**—Properties are used to define additional database configurations.

The following is a basic example configuration in the `.magento/services.yaml` file:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

The `properties` in the above example modifies the default `optimizer` settings as [recommended in the Performance Best Practices guide](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html#indexers).

**MariaDB configuration options**:

| Options              | Description                                         | Default value      |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset`    | The default character set.                          | utf8mb4            |
| `default_collation`  | The default collation.                              | utf8mb4_unicode_ci |
| `max_allowed_packet` | Maximum size for packets, in MB. Range `1` to `100`.| 16                 |
| `optimizer_switch`   | Set values for the query optimizer. See [MariaDB documentation](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Select the statistics used by the optimizer. Range `1` to `5`. See [MariaDB documentation](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 for 10.4 and later |

### Set up multiple database users

Optionally, you can set up multiple users with different permissions for accessing the `main` database.

By default, there is one endpoint named `mysql` that has administrator access to the database. To set up multiple database users, you must define multiple endpoints in the `services.yaml` file and declare the relationships in the `.magento.app.yaml` file. For Pro Staging and Production environments, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to request the additional user.

Use a nested array to define the endpoints for specific user access. Each endpoint can designate access to one or more schemas (databases) and different levels of permission on each.

The valid permission levels are:

- `ro`: Only SELECT queries are allowed.
- `rw`: SELECT queries and INSERT, UPDATE, and DELETE queries are allowed.
- `admin`: All queries are allowed, including DDL queries (CREATE TABLE, DROP TABLE, and more).

For example:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

In the preceding example, the `admin` endpoint provides admin-level access to the `main` database, the `reporter` endpoint provides read-only access, and the `importer` endpoint provides read-write access, which means:

- The `admin` user has full control of the database.
- The `reporter` user has SELECT privileges only.
- The `importer` user has SELECT, INSERT, UPDATE, and DELETE privileges.

Add the endpoints defined in the above example to the `relationships` property of the `.magento.app.yaml` file. For example:

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>If you configure one MySQL user, you cannot use the [`DEFINER`](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) access control mechanism for stored procedures and views.

## Connect to the database

Accessing the MariaDB database directly requires you to use an SSH to log in to the remote Cloud environment, and connect to the database.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Retrieve the MySQL login credentials from the `database` and `type` properties in the [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variable.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   or

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In the response, find the MySQL information. For example:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Connect to the database.

   - For Starter, use the following command:

     ```bash
     mysql -h database.internal -u <username>
     ```

   - For Pro, use the following command with hostname, port number, username, and password retrieved from the `$MAGENTO_CLOUD_RELATIONSHIPS` variable.

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>You can use the `magento-cloud db:sql` command to connect to the remote database and run SQL commands.

## Connect to secondary database

Sometimes, you have to connect to the secondary database to improve database performance or resolve database locking issues. If this configuration is required, use `"port" : 3304` to establish the connection. See the [Best practice to configure the MySQL slave connection](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html) topic in the _Implementation Best Practices_ guide.

## Troubleshooting

See the following Adobe Commerce Support articles for help with troubleshooting MySQL problems:

- [Checking slow queries and processes MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html)
- [Create database dump on Cloud](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html)
- [Data Migration Tool troubleshooting](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html)
- [Adobe Commerce upgrade: compact to dynamic tables 2.2.x, 2.3.x to 2.4.x](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html)
