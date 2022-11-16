---
title: Hooks property
description: See examples on how to configure the hooks property in the Commerce application configuration file.
---

# Hooks property

Use the `hooks` section to run shell commands during the build, deploy, and post-deploy phases:

-  **`build`**—Execute commands _before_ packaging your application. Services, such as the database or Redis, are not available at this time since the application has not been deployed yet. You must add custom commands _before_ the default `php ./vendor/bin/ece-tools` command so that custom-generated content continues to the deployment phase.

-  **`deploy`**—Execute commands _after_ packaging and deploying your application. You can access other services at this point. Since the default `php ./vendor/bin/ece-tools` command copies the `app/etc` directory to the correct location, you must add custom commands _after_ the deploy command to prevent custom commands from failing.

-  **`post_deploy`**—Execute commands _after_ deploying your application and _after_ the container begins accepting connections. The `post_deploy` hook clears the cache and preloads (warms) the cache. You can customize the list of pages using the `WARM_UP_PAGES` variable in the [Post-deploy stage](../environment/variables-post-deploy.md). Although not required, this works in tandem with the `SCD_ON_DEMAND` environment variable.

Add CLI commands under the `build`, `deploy`, or `post_deploy` sections _before_ the `ece-tools` command:

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Also, you can customize the build phase further by using the `generate` and `transfer` commands to perform additional actions when specifically building code or moving files.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

-  `set -e`—causes hooks to fail on the first failed command, instead of the final failed command.
-  `build:generate`—applies patches, validates configuration, generates DI, and generates static content if SCD is enabled for build phase.
-  `build:transfer`—transfers generated code and static content to the final destination.

The commands run from the application (`/app`) directory. You can use the `cd` command to change the directory. The hooks fail if the final command in them fails. To cause them to fail on the first failed command, add `set -e` to the beginning of the hook.

**To compile Sass files using grunt**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

You must compile Sass files using `grunt` before static content deployment, which happens during the build. Place the `grunt` command before the `build` command.

{{scenarios}}
