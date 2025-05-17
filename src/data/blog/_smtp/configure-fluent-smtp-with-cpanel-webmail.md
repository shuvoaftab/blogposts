---
author: Ibrahim Sharif
pubDatetime: 2022-05-07 05:00:00
modDatetime: null
title: Configure Fluent SMTP with cPanel Webmail
description: A guide to configuring your cPanel Webmail (Roundcube) with FluentSMTP for WordPress email delivery.
tags:
  - FluentSMTP
  - WordPress
  - Email
  - cPanel
  - Webmail
  - Roundcube
  - SMTP
  - Email Deliverability
category: WordPress
featured: false
draft: false
---

cPanel is the most popular and widely used control panel for web hosting on the web. cPanel uses Postfix and Exim to receive and as a Mail Transfer Agent.  
The goal of this tutorial is to send emails from WordPress using your Personal Domain Email **you@yourdomain.com** by using the Fluent SMTP Plugin. If you have checked or reviewed my other article about [Configuring Gmail with Fluent SMTP](../configure-gmail-with-fluent-smtp/) you will find it easier to follow this guide.

## Table of Contents

## Prerequisites to Configure Fluent SMTP with cPanel Webmail

In order to proceed, there are a few things that are needed beforehand to configure Fluent SMTP with cPanel Webmail as below:

| Requirement                | Description                                                                                      |
|----------------------------|--------------------------------------------------------------------------------------------------|
| **Email Address**          | An existing **_you@yourdomain.com_** email address and a password.                               |
| **cPanel Email Access**    | Sufficient permissions for accessing Emails.                                                     |
| **Administrative Permission** | WordPress Administrator role-based user access.                                               |
| **Firewall Status**        | Commonly used ports 25, 26, 465, 587 opened as needed.                                          |
| **TLS Support**            | TLS v1.0, v1.1, v1.2, v1.3 support from the server where WordPress is hosted.                   |

## Steps To Configure Fluent SMTP With CPanel Webmail

1. Grab the **Email Address** and the **password** and Check Emails from Roundcube Email Client.
2. Get the **SMTP** details from **Connect Devices** page.
3. Create a new Fluent SMTP Connection with **Other SMTP** Methods.
4. Put the necessary details and Save.
5. Test the Connection.
6. Extra Bonus: Manually check the **Outgoing Server** or **SMTP Host**.

## The Procedure To Configure Fluent SMTP With CPanel Webmail

### Check Emails from Roundcube Email Client

Let's assume our target Email Address to be configured is **ibrahim@ibrahim.com**.  
Go to **Email** \> **Email Accounts**

![cPanel email dashboard showing email accounts](@/assets/images/posts/fluentsmtp/cpanel_email_dashboard-shuvoaftab.png)

Select your Email Account & Click on **Check Email**

![cPanel email accounts list](@/assets/images/posts/fluentsmtp/cpanel_email_accounts-shuvoaftab.png)

Select **Roundcube** as the default Email Client

![Select Roundcube as default email client in cPanel](@/assets/images/posts/fluentsmtp/cpanel_email_accounts_roundcube-shuvoaftab.png)

This is the Email Client Dashboard for all your Emails to check from cPanel.

![Roundcube email client dashboard in cPanel](@/assets/images/posts/fluentsmtp/cpanel_email_accounts_roundcube_dashboard-shuvoaftab.png)

### Get the SMTP details

The most important part of this tutorial is to get the correct SMTP details in order to connect from Fluent SMTP to the cPanel Email Server. Please Go to **Email** > **Email Accounts** > Select your Email Account & Click on **Connect Devices**. There you will find 2 categories of information which are SSL and Non-SSL connections. Keep this information for configuration details of Fluent SMTP.

![cPanel connect devices page showing SMTP details](@/assets/images/posts/fluentsmtp/cpanel_email_connect_devices-shuvoaftab.png)

### Create a new Fluent SMTP Connection

Now it's time to configure Fluent SMTP. Create a new SMTP Connection and the method is the **Other** **SMTP.** Please keep in mind that these details vary from one server to another and from one hosting company to another company. I have used what I got from the test cPanel server.

If your Domain has a mail.domain.com DNS published according to the cPanel Zone, you may use directly this mail.domain.com as SMTP Host. And if that hostname has an SSL certificate issued you can use the most commonly used port 465 and SSL Protocol in SMTP settings. Otherwise, you will have to use a Non-SSL connection and ports like 25,26,2525,2526 which are provided by your hosting server. You should consult your hosting provider for more accurate details for this when you configure your domain.

### Keypoints of necessary details

| Setting           | Value/Description                                                                                   |
|-------------------|----------------------------------------------------------------------------------------------------|
| **From Email**    | The email address **ibrahim@ibrahim.com**                                                          |
| **From Name**     | The name you want to use (e.g., **Ibrahim Sharif**)                                                |
| **SMTP Host**     | In this example: **premium43.web-hosting.com**                                                     |
| **SMTP Port**     | **465**, **25**, **26**, or **587**                                                                |
| **Encryption**    | **SSL**, **TLS**, or **None**                                                                      |
| **Auto TLS**      | **Yes**                                                                                            |
| **Authentication**| Yes. It's better to store the access keys in the database.                                         |
| **SMTP Username** | The cPanel Webmail email address (**ibrahim@ibrahim.com**)                                         |
| **SMTP Password** | The **password** set when the email address was created in cPanel                                  |


![Fluent SMTP settings example for cPanel webmail](@/assets/images/posts/fluentsmtp/cpanel_webmail_Fluent_SMTP_settings-shuvoaftab.png)

### Test the Connection

Now it's time to test the connection if it's working or not! Go to Fluent SMTP > Email Test:  
\-> Use the From as your cPanel webmail email just configured.  
\-> Send To where you want to receive the test email.  
\-> HTML should be turned on to avoid suspicious activity by Spam Filters.

![Fluent SMTP email test sent successfully](@/assets/images/posts/fluentsmtp/Fluent_SMTP_email_test_successfully_sent.png)

Now click Send Test Email and check the destination Email Address.

![Test email received from cPanel webmail via Fluent SMTP](@/assets/images/posts/fluentsmtp/cpanel_email_received-shuvoaftab.png)

In this case, the test email is received and we are done configuring the cPanel Webmail Email address to send WordPress emails using the Fluent SMTP Plugin.

## Bonus: Manually check the **Outgoing Server** or **SMTP Host**

In case you find sometimes that using your domain as SMTP Host does not work, you need to manually find the Hostname your cPanel server is using. To do this please send an email to your own Gmail or by default cPanel sends a welcome email to each webmail which you can check for this step.

![Expand SMTP host details in cPanel email](@/assets/images/posts/fluentsmtp/cpanel_email_bonus_check_SMTP_host_expand-shuvoaftab.png)

Click on **More Details** and then **All Headers**. Now we need to check the **Received From** field from the source as below:

![View all headers to find SMTP host in cPanel email](@/assets/images/posts/fluentsmtp/cpanel_email_bonus_check_SMTP_host-shuvoaftab.png)

Use this hostname in Fluent SMTP as SMTP Host. Sometimes using only a Non-SSL connection works because of the hosting server's misconfiguration about SSL. If you need further help you may contact me for assistance.

## Important Note

It is highly recommended to configure a cronjob replacing WordPress's Default PHP-based Cronjob to operate Email sending and other scheduled jobs smoothly.  
Some hosting may not allow running a cronjob below 5 Minutes. But it is still better than a PHP-Based cronjob.

Emails landing in Spam Folders depend on numerous factors including IP reputation, Domain reputation, and Email Body Content.
