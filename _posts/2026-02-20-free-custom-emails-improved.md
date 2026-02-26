---
layout: post
title: A 13-year-old's (improved) guide to free custom emails 
author: Arslaan Pathan
image: /assets/images/post-image/free-custom-emails-improved.png
---

Are you a small business looking to get a free custom email?  
A software developer wanting a more professional inbox?  
Or a hobbyist just wanting to flex a custom email to their friends?

If so, this article is for **you**!

I'm Arslaan Pathan, and as of 2026, I'm 13 years old. This is an improved version of my [previous guide](/2025/12/16/free-custom-email.html). If you've already set that up, I'd recommend switching --- I'll explain why in a second. It only takes 30 minutes to an hour, and it's much more secure than the previous method.
If you're new and don't want to hear me yap about why the old method was broken, skip to the section titled "Getting Started".

## Why the old method was fundamentally broken

The previous method used Gmail SMTP to send the emails, which works, but it has a fundamental flaw that most tutorials don't tell you about.

The problem is that Gmail SMTP is made to send emails only through a Google-managed email, for example, a normal Gmail account, or if you pay for Google Workspace (the fact that you're here trying to find free emails shows you probably don't), that account.

When you send from the Gmail SMTP, SPF passes, because we place the correct records in our DNS, but DMARC still fails because of misalignment (and so does DKIM because DKIM is signed with Gmail's servers). Gmail SMTP will always, no matter what, set the Envelope-From to your Gmail address in the email headers, even if you have a different From address. This makes the DMARC alignment fail, which in turn causes DMARC itself to fail.

The only reason our emails were still even sending was that we had 'p=none' set in our DMARC TXT records, which tells the mail servers to accept our emails even if checks fail. This makes it extremely easy for an attacker to spoof our emails, because our DMARC records are set to accept everything. Setting it to 'p=quarantine' or 'p=reject' with the old method was impossible, because that would make our check-failing legitimate emails undeliverable.

The new method uses Resend SMTP to send emails, which is a mail-sending service that has a free tier for developers and hobbyists. Resend explicitly supports custom domains and passes all of the SPF/DKIM/DMARC checks, avoiding our issues from earlier.

## Getting Started

### Setting up Cloudflare Email Routing

The first step in creating a custom business email is receiving emails.  This guide assumes you are using Cloudflare nameservers with your domain.
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

### Setting up Resend SMTP

article is not finished
if you see this blog post that means i accidentally pushed an unfininished thing to git
and as a result the auto git pull on my server just took it :)
