---
title: Set up OpenSearch service
description: Learn how to enable the OpenSearch service for Adobe Commerce on cloud infrastructure.
exl-id: 10dc6367-3f90-4ab6-a84e-15e8c3b32a38
---
# Set up OpenSearch service

The [OpenSearch](https://www.opensearch.org) service is an open-source fork of Elasticsearch 7.10.2, following the licensing changes for Elasticsearch. See the [OpenSource Project](https://github.com/opensearch-project) in GitHub.

{{elasticsearch-support}}

OpenSearch enables you to take data from any source, any format, and search and visualize it in real time.

- Quick and advanced searches on products in the product catalog
- OpenSearch Analyzers support multiple languages
- Supports stop words and synonyms
- Indexing does not impact customers until the reindex operation completes

{{service-instruction}}

>[!TIP]
>
>Adobe recommends that you always set up OpenSearch for your Adobe Commerce on cloud infrastructure project even if you plan to configure a third-party search tool for your Adobe Commerce application. Setting up OpenSearch provides a fallback option if the third-party search tool fails.

**To enable OpenSearch**:

1. For Starter projects, add the `opensearch` service to the `.magento/services.yaml` file with the appropriate version and allocated disk space in MB. In this case, version 2 is appropriate. The minor version is not required because cloud infrastructure uses the latest version of OpenSearch.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   For Pro projects, you must [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to change the OpenSearch version in the Staging and Production environments.

1. Set the `relationships` property in the `.magento.app.yaml` file.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Add, commit, and push code changes.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable OpenSearch" && git push origin <branch-name>
   ```

   For information on how these changes affect your environments, see [Services](services-yaml.md).

1. [Verify the service relationships](services-yaml.md#service-relationships) and configure OpenSearch in the Admin UI.

1. Reindex the Catalog Search index.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Clean the cache.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## OpenSearch software compatibility

When you install or upgrade your Adobe Commerce on cloud infrastructure project, always check for compatibility between the OpenSearch service version and the [OpenSearch PHP](https://github.com/opensearch-project/opensearch-php) client for Adobe Commerce.

- **First time setup**–Confirm that the OpenSearch version specified in the `services.yaml` file is compatible with the OpenSearch PHP client configured for Adobe Commerce.

- **Project upgrade**–Verify that the OpenSearch PHP client in the new application version is compatible with the OpenSearch service version installed on the cloud infrastructure.

Service version and compatibility support is determined by versions tested and deployed on the Cloud infrastructure, and sometimes differ from versions supported by Adobe Commerce on-premises deployments. See [System requirements](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in the _Installation Guide_ for a list of supported versions.

**To verify OpenSearch software compatibility**:

1. On your local workstation, change to your project directory.
1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Retrieve the OpenSearch service connection details.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In the response, find the IP address and port for the OpenSearch service endpoint:

   ```terminal
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. Retrieve the installed OpenSearch service `version:number` from the service endpoint.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```terminal
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## Restart the OpenSearch service

If you need to restart the OpenSearch service, you must contact Adobe Commerce support.

## Additional search configuration

- By default, the search configuration for Cloud environments regenerates each time you deploy. You can use the `SEARCH_CONFIGURATION` deploy variable to retain custom search settings between deployments. See [Deploy variables](../environment/variables-deploy.md#search_configuration).

- After you set up the OpenSearch service for your project, use the Admin UI to test the OpenSearch connection and customize OpenSearch settings for Adobe Commerce.

### Add plugins for OpenSearch

Optionally, you can add plugins for OpenSearch by adding the `configuration:plugins` section to the OpenSearch service in the `.magento/services.yaml` file. For example, the following code enables the ICU analysis and Phonetic analysis plugins.

```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

See the [OpenSearch Project](https://github.com/opensearch-project) for more information on plugins.

### Remove plugins for OpenSearch

Removing the plugin entries from the `opensearch:` section of the `.magento/services.yaml` file does **not** uninstall or disable the service. To fully disable the service, you must reindex your OpenSearch data after removing the plugins from your `.magento/services.yaml` file. This design prevents the possible loss or corruption of data that depends on these plugins.

**To remove OpenSearch plugins**:

1. Remove the OpenSearch plugin entries from your `.magento/services.yaml` file.
1. Add, commit, and push your code changes.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Commit the `.magento/services.yaml` changes to your cloud repository.
1. Reindex the Catalog Search index.

    ```bash
    bin/magento indexer:reindex catalogsearch_fulltext
    ```

1. Clean the cache.

    ```bash
    bin/magento cache:clean
    ```
