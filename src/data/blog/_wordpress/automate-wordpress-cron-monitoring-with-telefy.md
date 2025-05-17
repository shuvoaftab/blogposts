---
author: Ibrahim Sharif
pubDatetime: 2025-05-14 13:00:00
modDatetime: null
title: "Automate WordPress Cron Monitoring with Telefy: A Server-Side Guide"
description: A guide on using telefy package for failed cron events.
tags:
  - cron
  - wordpress
  - server
  - telefy
  - telegram
  - npm
category: WordPress
featured: false
draft: false
---

WordPress relies heavily on scheduled tasks to run operations like publishing scheduled posts, sending emails, or clearing expired transients. By default, it uses a built-in pseudo-cron system (`wp-cron.php`) that is triggered by on-site visits. This behavior is unreliable, especially for low-traffic or high-performance sites. To achieve more dependable results, it's best to shift to **real server-side cron jobs**.

In this guide, you'll learn:

- Why server-side cron is essential for WordPress.
- How to set up server-side cron.
- How to monitor cron results using **Telefy**, a command-line tool for sending Telegram alerts.

## Table of Contents

---

## Why Use Server-Side Cron Instead of WordPress Default Cron?

By default, WordPress executes `wp-cron.php` on every page load, which:

- Can fail silently if there's no traffic.
- May cause performance issues under high load.
- Lacks visibility when something goes wrong.

**Server-side cron advantages:**

- Guaranteed execution on schedule.
- Better performance control.
- Easier logging and debugging.

---

## What is Telefy?

[**Telefy**](www.npmjs.com/package/telefy) is a CLI tool that sends messages to your Telegram channel(s). You can:

- Send alerts to multiple channels.
- Use Markdown, HTML, or MarkdownV2 parse modes.
- Attach inline buttons.
- Combine with cron jobs or scripts for real-time error notification.

### **Features**

- 📤 **Simple API**: Easy-to-use functions for sending Telegram messages
- 🔘 **Inline Buttons**: Support for adding clickable inline URL buttons
- 📝 **Markdown Support**: Format messages with Markdown, HTML, or MarkdownV2
- 💻 **CLI Tool**: Send messages directly from your command line with intuitive options
- 🌐 **Multi-Channel Support**: Configure and send to multiple Telegram channels
- 📢 **Broadcast Mode**: Send to all configured channels at once with `--all` option
- 🚀 **Promise-based**: Modern async/await and Promise support
- 🛡️ **Error Handling**: Detailed error messages with helpful suggestions
- ⚙️ **Environment Variables**: Secure configuration using .env files
- 🎨 **Raw Mode**: Optional MarkdownV2 formatting without automatic escaping

### **Prerequisites**

Before using this package, you'll need:

1.  A **Telegram Bot Token** (get one from [**@BotFather**](https://t.me/BotFather))
2.  **Your Chat ID** (use [@userinfobot](https://t.me/userinfobot) or [@get_id_bot](https://t.me/get_id_bot))
3.  **Node.js** version 18.0.0 or higher

### **Installation**

```bash
# Global installation for CLI usage
npm install -g telefy
```

For Mac users, you may need to configure the .env file under `/opt/homebrew/lib/node_modules/telefy`

### **Configuration**

Create a `.env` file in your project root with one or more channel configurations:

```env
# Single channel configuration
CHANNEL_NEWS_TOKEN=your_bot_token_here
CHANNEL_NEWS_CHAT_ID=your_chat_id_here

# Multiple channel configuration
CHANNEL_ALERTS_TOKEN=another_bot_token_here
CHANNEL_ALERTS_CHAT_ID=another_chat_id_here
```

### **Obtaining Telegram Credentials**

1.  **Bot Token:**

    - Open Telegram and message [@BotFather](https://t.me/BotFather)
    - Send `/start`, then `/newbot`
    - Follow the prompts to name your bot and receive a token

2.  **Chat ID:**

    - Start a chat with your bot
    - Send a message to your bot
    - Visit `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates` in your browser
    - Find the chat ID in the JSON response under `"chat":{"id":<CHAT_ID>}`

It's perfect for DevOps, WordPress admins, or developers looking to stay informed about automated scripts or issues in production.

Learn more about telefy from the [**npm repository**](www.npmjs.com/package/telefy).

---

## Monitor `wp-cron.php` Execution via Telefy

In this example, we'll run the WordPress cron manually and send any output (typically errors or warnings) directly to a Telegram channel using Telefy.

### Step 1: Prepare the Shell Script

Create a file named `telefy_cron.sh`:

```bash
#!/bin/bash

# Define your PHP binary path and the WordPress wp-cron.php file
php_bin="/usr/bin/php"
wp_cron="/Users/shuvoaftab/Sites/fluentinfo/wp-cron.php"

# Run the cron job and capture the output
output=$($php_bin $wp_cron 2>&1)

# Send message only if there is any output
if [ -n "$output" ]; then
  telefy "$output" --channel alerts --parse-mode markdown
fi
```

You can get the WordPress path from your dashboard. Please go to **Tools** ⮕ **Site Health** ⮕ **Info.** Then get the path from the **Directories and Sizes** section as shown in the screenshot below:

![Get WordPress Directory Path](@/assets/images/posts/get_wp_path.png)

Make the cron script executable:

```bash
chmod +x /path/to/telefy_cron.sh
```

### Step 2: Schedule via Crontab

Open your crontab:

```bash
crontab -e
```

Add the following line to execute the script every minute:

```bash
* * * * * /path/to/telefy_cron.sh
```

### Step 3: Configure Telefy

Ensure your `.env` file contains channel configuration:

```env
CHANNEL_ALERTS_TOKEN=your_bot_token
CHANNEL_ALERTS_CHAT_ID=your_channel_id
```

For usage, simply run:

```bash
telefy "Test Message" --channel alerts
```

---

## Benefits of This Setup

- **Real-time error reporting**: See `wp-cron.php` issues as they happen.
- **Silent success**: No output = no message. Keeps things noise-free.
- **Multi-environment compatible**: Use different PHP paths or cron files.
- **Secure and minimal**: Only messages with content are sent.

---

## Final Thoughts

Server-side cron jobs are a best practice for serious WordPress sites, and coupling them with a tool like **Telefy** ensures you're not left in the dark if something fails. With just a few lines of code and a scheduled cron job, you can set up lightweight, real-time monitoring directly in your Telegram inbox.

Stay alert. Stay efficient. Use Telefy.
