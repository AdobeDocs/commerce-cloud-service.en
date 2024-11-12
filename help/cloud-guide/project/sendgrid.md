---
title: SendGrid email service
description: Learn about the SendGrid email service for Adobe Commerce on cloud infrastructure and how you can test your DNS configuration.
exl-id: 30d3c780-603d-4cde-ab65-44f73c04f34d
---
# SendGrid email service

The SendGrid Simple Mail Transfer Protocol (SMTP) proxy service provides outbound email authentication and reputation monitoring services, including support for:

* All outbound transactional emails
* Dedicated IP addresses
* Domain registration, DomainKeys Identified Mail (DKIM) signatures for email domain validation (for Pro Staging and Production environments only)
* Custom domain registration (for Pro only)
* Automated integration for Starter and Pro integration environments. Pro Production and Staging environments require manual provisioning and configuration during the Infrastructure as a Service (IaaS) hardware provisioning process

The SendGrid SMTP proxy is not intended for use as a general-purpose email server to receive incoming email or for use with email marketing campaigns.

>[!TIP]
>
>Make sure that you have configured the appropriate store email addresses in the Admin by going to Stores > Configuration > General to avoid issues with deliverability and domain verification. You must uncheck **[!UICONTROL Use Default]** and replace the default values with a domain that you own. Public/shared-domain email services, such as gmail.com and outlook.com, should not be configured as the sender email address when sending emails through Sendgrid.

## Enable or disable email

You can enable or disable outgoing emails for each environment from the Cloud Console or from the command line.

By default, outgoing emails are enabled on Pro Production and Staging environments. However, [!UICONTROL Outgoing emails] may appear disabled in the environment settings until you set the `enable_smtp` property through the [command line](outgoing-emails.md#enable-emails-in-the-cli) or [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console). You can enable outgoing emails for integration and staging environments to send two-factor authentication or reset password emails for Cloud project users. See [Configure emails for testing](outgoing-emails.md).

If outgoing emails must be disabled or re-enabled on Pro Production or Staging environments, you can submit an [Adobe Commerce Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

>[!TIP]
>
>Updating the [!UICONTROL enable_smtp] property value by [command line](outgoing-emails.md#enable-emails-in-the-cli) also changes the [!UICONTROL Enable outgoing emails] setting value for this environment on the [Cloud Console](outgoing-emails.md#enable-emails-in-the-cloud-console).

## SendGrid dashboard

All Cloud projects are managed under a central account, so only Support has access to the SendGrid dashboard. SendGrid does not provide subaccount restriction features.

To review the Activity logs for delivery status or a list of bounced, rejected, or blocked email addresses, [submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket). The Support team **cannot** retrieve activity logs older than 30 days.

If possible, include the following information with your request:

* the affected email address or addresses
* the timeframe in question (within the past 30 days only)
* the subject of the email

## DomainKeys Identified Mail (DKIM)

DKIM is an email authentication technology that enables Internet Service Providers (ISPs) to identify both legitimate and fake sender addresses, a technique commonly used in phishing and email scams. DKIM relies on a domain owner managing the DNS records. When using DKIM, the sender server uses a private key to sign the messages. Also, the domain owner adds a DKIM record, which is a modified `TXT` record, to the sender-domain's DNS records. This `TXT` record contains a public key that recipient mail servers use to verify the signature of a message. The DKIM public-key cryptography procedure enables recipients to verify the authenticity of a sender. See [DKIM Records Explained](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>The SendGrid DKIM signatures and domain authentication support are only available on the Production and Staging environments for Pro projects, but not for all Starter environments. As a result, outbound transactional emails are likely to be flagged by spam filters. Using DKIM improves the delivery rate as an authenticated email sender. To improve the message delivery rate, you can upgrade from Starter to Pro or use your own SMTP server or email delivery service provider. See [Configure email connections](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/communications/email-communications) in the _Admin Systems guide_.

### Sender and domain authentication

For SendGrid to send transactional emails on your behalf from Pro Production or Staging environments, you must configure your DNS settings to include the three SendGrid subdomain DNS entries. Each SendGrid account is assigned a unique `TXT` record which is used to authenticate outbound emails.

>[!TIP]
>
>Make sure that you configure the **[!UICONTROLStore Email Addresses]** with the proper domain in **[!UICONTROL Stores > Configuration > General > Store Email Addresses]**. The domain authentication is performed on the sender's email address. If the default setting (`example.com`) is configured, the emails from `example.com` would be blocked by Sendgrid.

**To enable domain authentication**:

1. Submit a [support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) to request enabling DKIM for a specific domain (**Pro Staging and Production environments only**).
1. Update your DNS configuration with the `TXT` and `CNAME` records provided to you in the support ticket.

**Example `TXT` record with account ID**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Example `CNAME` records**:

| Domain     | Points To  | Record Type   |
| ---------- | ---------- | ------------- |
| em.emaildomain.com  | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM signatures and automated security

You can select between automated and manual security when setting up an authenticated domain. If you choose automated security, SendGrid manages your DKIM and SPF records automatically. When you add a new dedicated sending IP address to your account, SendGrid updates your DNS settings and DKIM signature immediately. If you turn off automated security, you are responsible for updating your DKIM signature anytime you change your sending domain.

**Example automated security enabled**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Example automated security disabled**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

After domain authentication is set up, SendGrid automatically handles Security Policy Framework (SPF) and DKIM records for you. After SendGrid provides the `CNAME` records to add to your DNS records, you can add dedicated IP addresses and make other account updates without having to manage your SPF records manually. See [Automated Security and Your DKIM Signature](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

To test your DNS configuration:

```
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Transactional email threshold

The transactional email threshold refers to the number of transactional email messages that you can send from Pro environments within a specific time period, such as 12,000 emails per month from non-production environments. The threshold is designed to protect against sending spam and potentially damaging your email reputation.

There are no hard limits on the number of emails that can be sent in the Production environment, as long as the Sender Reputation score is over 95%. The reputation is affected by the number of bounced or rejected emails and whether DNS-based spam registries have flagged your domain as a potential spam source. See [Emails not sent when SendGrid credits exceeded on Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) in the _Commerce Support Knowledge Base_.

**To check if maximum credits are exceeded**:

1. On your local workstation, change to your project directory.

1. Use SSH to log in to the remote environment.

   ```bash
   magento-cloud ssh
   ```

1. Check the `/var/log/mail.log` for `authentication failed : Maxium credits exceeded` entries.

   If you see any `authentication failed` log entries and the **Email sending reputation** is at a minimum of 95, you can [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) to request a credit allotment increase.

### Email sending reputation

An email sending reputation is a score assigned by an Internet Service Provider (ISP) to a company sending email messages. The higher the score, the more likely an ISP is to deliver messages to a recipient's inbox. If the score falls below a certain level, the ISP may route messages to recipients' spam folder, or even reject messages completely. The reputation score is determined by several factors such as a 30-day average of your IP addresses rank against other IP addresses and spam complaint rate. See [8 Ways to Check Your Email Sending Reputation](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation).

### Email suppression lists

An email suppression list is a list of recipients that emails should not be sent to if doing so would hurt your sending reputation and delivery rates. It is required by the CAN-SPAM Act to ensure that email senders have a method of opting-out recipients who unsubscribed or marked email as spam. The suppression list also collects emails that bounce, are blocked, or invalid. 

To prevent emails from being sent to the spam folder in the first place, follow Sendgrid's best practices article, [Why Are My Emails Going to Spam?](https://sendgrid.com/en-us/blog/10-tips-to-keep-email-out-of-the-spam-folder).

If some recipients are not receiving your emails, you can [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) to request a review of the suppression lists and remove the recipient(s) if necessary.

For more details, refer to [What Is a Suppression List?](https://sendgrid.com/en-us/blog/what-is-a-suppression-list)
