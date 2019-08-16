---
title: "My cloud gaming setup"
date: 2019-08-16T01:58:54+03:00
tags: [games]
---
I used to own Xbox One with Kinect around 5 years ago and had a lot of fun with it. My favorite games back then were Assassins Creed series, Prototype and Dishonored. At first I was thinking what should I buy PS4 or new Xbox? Maybe wait for next generation or fuck it and buy a gaming PC? But all of a sudden I found this 'cloud gaming' thing. I was sceptical at first because milliseconds of latency matter in video games and I get around 40-50 ms to nearest AWS region. Turns out I was wrong. 
## NVIDIA SHIELD
![nvshield](https://cdn.pocket-lint.com/r/s/1200x/assets/images/139934-tv-review-nvidia-shield-tv-2017-review-image1-ojemvonj4y.jpg)

I bought this device not because of it's cloud gaming feature but because it had best reviews among android STB's. And if it has cloud gaming features I can at least try it. It cost me around $220-$250 on Amazon and I had to pick it up in NY, because there are no way you can buy 2017 version in Ukraine apparently.

Experience with this device as STB was great and then I've played few demo games using NVIDIA Now service. It's a service that basically runs windows VM with GPU inside AWS on spot-instances. All instances have steam + most popular games installed. And currently it's free of charge because it's in beta.

You don't get full access to the server of course, they allow you to run steam and that's it. Instance has limited life time and 1 session is limited by 4 hours. Downsides caused by this:

* You have to login to steam each time in the beginning of the session
* If game is not popular and not included into base NVIDIA Now image you have to download it the beginning of each session
* If game doesn't support cloud saves - you can't use it

I don't think those are some huge drawbacks especially if you play something popular and 99% of popular games support cloud saves. Gaming experience is really good, I've played new Assassins Creed: Odyssey and it feels like you are playing local while actually this server is hundreds of miles away. My initial fear of 50 ms latency was caused by previous experience with Counter Strike where 50 ms makes game almost unplayable, but the difference is that latency to game server is not the same as latency to your input, you don't need to sync it with other player actions or whatever.

You can also connect keyboard + mouse to device and play stuff like Dota 2 or Counter Strike, but I don't have proper screen and playing those games from sofa is not really what you want.


In general I would highly recommend this device, it's my best purchase in a year. I don't only use it for games, but also watch videos and there is even possibility to install PopcornTime.

## Parsec
![parsec](https://s3.amazonaws.com/parsec-static/img/parsec-social.jpg)
So if NVIDIA SHIELD is so great, why do I need something else? Well unfortunately there is a game I've spend 300+ hours in and it doesn't support cloud saves (dunno why). FYI it's called Oxygen not Included.

It's also hard to play this game on my laptop because it's CPU heavy therefore my laptop is getting hot as f. I've researched what can I do to solve this. NVIDIA Now has desktop option, but there is not much difference in functions. I still can't save local files for local saved games.

Project I've found called [parsec](https://parsecgaming.com), they actually open sourced their [engine](https://github.com/parsec-cloud) and provide you and option to buy cloud server from them via few cloud providers that support GPU instances. Currently they support AWS, GCP and Pappertrail. And they have linux client which is perfect for me.

What is even better is that you can connect your own windows server with GPU and stream game from it. That's exactly what I need! I can just use AWS spot instance, save game files on EBS and turn it on only when I need it while also cutting costs by utilizing spot instance. I've registered my personal AWS account (I've managed so many, but never had my personal), added CC info, added request to support to increase my limits for GPU instances. And AWS said 'no'. Apparently they considered my account too new and refused to take my money. First time I get denied by AWS support on limit increase, what a joke. It also took them almost 48 hours to respond. Typical AWS support.

That's how I ended up on GCP. GCP doesn't have spot instances with spot market and non-fixed prices, what they do instead is 'preemptive' instances that have similar restrictions (can be shut down any moment) but have flat 80% discount. I'll take it! GCP support increased my limit within an hour and after 2 hours I was already playing ONI on GCP! I found that somebody made [GCP configuration](https://github.com/putty182/gcloudrig) that was near perfect for me. I just did few tweaks but nothing major.

I should mention ridiculous fees for licenses. I wasn't expecting windows license fee & nvidia license fee would cost more than hardware itself. In total I pay around $1 per hour of gaming on top tier PC with great video card. Totally worth it.

There is no way I'm going back to buying real hardware. Cloud gaming match perfectly my needs (occasional gaming few hours per week) and I always have top tier hardware to run games on. No upgrades or something. And for most of the games it's even free with NVIDIA Now. The only thing I need is proper internet connection (I have 1 Gbps) with low latency to nearest datacenter.
