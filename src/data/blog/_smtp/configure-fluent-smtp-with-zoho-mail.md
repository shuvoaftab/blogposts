---
author: Ibrahim Sharif
pubDatetime: 2022-05-11 20:40:00
modDatetime: null
title: Configure Fluent SMTP with Zoho Mail
description: A guide to configuring your Zoho email with FluentSMTP for WordPress email delivery.
tags:
  - FluentSMTP
  - WordPress
  - Email
  - Zoho
  - Workspace
  - SMTP
  - Email Deliverability
category: WordPress
featured: false
draft: false
---

The goal of this tutorial is to send emails from WordPress using your Personal Zoho Mail Email **_@zohomail.com_** by using the Fluent SMTP Plugin. If you have checked or reviewed my other article about [Configuring Gmail with Fluent SMTP](../configure-gmail-with-fluent-smtp/) you will find it easier to follow this guide.

## Table of Contents

## Prerequisites to Configure Fluent SMTP with Zoho Mail

In order to proceed, there are a few things that are needed beforehand to configure Fluent SMTP with Zoho Mail as below:

| Requirement                | Details                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------|
| **Zoho Mail Email Address** | An existing _you@zohomail.com_ email address with a Password.                                |
| **Administrative Permission** | WordPress Administrator Role-based user access.                                             |
| **Firewall Status**         | Port 465 Opened.                                                                             |
| **TLS Support**             | TLS v1.0, v1.1, v1.2, v1.3 support from the server where WordPress is hosted.                |

## Steps to Configure Fluent SMTP with Zoho Mail

1. Grab the Zoho Mail Email Address and its Password
2. Create a new Fluent SMTP Connection with Other Methods
3. Put necessary details and Save
4. Test the Connection

## Video Guide to Configure Fluent SMTP with Zoho Mail

https://youtu.be/4yQqelWMUOA

## The Procedure to Configure Fluent SMTP with Zoho Mail

### Grab the Zoho Mail Email Address

Let's assume our target Email Address to be configured is **ibrahim@zohomail.com** and its password: **I2X22AZ21**

![Zoho Mail dashboard screenshot](@/assets/images/posts/fluentsmtp/fluent_smtp_zohomail_dashboard.png)

### Create a new Fluent SMTP Connection

Now it's time to configure Fluent SMTP. Create a new SMTP Connection and the method is **Other**.

### Put necessary details

| Setting           | Value                                                                                   |
|-------------------|-----------------------------------------------------------------------------------------|
| **From Email**    | The Zoho Mail email address **ibrahim@zohomail.com**                                    |
| **From Name**     | The name you want to use. Example: **Ibrahim Sharif**                                   |
| **SMTP Host**     | smtp.zoho.com                                                                           |
| **SMTP Port**     | 465                                                                                     |
| **Encryption**    | SSL                                                                                     |
| **Auto TLS**      | Yes                                                                                     |
| **Authentication**| Yes. It's better to store the access keys in the database.                              |
| **SMTP Username** | The Zoho Mail email address **ibrahim@zohomail.com**                                    |
| **SMTP Password** | Email password: **I2X22AZ21**                                                           |

![Fluent SMTP Zoho Mail settings example](@/assets/images/posts/fluentsmtp/fluent_smtp_zohomail_settings.png)

### Test the Connection

Now it's time to test the connection if it's working or not! Go to Fluent SMTP > Email Test:  
\-> Use the From as your Zoho Mail email is just configured.  
\-> Send To where you want to receive the test email.  
\-> HTML should be turned on to avoid suspicious activity from Spam Filters.

![Fluent SMTP test email sent successfully (generic screenshot)](@/assets/images/posts/fluentsmtp/fluent_smtp_gmail_test_sent_success.png)

Now click Send Test Email and check the destination Email Address.

![Test email received from Zoho Mail via Fluent SMTP](@/assets/images/posts/fluentsmtp/fluent_smtp_zohomail_received.png)

In this case, the test email is received and we are done configuring the Zoho Mail Email address to send WordPress emails using the Fluent SMTP Plugin.

## Important Note

It is highly recommended to configure a cronjob replacing WordPress's Default PHP-based Cronjob to operate Email sending and other scheduled jobs smoothly.  
Some hosting may not allow running a cronjob below 5 Minutes. But it is still better than a PHP-Based cronjob.

Emails landing in Spam Folders depend on numerous factors including IP reputation, Domain reputation, and Email Body Content.
