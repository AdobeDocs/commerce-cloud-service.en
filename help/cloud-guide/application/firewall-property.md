---
title: Firewall property
description: See examples on how to configure the firewall property in the Commerce application configuration file.
feature: Cloud, Configuration, Security
exl-id: f169c008-c62a-41b7-a98d-cccd81c7291a
---
# Firewall property

>[!IMPORTANT]
>
>Starter projects only

For Starter projects, the `firewall` property adds an _outbound_ firewall to the application. This firewall has no effect on incoming requests. It defines which `tcp` outbound requests can _leave_ an Adobe Commerce site. This is called egress filtering. The outbound firewall filters what can egress—exit or escape your site. Limiting what can escape adds a powerful security tool to your server.

## Default restriction policies

The firewall provides two default policies to control outbound traffic: `allow` and `deny`. The `allow` policy _allows_ all outbound traffic by default. And the `deny` policy _denies_ all outbound traffic by default. But when you add a rule, the default policy is overridden, and the firewall blocks **all** outbound traffic not allowed by the rule.

For Starter plans, the default policy is set to `allow`. This setting ensures that all your current outbound traffic remains unblocked until you add your egress-filtering rules. The default policy can be set to `deny` upon request.

**To check your default policy**:

```bash
magento-cloud p:curl --project PROJECT_ID /settings | grep -i outbound
```

Unless you requested `deny` for your policy, the command should show your policy set to `allow`:

```terminal
"outbound_restrictions_default_policy": "allow"
```

>[!NOTE]
>
>**Key takeaway**: When you add an outbound rule, you block all outbound traffic except for the domains, IP addresses, or ports you add to the rule. So it is important to have a full outbound list defined and tested before adding it to your production site.

## Firewall options

The following example configuration in the `.magento.app.yaml` file shows all the `firewall` options that you can use to add rules for your egress filtering.

```yaml
firewall:
    outbound:
        - # Common accessed domains
            domains:
                - newrelic.com
                - fastly.com
                - magento.com
                - magentocommerce.com
                - google.com
            ports:
                - 80
                - 443
            protocol: tcp # Can be omitted from rules.

        - # Adobe Stock integration
            domains:
                - account.adobe.com
                - stock.adobe.com
                - console.adobe.io
            ports:
                - 80
                - 443

        - # Payment services
            domains:
                - braintreepayments.com
                - paypal.com
            ports:
                - 80
                - 443

        - # Shipping services
            domains:
                - ups.com
                - usps.com
                - fedex.com
                - dhl.com
            ports:
                - 80
                - 443

        - # Vertex Integrated Address Cleansing
            domains:
                - mgcsconnect.vertexsmb.com
            ports:
                - 80
                - 443

        - # New Relic networks
            ips:
                - 162.247.240.0/22 # US region accounts
                - 185.221.84.0/22 # EU region accounts
            ports:
                - 443

        - # New Relic endpoints
            domains:
                - collector.newrelic.com, # US region accounts
                - collector.eu01.nr-data.net # EU region accounts
            ports:
                - 443

        - # Fastly IP ranges
            ips:
                - 23.235.32.0/20
                - 43.249.72.0/22
                - 103.244.50.0/24
                - 103.245.222.0/23
                - 103.245.224.0/24
                - 104.156.80.0/20
                - 146.75.0.0/16
                - 151.101.0.0/16
                - 157.52.64.0/18
                - 167.82.0.0/17
                - 167.82.128.0/20
                - 167.82.160.0/20
                - 167.82.224.0/20
                - 172.111.64.0/18
                - 185.31.16.0/22
                - 199.27.72.0/21
                - 199.232.0.0/16
            ports:
                - 80
                - 443
```

## Egress filtering rules

Outbound firewall configurations are made up of rules. You can define as many rules as you need. The requirements for rules are as follows.

**Each rule:**

-  Must start with a hyphen (`-`). Adding a comment on the same line helps document and visually separate one rule from the next.
-  Must define at least one of the following options: `domains`, `ips`, or `ports`.
-  Must use the `tcp` protocol. Because this is the default protocol for all rules, you can omit it from the rule.
-  Can define `domains` or `ips`, but not both in the same rule.
-  Can include `yaml` comments (`#`) and line breaks to organize the domains, IP addresses, and ports allowed.

Each rule uses the following properties:

### `domains`

The `domains` option allows a list of fully qualified domain names (FQDN).

If a rule defines `domains` but not `ports`, the firewall allows domain requests on any port.

### `ips`

The `ips` option allows a list of IP addresses in the CIDR notation. You can specify single IP addresses or ranges of IP addresses.

To specify a single IP address, add the `/32` CIDR prefix to the end of your IP address:

```terminal
172.217.11.174/32  # google.com
```

To specify a range of IP addresses, use the [IP Range to CIDR](https://ipaddressguide.com/cidr) calculator.

If a rule defines `ips` but not `ports`, the firewall allows IP requests on any port.

### `ports`

The `ports` option allows a list of ports from 1 to 65535. For most rules in the example, ports `80` and `443` allow both HTTP and HTTPS requests. But for New Relic, the rules only allow access to domains and IP addresses on port `443`, as recommended in the New Relic documentation on [Network Traffic](https://docs.newrelic.com/docs/new-relic-solutions/get-started/networks/#agents).

If a rule only defines `ports`, the firewall allows access to all domains and IP addresses for the ports defined.

>[!NOTE]
>
>Port `25`, the SMTP port to send email, is always blocked, without exception.

### `protocol`

As mentioned, TCP is the default and only protocol allowed for rules. UDP and its ports are not allowed. For this reason, you can omit the `protocol` option from all rules. If you want to include it anyway, you must set the value to `tcp`, as shown in the first rule of the example.

## Finding domain names to allow

To help you identify the domains to include in your egress-filtering rules, use the following command to parse your server's `dns.log` file and show a list of all the DNS requests that your site has logged:

```shell
awk '($5 ~/query/)' /var/log/dns.log | awk '{print $6}' | sort | uniq -c | sort -rn
```

This command also shows DNS requests that were made but blocked by your egress-filtering rules. The output does not show which domains were blocked, only that requests were made. The output does not show requests made using an IP address.

```terminal
Example output:

97 magento.com
93 magentocommerce.com
88 google.com
70 metadata.google.internal.0
70 metadata.google.internal
65 newrelic.com
56 fastly.com
17 mcprod-0vunku5xn24ip.ap-4.magentosite.cloud
6 advancedreporting.rjmetrics.com
```

Domains, in contrast to IP addresses, are typically more specific and secure for egress filtering. For example, if you add an IP address for a service that uses a CDN, you are allowing the IP address for the CDN, which can be used by hundreds or thousands of other domains. With one IP address, you could be allowing outbound access to thousands of other servers.

## Testing egress-filtering rules

After collecting and configuring access rules for the domains and IP addresses your site needs, it is time to push and test.

To test your egress-filtering rules:

1. Create a shell script of `curl` commands to access the domains and IP addresses in your rules. Include commands that test access to domains and IP addresses that should be blocked.

1. Configure a `post_deploy` hook in your `.magento.app.yaml` file to run the script.

1. Push your `firewall` configuration and your test script to your `integration` branch.

1. Examine the `post_deploy` output from your `curl` commands.

1. Refine your `firewall` rules, update your `curl` script, commit, push, and repeat.

### `curl` script example

```shell
# curl-tests-for-egress-filtering.sh

# Use the -v option to display connection details

# Check domain access
curl -v newrelic.com
curl -v fastly.com
curl -v magento.com
curl -v magentocommerce.com
curl -v google.com
curl -v account.adobe.com
curl -v stock.adobe.com
curl -v console.adobe.io
curl -v braintreepayments.com
curl -v paypal.com
curl -v ups.com
curl -v usps.com
curl -v fedex.com
curl -v dhl.com
curl -v devdocs.magento.com

# Check domain denials
curl -v amazon.com
curl -v facebook.com
curl -v twitter.com

# IP address access
...

# IP address denials
...
```

### `post_deploy` example

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: "php ./vendor/bin/ece-tools run scenario/deploy.xml\n"
    post_deploy: |
        set -e
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
        echo "[$(date)] post-deploy hook end"
        ./curl-tests-for-egress-filtering.sh
        echo "[$(date)] curl finished"
```
