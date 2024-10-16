# ece-tools

**Version**: 2002.2.0

This reference contains 34 commands available through the `ece-tools` command-line tool.
The initial list is auto generated using the `ece-tools list` command at Adobe Commerce on cloud infrastructure.

## General

This reference is generated from the application codebase. To change the content, _Give us feedback_ (find the link at the upper right). For contribution guidelines, see [Code Contributions](https://developer.adobe.com/commerce/contributor/guides/code-contributions/).

### Global options

#### `--help`, `-h`

Display help for the given command. When no command is given display help for the list command

- Default: `false`
- Does not accept a value

#### `--quiet`, `-q`

Do not output any message

- Default: `false`
- Does not accept a value

#### `--verbose`, `-v|-vv|-vvv`

Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

- Default: `false`
- Does not accept a value

#### `--version`, `-V`

Display this application version

- Default: `false`
- Does not accept a value

#### `--ansi`

Force (or disable --no-ansi) ANSI output

- Does not accept a value

#### `--no-ansi`

Negate the "--ansi" option

- Default: `false`
- Does not accept a value

#### `--no-interaction`, `-n`

Do not ask any interactive question

- Default: `false`
- Does not accept a value


## `_complete`

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

Internal command to provide shell completion suggestions

### Options

For global options, see [Global options](#global-options).

#### `--shell`, `-s`

The shell type ("bash", "fish", "zsh")

- Requires a value

#### `--input`, `-i`

An array of input tokens (e.g. COMP_WORDS or argv)

- Default: `[]`
- Requires a value

#### `--current`, `-c`

The index of the "input" array that the cursor is in (e.g. COMP_CWORD)

- Requires a value

#### `--api-version`, `-a`

The API version of the completion script

- Requires a value

#### `--symfony`, `-S`

deprecated

- Requires a value


## `build`

```bash
ece-tools build
```

Builds application.

### Options

For global options, see [Global options](#global-options).


## `completion`

```bash
ece-tools completion [--debug] [--] [<shell>]
```

Dump the shell completion script

```
The completion command dumps the shell completion script required
to use shell autocompletion (currently, bash, fish, zsh completion are supported).

Static installation
-------------------

Dump the script to a global completion file and restart your shell:

    bin/ece-tools completion  | sudo tee /etc/bash_completion.d/ece-tools

Or dump the script to a local file and source it:

    bin/ece-tools completion  > completion.sh

    # source the file whenever you use the project
    source completion.sh

    # or add this line at the end of your "~/.bashrc" file:
    source /path/to/completion.sh

Dynamic installation
--------------------

Add this to the end of your shell configuration file (e.g. "~/.bashrc"):

    eval "$(/var/jenkins/workspace/gendocs-ece-tools-cli/bin/ece-tools completion )"
```

### Arguments

#### `shell`

The shell type (e.g. "bash"), the value of the "$SHELL" env var will be used if this is not given

### Options

For global options, see [Global options](#global-options).

#### `--debug`

Tail the completion debug log

- Default: `false`
- Does not accept a value


## `db-dump`

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```

Creates database backups.

### Arguments

#### `databases`

Databases for backup. Available Values: [ main quote sales ]. If the argument value is not specified, database backups will be created using the credentials stored in the `MAGENTO_CLOUD_RELATIONSHIP` environment variable or/and the `stage.deploy.DATABASE_CONFIGURATION` property of the .magento.env.yaml configuration file.

- Default: `[]`
- Array
   
### Options

For global options, see [Global options](#global-options).

#### `--remove-definers`, `-d`

Remove definers from the database dump

- Default: `false`
- Does not accept a value

#### `--dump-directory`, `-a`

Use alternative directory for saving dump

- Requires a value


## `deploy`

```bash
ece-tools deploy
```

Deploys the application.

### Options

For global options, see [Global options](#global-options).


## `help`

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```

Display help for a command

```
The help command displays help for a given command:

  bin/ece-tools help list

You can also output the help in other formats by using the --format option:

  bin/ece-tools help --format=xml list

To display the list of available commands, please use the list command.
```

### Arguments

#### `command_name`

The command name

- Default: `help`

### Options

For global options, see [Global options](#global-options).

#### `--format`

The output format (txt, xml, json, or md)

- Default: `txt`
- Requires a value

#### `--raw`

To output raw command help

- Default: `false`
- Does not accept a value


## `list`

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```

List commands

```
The list command lists all commands:

  bin/ece-tools list

You can also display the commands for a specific namespace:

  bin/ece-tools list test

You can also output the information in other formats by using the --format option:

  bin/ece-tools list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  bin/ece-tools list --raw
```

### Arguments

#### `namespace`

The namespace name

### Options

For global options, see [Global options](#global-options).

#### `--raw`

To output raw command list

- Default: `false`
- Does not accept a value

#### `--format`

The output format (txt, xml, json, or md)

- Default: `txt`
- Requires a value

#### `--short`

To skip describing commands' arguments

- Default: `false`
- Does not accept a value


## `patch`

```bash
ece-tools patch
```

Applies custom patches.

### Options

For global options, see [Global options](#global-options).


## `post-deploy`

```bash
ece-tools post-deploy
```

Performs after deploy operations.

### Options

For global options, see [Global options](#global-options).


## `run`

```bash
ece-tools run <scenario>...
```

Execute scenario(s).

### Arguments

#### `scenario`

Scenario(s)

- Default: `[]`
- Required

- Array
   
### Options

For global options, see [Global options](#global-options).


## `backup:list`

```bash
ece-tools backup:list
```

Shows the list of backup files.

### Options

For global options, see [Global options](#global-options).


## `backup:restore`

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

Restore important configuration files. Run backup:list to show the list of backup files.

### Options

For global options, see [Global options](#global-options).

#### `--force`, `-f`

Overwrite existing files during restoring a backup

- Default: `false`
- Does not accept a value

#### `--file`

A specific file recovery path

- Accepts a value


## `build:generate`

```bash
ece-tools build:generate
```

Generates all necessary files for build stage.

### Options

For global options, see [Global options](#global-options).


## `build:transfer`

```bash
ece-tools build:transfer
```

Transfers generated files into init directory.

### Options

For global options, see [Global options](#global-options).


## `cloud:config:create`

```bash
ece-tools cloud:config:create <configuration>
```

Creates a `.magento.env.yaml` file with the specified build, deploy, and post-deploy variable configuration. Overwrites any existing `.magento,.env.yaml` file.

### Arguments

#### `configuration`

Configuration in JSON format

- Required

### Options

For global options, see [Global options](#global-options).


## `cloud:config:update`

```bash
ece-tools cloud:config:update <configuration>
```

Updates the existing `.magento.env.yaml` file with the specified configuration. Creates `.magento.env.yaml` file if it does not exist.

### Arguments

#### `configuration`

Configuration in JSON format

- Required

### Options

For global options, see [Global options](#global-options).


## `cloud:config:validate`

```bash
ece-tools cloud:config:validate
```

Validates `.magento.env.yaml` configuration file

### Options

For global options, see [Global options](#global-options).


## `config:dump`

```bash
ece-tools config:dumpdump
```

Dump configuration for static content deployment.

### Options

For global options, see [Global options](#global-options).


## `cron:disable`

```bash
ece-tools cron:disable
```

Disable all Magento cron processes and terminates all running processes.

### Options

For global options, see [Global options](#global-options).


## `cron:enable`

```bash
ece-tools cron:enable
```

Enables Magento cron processes.

### Options

For global options, see [Global options](#global-options).


## `cron:kill`

```bash
ece-tools cron:kill
```

Terminates all Magento cron processes.

### Options

For global options, see [Global options](#global-options).


## `cron:unlock`

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

Unlock cron jobs that stuck in "running" state.

### Options

For global options, see [Global options](#global-options).

#### `--job-code`

Cron job code to unlock.

- Default: `[]`
- Accepts multiple values


## `dev:generate:schema-error`

```bash
ece-tools dev:generate:schema-error
```

Generates the dist/error-codes.md file from the schema.error.yaml file.

### Options

For global options, see [Global options](#global-options).


## `dev:git:update-composer`

```bash
ece-tools dev:git:update-composer
```

Updates composer for deployment from git.

### Options

For global options, see [Global options](#global-options).


## `env:config:show`

```bash
ece-tools env:config:show [<variable>...]
```

Display encoded cloud configuration environment variables.

### Arguments

#### `variable`

Environment variables to display, possible options: services,routes,variables

- Default: `[]`
- Array
   
### Options

For global options, see [Global options](#global-options).


## `error:show`

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```

Displays info about error by error id or info about all errors from the last deployment.

### Arguments

#### `error-code`

Error code, if not passed command display info about all errors from the last deployment

### Options

For global options, see [Global options](#global-options).

#### `--json`, `-j`

Used for getting result in JSON format

- Default: `false`
- Does not accept a value


## `module:refresh`

```bash
ece-tools module:refresh
```

Refreshes the configuration to enable newly added modules.

### Options

For global options, see [Global options](#global-options).


## `schema:generate`

```bash
ece-tools schema:generate
```

Generates the schema *.dist file.

### Options

For global options, see [Global options](#global-options).


## `wizard:ideal-state`

```bash
ece-tools wizard:ideal-state
```

Verifies ideal state of configuration.

### Options

For global options, see [Global options](#global-options).


## `wizard:master-slave`

```bash
ece-tools wizard:master-slave
```

Verifies master-slave configuration.

### Options

For global options, see [Global options](#global-options).


## `wizard:scd-on-build`

```bash
ece-tools wizard:scd-on-build
```

Verifies SCD on build configuration.

### Options

For global options, see [Global options](#global-options).


## `wizard:scd-on-demand`

```bash
ece-tools wizard:scd-on-demand
```

Verifies SCD on demand configuration.

### Options

For global options, see [Global options](#global-options).


## `wizard:scd-on-deploy`

```bash
ece-tools wizard:scd-on-deploy
```

Verifies SCD on deploy configuration.

### Options

For global options, see [Global options](#global-options).


## `wizard:split-db-state`

```bash
ece-tools wizard:split-db-state
```

Verifies ability to split DB and whether DB was already split or not.

### Options

For global options, see [Global options](#global-options).
