---
title: "My second attempt to use MacOS for work"
date: 2019-12-22T13:05:12+02:00
tags: [desktop, macos]
---
## MacOS

MacOS is an unix-like operation system developed by Apple. Apple cares a lot about UI/UX which makes graphic part of the system amazing. I love MacOS Dock idea and use dock-like software for Linux today. Being unix-like system gives MacOS a lot of advantages compared to say Windows. Native terminal, proper dir structure, process management, etc. On paper MacOS sounds amazing unix-like user-friendly OS for desktop. And it's very popular among software developers.

## First impressions

I first tried to use Macbook in 2006. I was already Linux-user by then and advised my parents to try Macbook, since it was well advertised and looked promising. Overall experience was not that different from Linux, it was okeish. Loved having terminal there. I've noticed few issues back then:

* Apple removed ability to change MAC address on your network device even for root. They reverted this change in next OS version, but it was very frustration and not only for me (see [apple forum discussions](https://discussions.apple.com/thread/1780907))
* Non-PC keyboard was irritating

It didn't offset huge price for Apple device for me back then and I've stayed on my PC with Linux.

# First attempt to work

Ten years after I've joined company where everyone was using MacOS and they suggested to try it for me. Like there is a browser and a terminal, what else do you need? For my personal use I was using Samsung Notebook 9 13 inch version (see [full spec](https://www.samsung.com/us/computing/windows-laptops/12-14/notebook-9-13-3-led-full-hd-core-i5-np900x3l-k06us/#specs)). Killed feature for me is 800g weight in this model.


This Samsung laptop was a clone of Macbook Air, so I've asked company to get me Macbook Air. Cost of Macbook Air in 2017 was a bit more than $1000. When it arrived I was disappointed:

1. Laptop that is almost twice as heavy as Samsung "clone"
1. Laptop for $1000+ in 2017 doesn't have fullHD resolution, while $300 laptops had one


But you can live with that, company is paying for hardware anyway and it's not like 1440x900 is not enough for terminal. Real issues began when I've tried to use MacOS for work, but I was too lazy to battle OS and decided to install Linux.

# Second attempt

Recently I've joined new company and they have me Macbook Pro 15' with touchbar and after 2 years I've decided to give it another try, but this time I'll try to solve my issues! And I've failed, turns out they are not really solvable. Here is my list:

* No way to change keyboard layout switch combination, you have to install special software for that. Ok, I've installed Karabiner Elements and turns out you can't bind 2 special keys (like Alt+Shift) as a hotkey even with special software. I've been using Alt+Shift for about 20 years, but Apple knows better what kind of keys you need to use. I ended up bind Alt+z.
* Non-PC keyboard. Not only Fn and Ctrl are switched, but special key and Alt too. So RIP my keyboard binding. Ok, I've attached standard PC keyboard and set PC keyboard as my keyboard type. Nope, it doesn't work like PC keyboard. When I try to type `'` symbol it starts diacritic mode and tries to add diacritic to my next symbol. So typing `'c` produces `č`, typing `'a` produces `å` and so on. Some other symbol are also acting weird on PC-type keyboard. Instead of `~` it tries to use `˜`. Input is just a pain.
* External PC keyboard not solving issue with layout, cuz sometimes you have to go on meeting or something without it.
* Although I've connected PC keyboard binding with CMD are still there. So I've remapped CMD to Ctrl, it's kinda solved.
* No console utils I got used to (ipcalc, calc, etc). I can probably compile it manually and add, but that's too much.
* Utils that are there are not the same utils I got used to. For some reason MacOS decided not use GNU utils, so sed & awk syntax is different. I know that I can install gnu utils and do symlinks, but I don't think it worth it.
* No hardware Esc key. As vim user I can't stand it.
* No copy-on-selection & paste-middle-click. In X-Windows there is separate copy-paste buffer for mouse. There is a feature in iTerm, but it works only for iTerm, you can't copy paster from/to browser. There is a software like macpaste, that allows you to do copy-on-selection & paste-middle-click, but it just spams Cmd+C on selection and Cmd+V on paste, which causes problems with some other software. And ofc it doesn't have separate buffer.
* No native docker. Since docker for MacOS is using Virtual machine, instead of getting lightweight & fast container you get VM overhead. Also since it's using virtual network you can't utilize network properly and connect to docker container IP directly.


After 2 months of suffering I've asked for PC laptop and installed Linux.

