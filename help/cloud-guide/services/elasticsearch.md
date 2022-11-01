---
title: Set up Elasticsearch service
description: Learn how to enable the Elasticsearch service for Adobe Commerce on cloud infrastructure.
---

# Set up Elasticsearch service

[Elasticsearch](https://www.elastic.co) is an open-source product that enables you to take data from any source, any format, and search and visualize it in real time.

{{elasticsearch-support}}

For Adobe Commerce version 2.4.4 and later, see [Set up OpenSearch service](opensearch.md).

- Elasticsearch performs quick and advanced searches on products in the product catalog
- Elasticsearch Analyzers support multiple languages
- Supports stop words and synonyms
- Indexing does not impact customers until the reindex operation completes

>[!TIP]
>
>Adobe recommends that you always set up Elasticsearch for your Adobe Commerce on cloud infrastructure project even if you plan to configure a third-party search tool for your Adobe Commerce application. Setting up Elasticsearch provides a fallback option in case the third-party search tool fails.

{{service-instruction}}

**To enable Elasticsearch**:

1. For Starter projects, add the `elasticsearch` service to the `.magento/services.yaml` file with the Elasticsearch version and allocated disk space in MB.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   For Pro projects, you must submit an Adobe Commerce Support ticket to change the Elasticsearch version in the Staging and Production environments.

1. Set the `relationships` property in the `.magento.app.yaml` file.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Add, commit, and push code changes.

   ```bash
   git add -A && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   For information on how these changes affect your environments, see [Services](services-yaml.md).

1. [Verify the service relationships](services-yaml.md#service-relationships) and configure Elasticsearch in the Admin UI.

1. Reindex the Catalog Search index.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Clean the cache.

   ```bash
   bin/magento cache:clean
   ```

{{change-service-version}}

## Elasticsearch software compatibility

When you install or upgrade your Adobe Commerce on cloud infrastructure project, always check for compatibility between the Elasticsearch service version and the [Elasticsearch PHP](https://github.com/elastic/elasticsearch-php) client for Adobe Commerce.

-  **First time setup**–Confirm that the Elasticsearch version specified in the `services.yaml` file is compatible with the Elasticsearch PHP client configured for Adobe Commerce.

-  **Project upgrade**–Verify that the Elasticsearch PHP client in the new application version is compatible with the Elasticsearch service version installed on the Cloud infrastructure.

Service version and compatibility support for Adobe Commerce on cloud infrastructure is determined by versions deployed on the Cloud infrastructure, and sometimes differ from versions supported by Adobe Commerce on-premises deployments. See [Service versions](services-yaml.md#service-versions).

**To check Elasticsearch software compatibility**:

1. Use SSH to log in to the remote environment.

1. Check the Composer package version for `elasticsearch/elasticsearch`.

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   In the response, check the installed version in the `versions` property.

   ```terminal
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v6.7.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org    licensesApache-2.0.html#licenseText
   source   : [git] https://github.com/elastic    elasticsearch-php.git7be453dd36d1b141b779f2cb956715f8e04ac2f4
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/     7be453dd36d1b141b779f2cb956715f8e04ac2f4 7be453dd36d1b141b779f2cb956715f8e04ac2f4
   path     : /app/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   Also, you can find the Elasticsearch PHP client version in the  `composer.lock` file in the environment root directory.

1. From the command line, retrieve the Elasticsearch service connection details.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In the response, find the IP address for the Elasticsearch service endpoint:

   ```terminal
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. Retrieve the installed Elasticsearch service `version:number` from the service endpoint.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```terminal
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Check version compatibility between the Elasticsearch service and the PHP client.

   If the versions are incompatible, make one of the following updates to your environment configuration:

   -  Change the Elasticsearch PHP client to a version that is compatible with the Elasticsearch service version.

      ```bash
      composer require "elasticsearch/elasticsearch:~<version>"
      ```

   -  Change the Elasticsearch service version in the `services.yaml` file to a version that is compatible with the Elasticsearch PHP client.

      {{pro-update-service}}

## Restart the Elasticsearch service

If you need to restart the [Elasticsearch](https://www.elastic.co) service, you must contact Adobe Commerce support.

## Additional search configuration

-  By default, the search configuration for Cloud environments regenerates each time you deploy. You can use the `SEARCH_CONFIGURATION` deploy variable to retain custom search settings between deployments. See [Deploy variables](../environment/variables-deploy.md#search_configuration).

-  After you set up the Elasticsearch service for your project, use the Admin UI to test the Elasticsearch connection and customize Elasticsearch settings for Adobe Commerce.

### Add plugins for Elasticsearch

Optionally, you can add plugins for Elasticsearch by adding the `configuration:plugins` section to the Elasticsearch service in the `.magento/services.yaml` file. For example, the following code enables the ICU analysis and Phonetic analysis plugins.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

If you use the ElasticSuite third-party plugin, you must [update the `ece-tools` package](../dev-tools/update-package.md) to version 2002.0.19 or later.
When setting up ElasticSuite, add the configuration settings to the `ELASTICSUITE_CONFIGURATION` deploy variable. This configuration saves the settings across deployments.

### Remove plugins for Elasticsearch

Removing the plugin entries from `elasticsearch:` in `.magento/services.yaml` does not uninstall or disable them as you might expect. You must reindex your Elasticsearch data. This behavior is intentional to prevent possible loss or corruption of data that depends on these plugins.

**To remove Elasticsearch plugins**:

1. Remove the Elasticsearch plugin entries from your `.magento/services.yaml` file.
1. Add, commit, and push your code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Commit the `.magento/services.yaml` changes to your Cloud repo.
1. Reindex the Catalog Search index:

    ```bash
    bin/magento indexer:reindex catalogsearch_fulltext
    ```

1. Clean the cache:

    ```bash
    bin/magento cache:clean
    ```

>[!TIP]
>
>For details on using or troubleshooting the Elasticsuite plugin with Adobe Commerce, see the [Elasticsuite documentation](https://github.com/Smile-SA/elasticsuite).

## Troubleshooting

See the following Adobe Commerce Support articles for help with troubleshooting Elasticsearch problems:

-  [Elasticsearch 5 is configured, but search page does not load with "Fielddata is disabled..." error](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-5-is-configured-but-search-page-does-not-load-with-fielddata-is-disabled...-error.html)
-  [Catalog pagination doesn't work when Elasticsearch 6.x is used](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/catalog-pagination-doesn-t-work-when-elasticsearch-6.x-is-used.html)
-  [Elasticsearch in Adobe Commerce troubleshooter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-in-magento-troubleshooter.html)
-  [Elasticsearch Index Status is `yellow` or `red`](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/elasticsearch/elasticsearch-index-status-is-yellow-or-red.html)
