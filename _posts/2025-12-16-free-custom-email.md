---
layout: post
title: A 12-year-old's guide to free custom emails
author: Arslaan Pathan
image: /assets/images/post-image/free-custom-email.jpg
---

Are you a small business looking for a custom email?  
A software developer wanting a more professional inbox?  
Or just a hobbyist flexing their custom email to friends?

If so, this article is for **you!**

I'm Arslaan Pathan, and as of 2025, I'm 12 years old.

Today, you'll learn exactly how to make your business email **completely free** — no payment required!

If a 12-year-old can do it, then you definitely can too.

*(Note: This does require you to have a domain name. It might work with a shared subdomain from FreeDNS or DuckDNS, but your mileage may vary.)*

This guide will be primarily focusing on Cloudflare Email Routing + Gmail SMTP.
If you want to use another provider or different services, please refer to another article.

## Step 1: Receiving emails

The first step in creating a custom business email is receiving emails.  
This guide assumes you are using Cloudflare nameservers with your domain.
If not, please follow [this guide.](https://developers.cloudflare.com/dns/zone-setups/full-setup/setup/){: target="_blank" }

1. Open the Cloudflare dashboard and select your domain if you haven't already.

2. On the left sidebar, click on `Email`, then `Email Routing`.

3. It should bring you to a `Getting started with Email Routing` page.

4. Enter the desired custom address in the `Custom address` field.

5. Enter the desired destination email (in this case, your current email) in the `Destination` field.  
    It may take you through to another page that makes you verify the destination email, but simply follow the steps and you should be good to go.

6. Press `Continue`.

7. Make sure email routing is enabled and add other desired addresses if you would like.

Done! You've setup email routing so you can receive emails in your normal Gmail inbox. It wasn't that hard, right?

## Step 2: Sending emails

Now comes the tricky part, sending emails. Don't leave just yet --- it isn't very hard, just a bit more complicated compared to receiving emails.

### 1. Create a Google App Password

First, you need to create a Google App Password so we can login to Gmail SMTP without being blocked by 2-Factor Authentication.

To create an app password for Gmail, go to [this link](https://security.google.com/settings/security/apppasswords).

Give it a memorable name, generate the app password, and store it in a safe place.

### 2. Add your Cloudflare Email as an alias in Gmail

In Gmail, press the Settings icon and click on `See All Settings`.

From there, go to `Accounts and Import` -> `Add another email address`.

In the first field that shows up, type your desired Cloudflare email address that you setup in the `Receiving emails` section.
Check the `Treat as an alias` box, and press `Next`.

It will now ask you to setup an SMTP server.  
Enter the following configuration:
- **SMTP Server**: `smtp.gmail.com`
- **Port**: `587`
- **Username**: Your gmail username before the `@`. If your email is `johnsmith@gmail.com`, this will be `johnsmith`.
- **Password**: The app password you generated earlier (not your Google account password!)
- **Encryption**: Secured connection using TLS

Once saved, you will receive a confirmation email in your inbox from Gmail. Press the link in the email to confirm your newly added email.

## Step 3: Adding DNS records

In your Cloudflare account, go to the DNS/Records page for your domain (located in the left sidebar).

Add another record with the following values:
- **Type**: `TXT`
- **Name**: `@`
- **TTL**: `auto`
- **Content**: `v=spf1 include:_spf.mx.cloudflare.net include:_spf.google.com ~all`

Finally, add one last record with the following values:
- **Type**: `TXT`
- **Name**: `_dmarc`
- **TTL**: `auto`
- **Content**: `v=DMARC1; p=none; rua=mailto:YOU@YOUR-DOMAIN.COM`

Make sure to replace YOU@YOUR-DOMAIN.COM with your chosen email address.  
For multiple addresses, comma-separate them like this:  
`v=DMARC1; p=none; rua=mailto:email1@example.com,email2@example.com,email3@example.com`

## Enjoy!

Good job! You've just set up your own custom email address with a custom domain for completely free!
You'll be able to send about 500 emails a day, which is more than enough for most small business or individuals.

It may take a couple days for all the DNS records to apply, so please be patient if your emails are being marked as spam or if emails aren't sending/receiving.

Thanks for reading!