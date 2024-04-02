---
title: PHP settings
description: Learn about the optimal PHP settings for Commerce application configuration in the cloud infrastructure.
feature: Cloud, Configuration, Extensions
exl-id: b4180265-f7a1-48e4-8c23-27835253e171
---
# PHP settings

You can choose which [version of PHP](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) to run in your `.magento.app.yaml` file:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>If upgrading to PHP 8.1 and later, remove JSON from the [`runtime: extensions:` property](properties.md#runtime) in the `.magento.app.yaml` file and redeploy. The JSON extension comes installed in Cloud environment since PHP 8.0.

## Configure PHP

You can customize the PHP settings for your environment using a `php.ini` file that is appended to the configuration maintained by Adobe Commerce.

In your repository, add the `php.ini` file to the root of the application (the repository root).

>[!TIP]
>
>Configuring PHP settings improperly can cause issues, so only advanced administrators should set these options.

### Increase PHP memory limit

To increase the PHP memory limit, add the following setting to the `php.ini` file:

```ini
memory_limit = 1G
```

For debugging, increase the value to 2G.

### Optimize realpath_cache configuration

Set the following `realpath_cache` settings to improve application performance.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

These settings allow PHP processes to cache paths to files instead of looking them up for each page load. See [Performance Tuning](https://www.php.net/manual/en/ini.core.php) in the PHP documentation.

>[!NOTE]
>
>For a list of recommended PHP configuration settings, see [Required PHP settings](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) in the _Installation guide_.

### Check custom PHP settings

After pushing the `php.ini` changes to your Cloud environment, you can check that the custom PHP configuration has been added to your environment. For example, use SSH to log in to the remote environment and view the file using something similar to the following:

```bash
cat /etc/php/<php-version>/fpm/php.ini
```

>[!WARNING]
>
>If you use Cloud Docker for Commerce for local development, see [Docker service containers](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#fpm-container) for information about using a custom `php.ini` file in a Docker environment.

## Enable extensions

You can enable or disable PHP extensions in the `runtime:extension` section. Also, the extensions specified become available in the Docker PHP containers.

>[!IMPORTANT]
>
>Before enabling extensions, it is important to understand that the PHP version must be compatible with the operating system hosting the project. Your project environment might require an OS upgrade by the Infrastructure team before you can proceed.

Example in `.magento.app.yaml` file:

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Use SSH to log in to an environment and list the PHP extensions.

```bash
php -m
```

For details about a specific PHP extension, see the [PHP Extension List](https://www.php.net/manual/en/extensions.alphabetical.php).

The following table shows the supported PHP extensions when deploying Adobe Commerce on the Cloud platform.

| Default extensions | Installed extensions<br>that cannot be uninstalled | Extensions that can be installed<br>and uninstalled as needed |
| ------------------ | --------------------- | --------------------- |
| `bcmath`<br>`bz2`<br>`calendar`<br>`exif`<br>`gd`<br>`gettext`<br> `intl`<br> `libxml` <br> `mysqli`<br> `openswoole`<br> `pcntl`<br> `pdo_mysql`<br> `Reflection` <br> `SPL` <br> `standard` <br> `soap`<br> `sockets`<br>  `sysvmsg`<br> `sysvsem`<br> `sysvshm`<br> `opcache` <br> `zip` <br> `zlib` | `ctype`<br> `curl`<br>`date`<br> `dba` <br> `dom`<br> `fileinfo`<br> `filter`<br> `ftp`<br> `hash`<br> `iconv`<br> `json`<br> `mbstring`<br> `mysqlnd`<br> `openssl`<br> `pcre`<br> `pdo`<br> `pdo_sqlite`<br> `phar`<br>`posix`<br> `readline`<br> `session` <br> `sqlite3`<br> `tokenizer`<br> `xml`<br> `xmlreader`<br> `xmlwriter`<br> |`geoip`<br>`gmp`<br> `igbinary`<br> `imagick`<br> `imap` <br>`ldap`<br> `mailparse`<br> `mcrypt`<br> `msgpack`<br> `mysqli`<br> `oauth`<br> `pdo_mysql`<br> `propro`<br> `pspell`<br> `raphf`<br> `recode`<br> `redis`<br> `shmop` <br> `sockets`<br> `sodium`<br> `ssh2`<br>`tidy`<br> `xdebug`<br> `xmlrpc`<br> `xsl`<br> `yaml` |

PHP module requirements are tied to the Adobe Commerce version. See [PHP requirements](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Extension support

For Pro projects, the following extensions require additional support to install:

- `sourceguardian`

For example, to set up PHP to execute only SourceGuardian-protected scripts in all environments, the following option must be set in the `php.ini` file:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

See [section 3.5 of the SourceGuardian documentation](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _This is a link to a PDF_.

[Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) for help with installing these PHP extensions in all Production environments and Pro Staging environments. Include your updated `.magento/services.yaml` file, `.magento.app.yaml` file with the updated PHP version and any additional PHP extensions. For changes to a live Production environment, you must provide a minimum of 48 hours notice. It can take up to 48 hours for the Cloud infrastructure team to update your project.

>[!WARNING]
>
>PHP compiled with debug is not supported and the Probe may conflict with [!DNL XDebug] or [!DNL XHProf]. Disable those extensions when enabling the Probe. The Probe conflicts with some PHP extensions like [!DNL Pinba] or IonCube.
