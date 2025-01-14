---
title: How I started making $700/month on TikTok within 3 months of creating my account.
tags: [Coding, Music Production, TikTok]
description: And grew to 12k followers from going LIVE.
comments: true
---

I created my TikTok account [@soundsandsimulations](https://www.tiktok.com/@soundsandsimulations) on July 6, 2024. The results since then speak for themselves: $700 earned per month, and 12k followers over 3 months.

Edit (2025-01-14): The most I've made to date is $2.8k in one month.

<blockquote class="tiktok-embed" cite="https://www.tiktok.com/@soundsandsimulations" data-unique-id="soundsandsimulations" data-embed-from="embed_page" data-embed-type="creator" style="border-left: none; max-width:780px; min-width:288px;"> <section> <a target="_blank" href="https://www.tiktok.com/@soundsandsimulations?refer=creator_embed">@soundsandsimulations</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>

<img src="/assets/posts/tiktok-earnings.jpg" width="400px">
<img src="/assets/posts/tiktok-followers.jpg" width="400px">

In this article, I'll reveal how I did it, and the strategies I learned along the way.

{% capture list_items %}
The Inspiration
The Generator
Creating the Account
Going LIVE
Conclusion
{% endcapture %}
{% include elements/list.html title="Table of Contents" type="toc" %}

## The Inspiration

I was scrolling through my FYP one day when I came across a video by [@mysmallproject_](https://www.tiktok.com/@mysmallproject_): a square bouncing along to some music. I thought to myself, *How did they make this?*

Then I looked at their profile. Their videos averaged 50-100k views. I looked up how much TikTok pays: ~50 cents per 1k views.

I did the math. $25 to $50 per video.

*I can do that!*

I began with some market research. [@mysmallproject_](https://www.tiktok.com/@mysmallproject_) was my blueprint, but there were plenty of other accounts competing in the same niche: [@rhythm.paradise](https://www.tiktok.com/@rhythm.paradise?_t=8mxvNoQU5Hy&_r=1), [@square.boom](https://www.tiktok.com/@square.boom?_t=8mxvo2QTsid&_r=1), to name a couple. I took note of which characteristics seemed to make some accounts more successful than others, from video quality to audio quality to branding.

I noticed that quite a few accounts had the exact same video style (background color, animation, etc.), so I suspected that they were using the same generator. Sure enough, with some Googling, I found it: a GitHub repository called [midi-playground](https://github.com/quasar098/midi-playground).

But the key to succeeding in a crowded niche is to be unique. So I decided to make my own generator from scratch.

## The Generator

In order to make the account scaleable, I needed a generator where I input a [MIDI](https://www.lifewire.com/midi-file-2621979) file, and it automatically spits out an animation. That way, I could easily pump out one video per day.

This was a fun, LeetCode-esque challenge. I had to read a list of MIDI notes and create an animation where the square bounces perfectly in time with each note. But there were a couple of key obstacles:

1. As I place each bounce pad, I need to make sure it doesn't send the square flying in a direction where the square hits a wall too soon (before the next note plays).

1. I also need to make sure the pad doesn't get in the way of the path that the square has already taken to get to this point.

<img src="/assets/posts/tiktok-pad.jpg" width="400px">

The solution: recursive backtracking! The final algorithm looked something like this:

1. Parse the MIDI file.

1. Use recursive backtracking to create a bounce path for the square, where the square bounces in a random direction during each note. If the current path fails for either of the reasons listed above, then backtrack and try a different path.

1. Finally, use binary search to expand each bounce pad to be as large as possible without interfering with the square's path. This creates the vast tunnel network that you see in my videos.

<img src="/assets/posts/tiktok-expand-pads.jpg" width="600px">

For the finishing touches, I added colors, particles, and bloom. At the start of each video, I also added a flurry of notes to grab the viewer's attention (a strategy used by many other accounts).

Ultimately, I think it was my terrain generation algorithm, visual effects, and audio quality that set my account apart.

<blockquote class="tiktok-embed" cite="https://www.tiktok.com/@soundsandsimulations/video/7413621582725303598" data-video-id="7413621582725303598" data-embed-from="embed_page" style="border-left: none; max-width:605px; min-width:325px;"> <section> <a target="_blank" title="@soundsandsimulations" href="https://www.tiktok.com/@soundsandsimulations?refer=embed">@soundsandsimulations</a> <p>Replying to @👾👾𖣂 ᎿᎻᎬᎽ.სႮV.ᏝᎬᎨᎶᎻ𖣂👾👾 When did you get it? 🟥🟨🟩🟦 <a title="guessthesong" target="_blank" href="https://www.tiktok.com/tag/guessthesong?refer=embed">#guessthesong</a> <a title="karaoke" target="_blank" href="https://www.tiktok.com/tag/karaoke?refer=embed">#karaoke</a> <a title="singalong" target="_blank" href="https://www.tiktok.com/tag/singalong?refer=embed">#singalong</a> <a title="hamilton" target="_blank" href="https://www.tiktok.com/tag/hamilton?refer=embed">#hamilton</a> <a title="musicaltheatre" target="_blank" href="https://www.tiktok.com/tag/musicaltheatre?refer=embed">#musicaltheatre</a> <a title="theatrekid" target="_blank" href="https://www.tiktok.com/tag/theatrekid?refer=embed">#theatrekid</a> <a title="satisfied" target="_blank" href="https://www.tiktok.com/tag/satisfied?refer=embed">#satisfied</a> <a title="angelicaschuyler" target="_blank" href="https://www.tiktok.com/tag/angelicaschuyler?refer=embed">#angelicaschuyler</a> </p> <a target="_blank" title="♬ original sound - soundsandsimulations" href="https://www.tiktok.com/music/original-sound-7413621497803115306?refer=embed">♬ original sound - soundsandsimulations</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>

## Creating the Account

I created the account on July 6, 2024. My process for creating each video took about 1.5 hours:

1. Use [FL Studio](https://www.image-line.com/) to make a cover of a song, and then export the MIDI file.

1. Plug the MIDI file into my generator to create an animation.

1. Pair the animation with the music in [Adobe Premiere](https://www.adobe.com/products/premiere.html).

1. Upload the video to TikTok.

For branding, I chose the name @soundsandsimulations and drew the logo in Photoshop. To prompt engagement, I started each video with a hook: "Can you guess the song before the background color changes?"

**My goal was to reach 10k followers**: the minimum threshold to join Tiktok's Creator Rewards Program.

Growth was slow at first. I was averaging 1k, maybe 2k views per video.

My first big break was on July 17, when, upon request, I posted a video of [*FAERIE SOIRÉE*](https://www.tiktok.com/@soundsandsimulations/video/7392498847173348650), a Melanie Martinez song I had never of. Suddenly, the Melanie Martinez fandom came flooding in, follow after follow. I jumped to 2k followers.

<img src="/assets/posts/tiktok-melanie.jpg" width="400px">

Afterward, I was getting about 50k views per video—but people weren't following. I posted songs from different corners of the internet, from musicals to video games to TV shows, trying to appeal to different niches, but I wasn't getting the spike in followers that I hoped for. It turns out that on TikTok, **it's easy to get views, but it's difficult to incentivize viewers to click the follow button.**

My growth was plateauing. I needed a new strategy.

## Going LIVE

I reached out for advice from a friend who ran a successful TikTok account. He said, "You should try going LIVE, that's a great way to grow."

So I downloaded [TikTok LIVE Studio](https://www.tiktok.com/studio/download) and [OBS Studio](https://obsproject.com/). I didn't want to show my face on my account, so I decided to create a PNGTuber avatar (a simple avatar that shakes when you speak) using [veadotube](https://veado.tube/).

<img src="/assets/posts/tiktok-avatar.png" width="50px">

I took a break from posting and focused on going LIVE to gain followers. At first, I tried streaming my video creation process. It flopped. People didn't care.

I asked myself, *If I were a viewer, what would I want to watch on LIVE?*

Then I remembered that during COVID, I used to spend hours on a livestream playing an automated, interactive word guessing game.

Inspired, I programmed interactive versions of my favorite online word games: Wordle, Contexto, and Connections. Viewers would send their guesses in the chat, and my program would use the [TikTok-Live-Connector](https://github.com/zerodytrash/TikTok-Live-Connector) library to automatically read and respond to their guesses.

<img src="/assets/posts/tiktok-games.png">

<div style="text-align: center; margin: 0 auto; width: 50%;">
  <blockquote style="border-left: none;" class="imgur-embed-pub" lang="en" data-id="a/IbWyA6T">
    <a href="//imgur.com/a/IbWyA6T">LIVE</a>
  </blockquote>
</div>
<script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>


It was a success. On a good night of streaming, I would reach over 600 concurrent viewers and gain ~500 new followers.

<img src="/assets/posts/tiktok-live.png">

Finally, during a livestream on September 11, it happened: I reached 10k followers and officially joined the TikTok Creator Rewards Program. 🥳

Afterward, I stopped streaming and returned to posting videos. With each new video, the money came rolling in.

## Conclusion

In summary, this was the journey that I took to grow my TikTok account:

1. I had an idea.

1. I did some market research.

1. I came up with a way to generate content that was unique and scaleable.

1. I posted until I reached 1k followers (the minimum threshold in order to go LIVE).

1. I went LIVE until I reached 10k followers (the minimum threshold to get monetized).

1. Profit!

Here are some generalizable tips that I learned along the way:

- It's critical to start with market research. Make a spreadsheet of both successful *and* unsuccessful creators in your niche. Take note of what sets the successful ones apart from the others.

- Make sure that your content stands out in some way. It's almost impossible to compete in oversaturated niches like [#RedditStories](https://www.tiktok.com/tag/redditstories) unless you have something unique to offer.

- Ideally, come up with a content niche where you can easily generate videos that are longer than 1 minute. Only videos longer than 1 minute qualify for monetization.

- You have <1 second at the start of your video to grab the viewer's attention before they scroll away.

For going LIVE:

- An easy way to gain traction is by streaming interactive games. Even if you don't know how to code, you could still stream yourself playing games and invite audience participation.

- Regularly remind viewers to follow, and give them incentives for following.

- Don't expect to make much money from LIVE gifts; a TikTok rose amounts to less than 1 cent.

- If you don't want to show your face, you should still use an avatar of some sort (like a PNGTuber avatar).

Good luck!
