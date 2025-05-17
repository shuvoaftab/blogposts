---
author: Ibrahim Sharif
pubDatetime: 2022-05-06 20:01:00
modDatetime: null
title: Configure Fluent SMTP with Yahoo
description: A guide to configuring your Yahoo email with FluentSMTP for WordPress email delivery.
tags:
  - FluentSMTP
  - WordPress
  - Email
  - Yahoo
  - SMTP
  - Email Deliverability
category: WordPress
featured: false
draft: false
---


The goal of this tutorial is to send emails from WordPress using your Personal Yahoo Email **you_@yahoo.com_** by using the Fluent SMTP Plugin. If you have checked or reviewed my other article about [Configuring Gmail with Fluent SMTP](../configure-gmail-with-fluent-smtp/) you will find it easier to follow this guide.

## Table of Contents

## Prerequisites to Configure Fluent SMTP with Yahoo

In order to proceed, there are a few things that are needed beforehand to configure Fluent SMTP with Yahoo as below:

| Requirement                | Description                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------|
| Yahoo Email Address        | An existing **_you@Yahoo.com_** email address.                                                |
| Yahoo App Password         | Generate an app password.                                                                     |
| Administrative Permission  | WordPress Administrator Role-based user access.                                               |
| Firewall Status            | Port 465 Opened.                                                                              |
| TLS Support                | TLS v1.0, v1.1, v1.2, v1.3 support from the server where WordPress is hosted.                 |

## Steps to Configure Fluent SMTP with Yahoo

1. Grab the Yahoo Email Address.
2. Generate an app password.
3. Create a new Fluent SMTP Connection with Other SMTP Methods.
4. Put the necessary details and Save.
5. Test the Connection.

## Video Guide to Configure Fluent SMTP with Yahoo

https://youtu.be/3JQPceUKkhw

## The Procedure to Configure Fluent SMTP with Yahoo

### Grab the Yahoo Email Address

Let's assume our target Email Address to be configured is **ibrahim@yahoo.com**.

![Yahoo Mail dashboard screenshot](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_dashboard.png)

### Generate an app password

Yahoo requires a different password rather than the account password like Gmail, Outlook, and Zoho Mail. Please visit: [https://login.yahoo.com/account/security#less-secure-apps](https://login.yahoo.com/account/security#less-secure-apps) and create a new app password which we will be using inside Fluent SMTP settings

**Click on Generate and Manage app passwords.**

![Yahoo generate app password page](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_generate_app_password.png)

**Give a name for the app. Here I used Fluent SMTP Guide**

![Naming Yahoo app password for Fluent SMTP](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_generate_app_password_name.png)

**Now copy the generated password.**

![Yahoo generated app password key](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_generate_app_password_key.png)

### Create a new Fluent SMTP Connection

Now it's time to configure Fluent SMTP. Create a new SMTP Connection and the method is **Other**.

### Put necessary details

| Setting           | Value/Description                                                      |
|-------------------|-----------------------------------------------------------------------|
| **From Email**    | The Yahoo email address **ibrahim@yahoo.com**                         |
| **From Name**     | The name you want to use (e.g., **Ibrahim Sharif**)                   |
| **SMTP Host**     | **smtp.mail.yahoo.com**                                               |
| **SMTP Port**     | **465**                                                               |
| **Encryption**    | **SSL**                                                               |
| **Auto TLS**      | Yes                                                                   |
| **Authentication**| Yes. It's better to store the access keys in the database.            |
| **SMTP Username** | The Yahoo email address **ibrahim@yahoo.com**                         |
| **SMTP Password** | The **generated app password** we created earlier.                    |

![Fluent SMTP Yahoo settings example](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_settings.png)

### Test the Connection

Now it's time to test the connection if it's working or not! Go to Fluent SMTP > Email Test:  
\-> Use the From as your Yahoo email is just configured.  
\-> Send To where you want to receive the test email.  
\-> HTML should be turned on to avoid suspicious activity by Spam Filters.

![Fluent SMTP test email sent successfully (generic screenshot)](@/assets/images/posts/fluentsmtp/fluent_smtp_gmail_test_sent_success.png)

Now click Send Test Email and check the destination Email Address.

![Test email received from Yahoo via Fluent SMTP](@/assets/images/posts/fluentsmtp/fluent_smtp_yahoo_received.png)

In this case, the test email is received and we are done configuring the Yahoo Email address to send WordPress emails using the Fluent SMTP Plugin.

## Important Note

It is highly recommended to configure a cronjob replacing WordPress's Default PHP-based Cronjob to operate Email sending and other scheduled jobs smoothly.  
Some hosting may not allow running a cronjob below 5 Minutes. But it is still better than a PHP-Based cronjob.

Emails landing in Spam Folders depend on numerous factors including IP reputation, Domain reputation, and Email Body Content.

<!-- * * * -->
