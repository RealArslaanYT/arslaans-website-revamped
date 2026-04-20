---
layout: post
title: "Why I wrote my own browser in C (and why it still failed me)"
author: Arslaan Pathan
image: /assets/images/post-image/browser-in-c.png
---

Chrome, Firefox, Edge, Brave, Safari, Opera.  
These are the most mainstream browsers in use today. Chances are, you probably use one of these browsers on your computer too.  
But what if you wanted to go *further?*

## Vim-like browsers

For people like me, who live in the terminal, normal browsing feels slow. You have to keep reaching for your mouse, clicking buttons, and the only thing close to keyboard-based navigation is "spam tab" and "scroll with the arrow keys".

To combat this problem, there are a multitude of browsers with keybinds inspired by Vim, which, in short terms, is a terminal-based text editor focused around modal editing. You're never reaching for the mouse, because everything is simply a keybind. It takes a while to learn, but in the long run, it makes your workflow ten times faster.

There are many Vim-like browsers, but the most popular one is **qutebrowser**.

Written in Python, qutebrowser is easily configurable, and has support for most modern web features due to being based on QtWebEngine, which, in turn, is a wrapper around Chromium.

## Random Access Memory (RAM)

For almost a year, I was a long-time user of qutebrowser. Coming from normal Firefox, I loved how efficiently I was able to read documentation and navigate pages compared to your average browser, and, simply put, I never thought I'd use another browser again.

Oh, was I so, so wrong.

To put it simply, Chromium uses *RAM*. Lots, and lots of RAM. It'll easily use over 500MB+ *per tab* and take 500MB more for just the runtime.  
Because qutebrowser is based on Chromium, it has the same RAM issues as Chromium, except it's actually **MULTIPLIED**, because it has to run Qt, which is already quite heavy, and on top of that is written in Python, which adds tons of overhead.  
On my RAM-constrained system (8GB), I would see system slowdowns, lockups, and OOM kills on the daily, which, is not ideal for a browser that claims to "improve productivity".

After a few months of this, I ended up getting sick of the constant lockups. A solution was to allocate more swap space, but that's not ideal in the long run: you still get tons of system slowdowns and other issues like SSD wear after utilising swap for too long.

## The Search(TM)

"Alright then," I thought.  
"I'll just search for another vim-like browser that doesn't use Chromium! It can't be *THAT* hard," I thought.

I tried **EVERY SINGLE ONE**. Well, every one that I could find, but I'm pretty sure it's an exhaustive list.
- Nyxt
- vimb
- wyeb
- surf
- Glide
- Luakit
- Tridactyl (an extension, I'll get to that)

The problem was, coming from qutebrowser, which is on the more featureful side, they all had their own issues and quirks that made them break my workflow.

I'll try to keep this short:

- Nyxt? Too emacs-y, and also, I dislike Lisp's syntax
- vimb? I'm not actually sure why I didn't use this one, there was some issue with compilation that made it not work properly or something along the lines of that  
- wyeb? I don't remember this one either  
- surf? Too minimal, I need at least tabs  
- Glide? This one was interesting, it's a fork of Firefox with Vim keybindings. I actually daily-drove it for a month, and it was a great browser, but after switching to Gentoo, it would keep freezing after 2 minutes of use and it kept consuming copious amounts of file descriptors. After a bit of troubleshooting, I just gave up on it.  
- Luakit? I had really tried to get this one to work. The concept was great: a lightweight browser, easily scriptable in Lua. But it had one missing feature: bookmark-style quickmarks. Luakit's quickmarks were single-letter, but I was looking for multi-character ones like in qutebrowser. To keep this short, I spent about 2 hours trying to make a Lua plugin that added one, but the docs were so bad I gave up.  
- Tridactyl? After trying it for just a little while, it just didn't work well enough for me. Browser extensions don't have as deep integration into the browser, so sometimes if things are focused wrong or if you are in the browser settings UI, it won't work, along with other quirks.

## The Dilemma(TM)

After all of that, I had 2 options:
- Go back to Firefox
- Make my own browser

So obviously, I chose the sane and pragmatic one: go back to Fi-  
**NO!!!!!!!!!!!!!!!!!!!!! WEBKITGTK TIME!!!**

all roads lead to writing code

## cinnamon-browser

In the end, I decided to make my own browser in C, powered by GTK3 and WebKit2GTK-4.1 (the simpler, less bloated API compared to GTK4 and WebKit2GTK-6.0). The source code is available [here](https://git.arslaancodes.com/cinnamon-browser.git/about/).

It has support for Vim keybindings, link following, hint mode, and is configurable in C with a config.h. (yes, you compile your config, suckless style. Why you ask? less work for me, and it loads 2 seconds faster)  
The sky is the limit for customization, config.h has a user_start function that runs before gtk_main, and you can have keybinds/commands that just run C code.  

Some crazy ideas I've had:  
- A keybind/command to `git clone` the current URL and open it in Neovim
- A keybind/command to run a userscript on the current URL from a file
- A keybind/command to inject YouTube adblock userscripts on the current page 
- A command that downloads Wii homebrew of your choice by simply searching and saves then in `/mnt/wii`
- And tons more...

## The Downfall(TM)

But, there's one issue with my custom browser:

None of those features matter if the browser eats RAM just like Chrome does.  
You might ask, "but didn't you use WebKitGTK? WebKit is a lot lighter than Chromium!"

And you're right---in theory.

But in execution? WebKitGTK is a horrible piece of software. Horrible, horrible browser engine.

While, yes, WebKitGTK has less RAM usage *on paper*, it leaks RAM. And when I say it leaks RAM, I mean it *REALLY* leaks RAM.

This is WebKitGTK's RAM usage with 5 tabs just after launch. The only other apps I have open are a few terminal windows (Neovim, nchat, profanity), Mumble, and Thunderbird.
```
arslaan@m2-mbp-gentoo:~
$ free -h
               total        used        free      shared  buff/cache   available
Mem:           7.3Gi       5.9Gi       549Mi       3.1Gi       4.5Gi       1.4Gi
Swap:           15Gi          0B        15Gi
```
Already not great. Accounting for overhead of around 1GB of shared RAM, WebKitGTK is already taking around 2GB in shared RAM.

This is WebKitGTK RAM usage with the same tabs and same background apps after about an hour of use.
```
arslaan@m2-mbp-gentoo:~
$ free -h
               total        used        free      shared  buff/cache   available
Mem:           7.3Gi       6.1Gi       621Mi       3.7Gi       4.8Gi       1.2Gi
Swap:           15Gi       1.7Gi        14Gi
```
This is on a GOOD day. Use the browser for 3-4 hours and you'll get swap usage ballooning to 3.5Gi+ and available memory going down to as low as 200Mi and less.  
I have to restart the browser many times per day, even though I shutdown after using my computer.

## The final question: What browser do I use now?

With all this trouble, you might ask the question: what browser do I use now?

And the answer is: cinnamon.

You might be confused, after watching me complain about RAM leaks for a while.

But all the alternatives are worse. I mean, not really, technically Chromium browsers are more stable, even if they eat more RAM. Technically, Firefox is the only engine that has acceptable RAM usage and still doesn't leak. (Mozilla, if you see this, PLEASE make an embeddable version of Firefox's engine/Gecko. PLEASE!!! I know you discontinued it in 2015 but BRING IT BACK!!!! IT WILL SOLVE ALL MY PROBLEMS)

But it's not *my* browser.  
That might sound like a stupid justification, and you know what, it might be.

But no browser can reach that level of customizability and personality than one you made yourself.

It's not perfect. I have to restart the browser at times. WebKitGTK leaks, it's sad to see a project with such potential be neglected. But I still like it, because I wrote it myself. The browser still works fine. I bet you that vimb, wyeb or any other WebKitGTK-based browser, like Epiphany, also have memory leaks. In fact, they do, I tested it.

And honestly? Even with the leaks, just restarting the browser occasionally is still better than using Chromium on my 8GB RAM system.

With how bloated and horrible the modern web is, the question isn't "Which browser works well on RAM-constrained systems?"  
The question is "Which browser works good enough for my use case?"  
And for me, that browser is cinnamon.

---

Thank you so much for reading my blog post! I'm a 13-year-old developer writing blog posts and making YouTube videos in my free time, so I'd really appreciate that you share this to others if you enjoyed it. Hopefully, I'll be coming out with a corresponding YouTube video for this blog post too, and when I do, it will be linked here.
