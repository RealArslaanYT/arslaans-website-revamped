---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

title: Home
layout: base
head_extra: |
  <link rel="stylesheet" href="/assets/css/home.css">
nav_order: 1
---

### Hi, I'm Arslaan!

# I'm a 13-year-old developer exploring programming, Linux, FOSS, iOS jailbreaking, embedded systems, robotics, and game development.

<details class="about-me">
  <summary>Read more about me</summary>
  <div markdown="1">

I like computer science, writing stories (sometimes), Linux, FOSS (Free Open-Source Software), hacking, reverse-engineering and iOS jailbreaking. My favorite genre of music is Hyperpop, particularly Hyperpop-Digicore & Hyperpop-Glitchcore. I work on various projects in web development, system programming, and hardware hacking.

I mainly use Gentoo Linux on my M2 MacBook Pro (thanks to the [Asahi Linux](https://asahilinux.org){: target="_blank" } project) with the MangoWM tiling window manager along with waybar, wofi, swaylock-effects, and more. My favorite games are osu!, Minecraft and Stick Fight: The Game. I’ve been programming and tinkering with devices since somewhere around the age of six. What originally got me into programming was looking at my old iPad 2 (which I still have as of 2025, seven years later - it's now jailbroken with [EtasonJB](https://etasonjb.tihmstar.net/){: target="_blank" } because I felt like it) and saying – “how are these apps made?”

Feel free to explore my projects, stories, and achievements, and thanks for stopping by!

  </div>
</details>

<br/>

<div class="full-bar bg1">
<div class="content" markdown="1">

# [cinnamon-browser](https://git.arslaancodes.com/cinnamon-browser.git/about/){: .white target="_blank" }

A lightweight suckless-inspired vimlike browser written in C, powered by WebKit2GTK-4.1 and GTK3.

- Built with: C, GTK3, WebKit2GTK
- Status: Completed

---

## Features

- Vim-like keybindings
- Command mode with `:`
- Quickmarks (similar to ones in qutebrowser)
- Tabs
- Hint mode
- Suckless-style C configuration file (config.h)

---

## Why I built it 

For a while, I was a long-time user of qutebrowser, a popular vim-like browser written in Python and PyQtWebEngine. It was a great browser, and worked very well for my use cases, but eventually, I ran into an issue: the browser was too heavy on my system. Even though (as of 2026-04-15) I have a MacBook Pro M2, which is a powerful machine, I only have 8GB RAM, which, in this digital world, is absolutely nothing. Open too many Chrome tabs? Good luck, mr. OOM killer has come to your doorstep. Because qutebrowser is powered by PyQtWebEngine, which in turn is powered by Chromium, it tends to be quite heavy on my system and eat a lot of RAM.

So, to fix this problem, there was only one proper way. MAKE YOUR OWN BROWSER IN C AND WEBKITGTK!!!!!!!!!!!!!!!!!!!!!!!!!

</div>
</div>

<br/>

<div class="full-bar bg2">
<div class="content" markdown="1">

# [styl1sh.js](https://github.com/RealArslaanYT/styl1sh.js){: .white target="_blank" }

A lightweight CSS-in-JS library that makes your styles dynamic.

- Built with: JavaScript
- Status: Completed

---

## Features

- Dynamic, event-based styles: Attach styles to events like `click`, `scroll`, `keydown`, `animationFrame`, and much more.
- Theme-aware: `styl1sh.runtimeState.currentTheme` reacts to theme changes instantly, providing a seamless experience.
- Minimal & Fast: Tiny footprint, no dependencies.
- Familiar syntax: With stylesheet syntax almost identical to CSS, you can learn to use styl1sh.js easily.

---

## Why I built it 

I was browsing the web when I found an old concept from late 1996, titled JSSS, which stood for "JavaScript-based Style Sheets". It's goal was to implement dynamic and adjustable stylesheets in JavaScript using simple but powerful syntax.  
I found this concept really cool, and was somewhat sad that it wasn't taken into the modern web. The only web browser known to make some implementation of it was Netscape Navigator, and, we all know that Netscape doesn't really exist anymore.  
So, I did the only sane thing: I just made it myself! My concept for the syntax is quite different and more modernized to add event handlers and hooks, but the idea is about the same.

</div>
</div>

<br/>

<div class="full-bar bg3">
<div class="content" markdown="1">

# [SCR4TCH](/links-page/scr4tch/){: .white }
A modification of Scratch that allows you to parse JSON, send HTTP requests, and a few extras. Mainly created as a side-project.

- Built with: Node.js, React
- Status: Completed

---

## Features

- HTTP Requests in Scratch via the custom `HTTP Requests` extension
- JSON Parsing in Scratch via the custom `JSON Parse` extension

---

## Why I built it

scratch from temu

</div>
</div>

<br/>

<div class="full-bar bg4">
<div class="content" markdown="1">

# [Onyx Client](https://github.com/RealArslaanYT/onyx-client-core){: .white target="_blank" }

A modern, feature-packed client for Minecraft 1.21.5, designed to enhance the user experience with a variety of Quality of Life improvements and intuitive features. Mainly created as a side-project.

- Built with: Fabric, Java
- Status: Completed

---

## Features
- 1.8-style Combat
- Coordinates HUD
- Keystrokes HUD
- Freelook
- Mod state saving

--- 

## Why I built it 

No specific reason, I just wanted to get into Minecraft modding at the time and thought it'd be a fun project.

</div>
</div>

<br/>

<div class="full-bar bg5">
<div class="content" markdown="1">

# [BrowserServicePython](https://github.com/RealArslaanYT/BrowserServicePython){: .white target="_blank" }
A lightweight remote browser service written in Python. Allows you to access a remote browser in a browser window. Mainly created as a side-project.

- Built with: Python, JavaScript/WebSockets
- Status: Completed

---

## Features

- Responsive remote browser feed
- Very lightweight --- one .html file for the frontend, one .py file for the backend.
- Easy deployment using Docker

---

## Why I built it 

Like some of my other projects, there's no specific reason, I just felt like it.

</div>
</div>

<br/>

<div class="full-bar bg2">
<div class="content" markdown="1">

# [Showdown of the Sticks](https://realarslaanyt.github.io/Showdown-Of-The-Sticks){: .white target="_blank" }
A fast-paced, pixel-art style stick figure fighting game.

- Built with: SDL2, C++, Lua
- Status: In-progress (pretty much abandoned)

---

## Features

- Fast-paced stick figure combat
- Retro pixel-art aesthetic (artwork not finished)
- Local multiplayer support
- Online multiplayer support (in development)
- Unique weapons and abilities (in development)

---

## Why I built it 

"If Animation VERSUS will take too long to release, then FINE, ILL DO IT MYSELF!!!!!!!!!!" - me, 2025

</div>
</div>
