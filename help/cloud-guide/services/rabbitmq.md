---
title: Set up RabbitMQ service
description: Learn how to enable the RabbitMQ service to manage message queues for Adobe Commerce on cloud infrastructure.
---

# Set up [!DNL RabbitMQ] service

The [Message Queue Framework (MQF)](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) is a system within Adobe Commerce that allows a [module](https://glossary.magento.com/module) to publish messages to queues. It also defines the consumers that receive the messages asynchronously.

The MQF uses [RabbitMQ](https://www.rabbitmq.com/) as the messaging broker, which provides a scalable platform for sending and receiving messages. It also includes a mechanism for storing undelivered messages. [!DNL RabbitMQ] is based on the Advanced Message Queuing Protocol (AMQP) 0.9.1 specification.

>[!WARNING]
>
>If you prefer using an existing AMQP-based service, like [!DNL RabbitMQ], instead of relying on Adobe Commerce on cloud infrastructure to create it for you, use the [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) environment variable to connect it to your site.

{{service-instruction}}

**To enable RabbitMQ**:

1. Add the required name, type, and disk value (in MB) to the `.magento/services.yaml` file along with the installed RabbitMQ version.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configure the relationships in the `.magento.app.yaml` file.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. Add, commit, and push your code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [Verify the service relationships](services-yaml.md#service-relationships).

{{service-change-tip}}

## Connect to RabbitMQ for debugging

For debugging purposes, it is useful to directly connect to a service instance in one of the following ways:

- Connect from your local development environment
- Connect from the application
- Connect from your PHP application

### Connect from your local development environment

1. Log in to the `magento-cloud` CLI and project:

   ```bash
   magento-cloud login
   ```

1. Check out the environment with RabbitMQ installed and configured.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Use SSH to connect to the Cloud environment:

   ```bash
   magento-cloud ssh
   ```

1. Retrieve the RabbitMQ connection details and login credentials from the [$MAGENTO_CLOUD_RELATIONSHIPS](../application/properties.md#relationships) variable:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

      or

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In the response, find the RabbitMQ information, for example:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Enable local port forwarding to RabbitMQ.

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   An example for accessing the RabbitMQ management web interface at `http://localhost:15672` is:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. While the session is open, you can start a RabbitMQ client of your choice from your local workstation, configured to connect to the `localhost:<portnumber>` using the port number, username, and password information from the MAGENTO_CLOUD_RELATIONSHIPS variable.

### Connect from the application

To connect to RabbitMQ running in an application, install a client, such as [amqp-utils](https://github.com/dougbarth/amqp-utils), as a project dependency in your `.magento.app.yaml` file.

For example,

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

When you log in to your PHP container, you enter any `amqp-` command available to manage your queues.

### Connect from your PHP application

To connect to RabbitMQ using your PHP application, add a PHP [library](https://glossary.magento.com/library) to your source tree.
