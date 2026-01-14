---
layout: post
title: Linux on a TV Box—Raspberry Pi Alternative?
author: Arslaan Pathan
image: /assets/images/post-image/linux-tv-box.png
---

Raspberry Pis are quite popular—and for good reason.  
They have quite a lot to offer, from running home servers and retro gaming consoles to making mini robotics projects in your bedroom. They’re compact, affordable, and quite powerful, making them great for computer enthusiasts, like you (hopefully) and me.

But recently, due to the RAM shortages and other supply chain issues, the prices for Raspberry Pis have gone up quite a bit. A Raspberry Pi 5 with 16GB RAM now costs $300 New Zealand dollars, over $100 dollars more than it’s previous price.

Even with the price increases, it’s been hard to get a Pi at MSRP in some countries nowadays.

And that’s where the TV box from AliExpress comes in!

## The Chronicles of AliExpress: Prince T95

When you first look at one of these TV boxes, it may just look like another streaming device---but under the hood, it’s still a somewhat capable computer! Although some can ship with questionable firmware, and usually have bootloaders that make you want to bang your head against the wall, these boxes still have a decent processor, a mediocre but still functional amount of RAM, and a good amount of I/O and ports, which makes them *seemingly* quite suitable to act as a Raspberry Pi alternative.

The best part? These boxes are dirt cheap on AliExpress! I can purchase one right now for about $17.70 from AliExpress here in NZ, which is about $10.16 in US dollars. Way cheaper than a even a Raspberry Pi Zero.

So, that’s it, right? We’ve found a cheaper alternative to Raspberry Pi products?  
Don’t get your hopes up, because as we know, if it’s too good to be true, then it’s… too good to be true. Yes.

So what’s the catch with these TV boxes, you may ask?

## "Mum, I downloaded malware off LimeWire again"

CopyCat malware was found preinstalled on hundreds of these boxes commonly sold on AliExpress and Amazon. That alone should deter you from purchasing one of these and even coming close to plugging one of them into your network.

"But aren't we going to install Linux on them anyway? The malware wouldn't survive a clean Linux install!"  
Good question.

## Five Nights at Allwinner's

While technically, yes, you can install Linux on these boxes, that doesn’t mean it’s going to be easy. Most of the time, buying one of these boxes is a CPU roulette. You’ll buy a TV box off of AliExpress that claims it has a Rockchip SoC, but instead you’ll open it up and find an Amlogic SoC instead, or even worse, an *Allwinner*.

“But once you find the CPU model it’s not that hard, right?”  
Don’t get your hopes up yet, for there is a lot more to come.

## Nightmare on DTB Street

Figuring out how to get Linux to boot in the first place is not the best experience. You’ll find yourself in a rabbit hole of questionable tools, weird USB-A to USB-A cables, and flashing random SD card images until the bootloader decides it wants to have mercy on you.  
Some boxes will only boot custom images if tilted just at the right angle, or if it’s at specifically 11:23am on a Tuesday. Of course I’m exaggerating here, but it really does matter. I’ve had a TV box refuse to boot from eMMC unless I tilted it towards the corner of the room while it was booting and plugged into a specific power supply. 

There have been countless times that I’ve got something to boot on the TV box, ran to my mum shouting “MUM IT WORKED!!!!” and then came back to see it refuse to boot again.

And when you think that you’ve finally got it to boot, you realize that the Wi-Fi doesn’t work, the USB ports only work on Thursdays, and that drivers and documentation are either non-existent or all in Chinese.

## Conclusion

By the end of the process, you’ll realize that this $10 bargain cost you several hours wasted, your sanity, and your patience. Working with these TV boxes, ESPECIALLY ones that use an Allwinner SoC, are the kind of project that teach you more about patience than actual computing work.

So, do they work? Technically, yes.  
Are they worth it? No. Never again. We don’t talk about my experiences with the “Trivision TV Box”.

---

Thanks for reading my blog post!  
Feel free to watch the YouTube video linked below if you prefer to watch content in video format.

<div class="video-container">
  <iframe src="https://www.youtube.com/embed/h3BHi7Ohl1M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>