---
title: Commerce Command-line Tools
description: Use the Commerce command-line tools to manage programs, environments, and pipelines for Commerce on AEC.
---
# Commerce command-line tools

Commerce provides a command-line interface to perform installation and configuration tasks. Because Commerce on Experience Cloud has a Cloud Manager program UI, some of those commands are now included in the Cloud Manager plugin.

As stated in the Getting started workflow, you must install the following tools to begin using the CLI:

- [Node.js version 14 or 12][node]
- [Adobe I/O Extensible CLI (AIO)][aio-cli]
- [Cloud Manager plugin for AIO][cm-plugin]

## Cloud Manager plugin tool

The Cloud Manager CLI is a plugin for the general-purpose Adobe I/O CLI. You can use the CLI to manage Commerce programs, environments, and pipelines to streamline your developer experience. The CLI communicates between your local machine and the remote resources hosting your code.

Verify the installation by listing the programs available to your identity:

```bash
aio cloudmanager:list-programs
```

>[!TIP]
>
>If you are experiencing problems with the CLI, see [Command-line authentication](cli-authentication.md) or try updating the CLI tools.

## Commerce commands

Commerce commands are part of the Cloud Manager plugin. Use the following to list the available Commerce commands:

```bash
aio cloudmanager:commerce:bin-magento
```

### `app`

The database contains default configurations for your store. Configuration changes apply to the `app/etc/config.php` file. You can then use this file to manage and synchronize the application configuration across multiple environments.

```bash
aio cloudmanager:commerce:bin-magento:app:config
```

- `dump`—Create a configuration dump.
- `import`—Import data from shared configuration files to a data storage. See [Import data from configuration files][import-dump] in the _Commerce developer_ documentation.

### `cache`

Purge the cache using the `clean` and `flush` options.

- `clean`—deletes all items from enabled cache types only. As a best practice, always clean the cache after an upgrade process or after installing any module.
- `flush`—purges the cache storage, which might affect processes using the same storage. If you are still experiencing problems after cleaning the cache, try using flush option.

### `indexer`

Manually reindex all or selected indexers one time only. Use to set up a cron job that runs at qualifying or regular intervals.

### `maintenance`

Enabling maintenance mode takes your site offline and allows write access for updates and configuration changes.

- `enable`—Enable maintenance mode. Site visitors see a default `Service Temporarily Unavailable` page.
- `disable`—Disable maintenance mode. Site becomes available.
- `status`—Verify that maintenance mode is active or not active, and view a list of exempt IP addresses from an allowlist.

<!-- link definitions -->

[aio-cli]: https://github.com/adobe/aio-cli
[cm-plugin]: https://github.com/adobe/aio-cli-plugin-cloudmanager
[node]: https://nodejs.org/en/download/package-manager/
[import-dump]: https://devdocs.magento.com/guides/v2.4/config-guide/cli/config-cli-subcommands-config-mgmt-import.html
