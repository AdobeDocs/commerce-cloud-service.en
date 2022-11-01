---
title: Set up OpenSearch service
description: Learn how to enable the OpenSearch service for Adobe Commerce on cloud infrastructure.
---

# Set up OpenSearch service

The [OpenSearch](https://www.opensearch.org) service is an open-source fork of Elasticsearch 7.10.2, following the licensing changes for Elasticsearch. See [System requirements](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) for a list of supported versions.

{{elasticsearch-support}}

OpenSearch enables you to take data from any source, any format, and search and visualize it in real time.

- Quick and advanced searches on products in the product catalog
- Elasticsearch Analyzers support multiple languages
- Supports stop words and synonyms
- Indexing does not impact customers until the reindex operation completes

{{service-instruction}}

>[!TIP]
>
>Adobe recommends that you always set up OpenSearch for your Adobe Commerce on cloud infrastructure project even if you plan to configure a third-party search tool for your Adobe Commerce application. Setting up OpenSearch provides a fallback option if the third-party search tool fails.

**To enable OpenSearch**:

1. For Starter projects, add the `opensearch` service to the `.magento/services.yaml` file with the appropriate version and allocated disk space in MB.

   ```yaml
   opensearch:
       type: opensearch:<version>
       disk: 1024
   ```

   For Pro projects, you must submit a [Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to change the OpenSearch version in the Staging and Production environments.

1. Set the `relationships` property in the `.magento.app.yaml` file.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Add, commit, and push code changes.

   ```bash
   git add -A && git commit -m "Enable OpenSearch" && git push origin <branch-name>
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

{{change-service-version}}
