---
layout: post
section-type: post
title: Brightness adjustment failure in Toshiba Satellite L755 with Ubuntu 12.04 LTS -- Fixed!
category: tech
tags: [ 'ubuntu' ]
---

This is a hack I came across in Ubuntu some time ago but just felt that it would be worth sharing.

I am having a Toshiba Satellite L755 laptop and I always came across some issues or incompatibilities when ever I installed Ubuntu in it. Most of them were related with the graphic card I'm having which is the NVIDIA® GeForce® GT 525M. So the most excruciating experience I had from those issues was the inability to change the screen brightness. The usual brightness adjustment keyboard key combinations do not work and the brightness slider in System Settings even did not have any effect when changed. This almost made it unable for me to work in Ubuntu because I started getting headaches due to the unbearable brightness of the screen.

![Toshiba Satellite L755](/img/posts/ubuntu-brightness-fix/L755.jpg)

After ages of searching on the internet I finally found a neat solution. The first step is to run this command in a terminal

<pre><code data-trim class="bash">
xrandr -q | grep " connected"

</code></pre>

The result of the above command in my machine is

<pre><code data-trim class="text">
LVDS-0 connected 1366x768+0+0 (normal left inverted right x axis y axis) 344mm x 194mm

</code></pre>

and should not necessarily be equal to what someone else would get. The important information that should be reaped from the above result is the part that stands for the display, which is in my case *LVDS-0*.

All that is needed to be done next is run the command

<pre><code data-trim class="bash">
xrandr --output LVDS-0 --brightness 0.5

</code></pre>

in the terminal replacing whatever you got in place of *LVDS-0*.

The value 0.5 represents the amount the screen should be dimmed and can be given any value from 0 to 1.