# ece-tools

<!-- The template to render with above values -->
**Version**: 2002.1.19

This reference contains 34 commands available through the `ece-tools` command-line tool.
The initial list is auto generated using the `ece-tools list` command at Adobe Commerce on cloud infrastructure.

>[!NOTE]
>
>This reference is generated from the application codebase. To change the content, you can update the source code for the corresponding command implementation in the [codebase](https://github.com/magento/magento-cloud-cli) repository and submit your changes for review. Another way is to _Give us feedback_ (find the link at the upper right). For contribution guidelines, see [Code Contributions](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

## `_complete`

Internal command to provide shell completion suggestions

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

### `--shell`, `-s`

The shell type ("bash", "fish", "zsh")
   
-  Requires a value

### `--input`, `-i`

An array of input tokens (e.g. COMP_WORDS or argv)
   
-  Default: `[]`
-  Requires a value

### `--current`, `-c`

The index of the "input" array that the cursor is in (e.g. COMP_CWORD)
   
-  Requires a value

### `--api-version`, `-a`

The API version of the completion script
   
-  Requires a value

### `--symfony`, `-S`

deprecated
   
-  Requires a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `build`

Builds application.

```bash
ece-tools build
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `completion`

Dump the shell completion script

```bash
ece-tools completion [--debug] [--] [<shell>]
```


### `shell`

The shell type (e.g. "bash"), the value of the "$SHELL" env var will be used if this is not given
   

### `--debug`

Tail the completion debug log
   
-  Default: `false`
-  Does not accept a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `db-dump`

Creates database backups.

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```


### `databases`

Databases for backup. Available Values: [ main quote sales ]. If the argument value is not specified, database backups will be created using the credentials stored in the `MAGENTO_CLOUD_RELATIONSHIP` environment variable or/and the `stage.deploy.DATABASE_CONFIGURATION` property of the .magento.env.yaml configuration file.
   
-  Default: `[]`
   
-  Array

### `--remove-definers`, `-d`

Remove definers from the database dump
   
-  Default: `false`
-  Does not accept a value

### `--dump-directory`, `-a`

Use alternative directory for saving dump
   
-  Requires a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `deploy`

Deploys the application.

```bash
ece-tools deploy
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `help`

Display help for a command

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```


### `command_name`

The command name
   
-  Default: `help`
   

### `--format`

The output format (txt, xml, json, or md)
   
-  Default: `txt`
-  Requires a value

### `--raw`

To output raw command help
   
-  Default: `false`
-  Does not accept a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `list`

List commands

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```


### `namespace`

The namespace name
   

### `--raw`

To output raw command list
   
-  Default: `false`
-  Does not accept a value

### `--format`

The output format (txt, xml, json, or md)
   
-  Default: `txt`
-  Requires a value

### `--short`

To skip describing commands' arguments
   
-  Default: `false`
-  Does not accept a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `patch`

Applies custom patches.

```bash
ece-tools patch
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `post-deploy`

Performs after deploy operations.

```bash
ece-tools post-deploy
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `run`

Execute scenario(s).

```bash
ece-tools run <scenario>...
```


### `scenario`

Scenario(s)
   
-  Default: `[]`
   
-  Required
-  Array

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `backup:list`

Shows the list of backup files.

```bash
ece-tools backup:list
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `backup:restore`

Restore important configuration files. Run backup:list to show the list of backup files.

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

### `--force`, `-f`

Overwrite existing files during restoring a backup
   
-  Default: `false`
-  Does not accept a value

### `--file`

A specific file recovery path
   
-  Accepts a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `build:generate`

Generates all necessary files for build stage.

```bash
ece-tools build:generate
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `build:transfer`

Transfers generated files into init directory.

```bash
ece-tools build:transfer
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cloud:config:create`

Creates a `.magento.env.yaml` file with the specified build, deploy, and post-deploy variable configuration. Overwrites any existing `.magento,.env.yaml` file.

```bash
ece-tools cloud:config:create <configuration>
```


### `configuration`

Configuration in JSON format
   
-  Required

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cloud:config:update`

Updates the existing `.magento.env.yaml` file with the specified configuration. Creates `.magento.env.yaml` file if it does not exist.

```bash
ece-tools cloud:config:update <configuration>
```


### `configuration`

Configuration in JSON format
   
-  Required

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cloud:config:validate`

Validates `.magento.env.yaml` configuration file

```bash
ece-tools cloud:config:validate
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `config:dump`

Dump configuration for static content deployment.

```bash
ece-tools config:dump
```


```bash
ece-tools dump
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cron:disable`

Disable all Magento cron processes and terminates all running processes.

```bash
ece-tools cron:disable
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cron:enable`

Enables Magento cron processes.

```bash
ece-tools cron:enable
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cron:kill`

Terminates all Magento cron processes.

```bash
ece-tools cron:kill
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `cron:unlock`

Unlock cron jobs that stuck in "running" state.

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

### `--job-code`

Cron job code to unlock.
   
-  Default: `[]`
-  Accepts multiple values

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `dev:generate:schema-error`

Generates the dist/error-codes.md file from the schema.error.yaml file.

```bash
ece-tools dev:generate:schema-error
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `dev:git:update-composer`

Updates composer for deployment from git.

```bash
ece-tools dev:git:update-composer
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `env:config:show`

Display encoded cloud configuration environment variables.

```bash
ece-tools env:config:show [<variable>...]
```


### `variable`

Environment variables to display, possible options: services,routes,variables
   
-  Default: `[]`
   
-  Array

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `error:show`

Displays info about error by error id or info about all errors from the last deployment.

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```


### `error-code`

Error code, if not passed command display info about all errors from the last deployment
   

### `--json`, `-j`

Used for getting result in JSON format
   
-  Default: `false`
-  Does not accept a value

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `module:refresh`

Refreshes the configuration to enable newly added modules.

```bash
ece-tools module:refresh
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `schema:generate`

Generates the schema *.dist file.

```bash
ece-tools schema:generate
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:ideal-state`

Verifies ideal state of configuration.

```bash
ece-tools wizard:ideal-state
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:master-slave`

Verifies master-slave configuration.

```bash
ece-tools wizard:master-slave
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:scd-on-build`

Verifies SCD on build configuration.

```bash
ece-tools wizard:scd-on-build
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:scd-on-demand`

Verifies SCD on demand configuration.

```bash
ece-tools wizard:scd-on-demand
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:scd-on-deploy`

Verifies SCD on deploy configuration.

```bash
ece-tools wizard:scd-on-deploy
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value


## `wizard:split-db-state`

Verifies ability to split DB and whether DB was already split or not.

```bash
ece-tools wizard:split-db-state
```

### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command
   
-  Default: `false`
-  Does not accept a value

### `--quiet`, `-q`

Do not output any message
   
-  Default: `false`
-  Does not accept a value

### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
   
-  Default: `false`
-  Does not accept a value

### `--version`, `-V`

Display this application version
   
-  Default: `false`
-  Does not accept a value

### `--ansi`

Force (or disable --no-ansi) ANSI output
   
-  Does not accept a value

### `--no-ansi`

Negate the "--ansi" option
   
-  Default: `false`
-  Does not accept a value

### `--no-interaction`, `-n`

Do not ask any interactive question
   
-  Default: `false`
-  Does not accept a value

