---
title: 'Raspberry Pi 4-Getting Started with Manjaro'
date: 2021-03-24
permalink: /posts/2021/03/Raspberry-pi-blog/
tags:
  - mathjax
  - latex
---
## Table of contents

[What is Raspberry Pi??](#what-is-raspberry-pi??)

[Things you will need](#things-you-will-need)

[Hardware Setup](#hardware-setup)

[Software Setup](#software-setup)

[Booting the Raspberry Pi](#booting-the-raspberry-pi)

[Display orientation issue](#display-orientation-issue)



## What is Raspberry Pi??

![Pic1](https://user-images.githubusercontent.com/81288438/112384822-deb1f900-8d14-11eb-9436-565c94b5bf27.jpg)

It is a low-cost Linux and ARM-based computer on a small circuit board sponsored by the charitable Raspberry Pi Foundation in the UK. One should not underestimate the power of these beasts as they can perform a whole lot of things a laptop can. With the 8GB RAM variant now available for Raspberry pi 4, these are becoming ever more powerful. From learning coding to performing pentesting on Kali OS, this portable beast is a machine worth having a look at.

Raspbian is the Debian-based Linux OS that is provided with the device, but one can install several other Linux variants like [Ubuntu](https://ubuntu.com/download/raspberry-pi), [Manjaro](https://manjaro.org/download/#raspberry-pi-4), [Fedora](https://arm.fedoraproject.org/) etc if they want.

----
## Things you will need.

There are lots of good starter Raspberry Pi 4 kits available on the market which has all the neccessary hardware required to get started. What the kit won't provide is a screen you would want to attach to the Raspberry Pi. It can obviously work on A.C supply but I would recommed getting an steady power supply(powerbanks) as Pi's **do not** like to be interrupted (especially during updates). 

Following things are required to get started with Raspberry Pi 4.

1. A 15W USB-C power supply
2. A microSD card (Get a 32 GB class 10 microSD card) *You can also buy preinstalled NOOBS card (New Out Of Box Software) but here we are installing Manjaro hence we need an empty card.*
3. A keyboard and a mouse
4. Cables to connect to display via Raspberry Pi 4's micro HDMI ports (*If you get a starter kit, you don't have to worry about it*)
5. An external display to connect with. (*You can buy touch screen display like [this one](https://www.raspberrypi.org/products/raspberry-pi-touch-display/), although if you have any spare monitor around you, use them instead*)

----
## Hardware Setup

If you have an external monitor to connect with, you can skip this step completely and go ahead to the next section of software setup. If you have an 7" touch screen display, you need to make some setup here before going ahead. With your display you will be provided with

1. Touchscreen Display with adapter Board attached with it.
2. DSI Ribbon cable.
3. Screws (used to mount the adapter board and Raspberry Pi board to the back of the display.)
4. Jumper wires (used to connect the power from the Adapter Board and the GPIO pins on the Pi )

![display](https://user-images.githubusercontent.com/81288438/112388619-6863c580-8d19-11eb-9922-fc664204a601.png)

Once we have everything we need, we can start making connections between Pi and the display. The following shows the connection of the jumper wires in the display. The DSI cable is attached as shown into the DSI connector which has a push lock mechanism to hold the cable securely. 

![screen_pins](https://user-images.githubusercontent.com/81288438/112388991-0192dc00-8d1a-11eb-929f-af38fafe08d4.jpg)

Once the connections are made, we can connect the wires in the Raspberry Pi 4 GPIO pins. The following image shows the numbering of the GPIO pins and the table below shows which wires go into which GPIO pin.

![GPIO](https://user-images.githubusercontent.com/81288438/112390238-fa6ccd80-8d1b-11eb-9591-2b6ecbc4266b.png)

| Colour        | GPIO pin | 
| ------------- |:--------:| 
| Red           |    4     | 
| Black         |    6     |   
| Yellow        |    5     |   
| Green         |    3     |   


![pi_pin](https://user-images.githubusercontent.com/81288438/112390186-e7f29400-8d1b-11eb-9e0a-f02d18a7084d.jpg)

Once connected, attach the display and the board with screws. Now if you have a case for the display, you can attach them as well. 

![final](https://user-images.githubusercontent.com/81288438/112390936-158c0d00-8d1d-11eb-979e-f0e23224a1aa.jpg)

----

## Software Setup

Once the assembly is ready we can move ahead to actual installation of Manjaro OS in the microSD card we have. Ideally a minimum of 8GB card is required but in my experience 32 GB card is worth an investment. If you are on a tight budget, get a 16GB microSD card. **Make sure you buy a fast microSD card, possibly a class 10**.

Before we can start the installation, we need to prepare our microSD card for it. We need to flash our Manjaro image onto the microSD card. For this you can download your preffered image of Manjaro from [here](https://manjaro.org/download/#raspberry-pi-4). For this post, I will be using KDE Plasma as I encountered certain issues with the XFCE version. You can go ahead and download any version you want. Next we need a tool to flash the downloaded image onto the microSD card. For this I will be using **balenaEtcher** which can be downloaded from [here](https://www.balena.io/etcher/). Since I am using Linux, I will be downloading the appimage for that. The following images will guide you to flash your microSD card.


Choose the image you have downloaded.
![etcher1](https://user-images.githubusercontent.com/81288438/112392347-3ead9d00-8d1f-11eb-87b8-2dae3dbc0465.png)

in my case it is Manjaro ARM KDE plasma
![etcher2](https://user-images.githubusercontent.com/81288438/112392355-41a88d80-8d1f-11eb-92bd-cbcfdf83837b.png)

Choose your microSD card (*Be careful here to choose your card*)

![etcher3](https://user-images.githubusercontent.com/81288438/112392370-44a37e00-8d1f-11eb-9f40-310d78db9a4f.png)

![etcher4](https://user-images.githubusercontent.com/81288438/112392382-4a00c880-8d1f-11eb-8396-3cec23a6f2e3.png)

Click flash

![etcher5](https://user-images.githubusercontent.com/81288438/112392386-4bca8c00-8d1f-11eb-8a41-195ea4e00de0.png)

In linux, provide authorisation

![etcher6](https://user-images.githubusercontent.com/81288438/112392400-5127d680-8d1f-11eb-82e6-c8e06d000cb1.png)

And done. This whole process can take upto 10 - 15 minutes depending on the write speed of the microSD card. Have patience.

![etcher7](https://user-images.githubusercontent.com/81288438/112392406-52f19a00-8d1f-11eb-91df-07c04330ca52.png)

Once done flashing, eject your microSD card and insert it into the Raspberry Pi. Provide your Pi with power supply via the USB-C cable. Once it recieves the power, it should turn on
(***you might get an inverted screen but don't worry, the solution is simple and is given at the end of the post***)

![Pic2](https://user-images.githubusercontent.com/81288438/112384991-128d1e80-8d15-11eb-8603-4c43885efb67.jpg)

----

## Booting the Raspberry Pi

Well we are in the endgame now(*wink wink*). Follow the images as shown here and you will have a booted Raspberry Pi runnning Manjaro within no time.


![Boot1](https://user-images.githubusercontent.com/81288438/112393651-71589500-8d21-11eb-926b-e168545f2c09.jpg)

Choose your keyboard layout( I have chosen **us**)
![Boot2](https://user-images.githubusercontent.com/81288438/112393660-73225880-8d21-11eb-81e1-e306da55237d.jpg)

Your desired user name
![Boot3](https://user-images.githubusercontent.com/81288438/112393664-74538580-8d21-11eb-90f0-390c6c35a3bd.jpg)

You can leave this empty if you aren't sure what it is or setup accordingly.
![Boot4](https://user-images.githubusercontent.com/81288438/112393681-7ae1fd00-8d21-11eb-9510-743a64c362fa.jpg)

![Boot5](https://user-images.githubusercontent.com/81288438/112393685-7d445700-8d21-11eb-96f0-af67716e981c.jpg)

Enter password and remember it as this is what you will need.
![Boot6](https://user-images.githubusercontent.com/81288438/112393689-7f0e1a80-8d21-11eb-89de-1806bb249448.jpg)

![Boot7](https://user-images.githubusercontent.com/81288438/112393697-80d7de00-8d21-11eb-938e-daf9b68247dc.jpg)

Choose password for root user
![Boot8](https://user-images.githubusercontent.com/81288438/112393698-82a1a180-8d21-11eb-98c1-d594896c01c5.jpg)

![Boot9](https://user-images.githubusercontent.com/81288438/112393702-846b6500-8d21-11eb-8779-a1db8c3dc750.jpg)

Choose you timezone (mine was Asia/Kolkata)
![Boot10](https://user-images.githubusercontent.com/81288438/112393708-86352880-8d21-11eb-9b7b-e4b25704d3e6.jpg)

Choose locale(en_US.UTF-8)

![Boot11](https://user-images.githubusercontent.com/81288438/112393711-87feec00-8d21-11eb-9630-1be7d13131dc.jpg)

Choose Hostname
![Boot12](https://user-images.githubusercontent.com/81288438/112393722-8a614600-8d21-11eb-8870-bad48327bcc0.jpg)

![Boot13](https://user-images.githubusercontent.com/81288438/112393728-8c2b0980-8d21-11eb-80be-8ba4c22b1cf3.jpg)

![Boot14](https://user-images.githubusercontent.com/81288438/112393738-8fbe9080-8d21-11eb-9cde-7c3e2e811d70.jpg)

![Boot15](https://user-images.githubusercontent.com/81288438/112393748-9220ea80-8d21-11eb-811d-0c9c537b6a7e.jpg)

The Welcome screen.
![Boot17](https://user-images.githubusercontent.com/81288438/112393774-99e08f00-8d21-11eb-9481-1337e77f4a58.jpg)

----

**Now you are done with the installation of Manjaro OS on your Raspberry Pi. I didn't find any issue with the KDE version of Manjaro on my pi. Everthing from touch, bluetooth, wifi worked right out of the box. Don't worry if your wifi takes a bit of time to be connected. Try using 5 GHz for your wifi connection. Once the Pi is connected with internet, the date and time are updated. updating your system is recommended either by using the GUI or by the following command from terminal(use ctrl+Alt+T)**

```bash
sudo pacman -Syu
```
---

## Display orientation issue

**If your touch screen  display is not in correct orientation all you have to do is take your microSD card out(after you shut down your pi obviously) and connect it to your computer and edit the config.txt file. Add the following command in the txt file and save it (if you get permission denied error while doing that, try sudo)**

```bash
lcd_rotate=2 # for touch screen displays
```

```bash
display_rotate=2 # for non touch displays
```

**If you do not want to remove the microSD card, you can do the same from terminal as well**

1. Open terminal by CTRL+ALT+T
2. Type:
```bash
sudo nano /boot/config.txt
```
3. Same as last. Add the line and restart your Pi. It should be done.

This is how your config file should look.

![config3](https://user-images.githubusercontent.com/81288438/112667512-556d0480-8e83-11eb-9ae9-488269054406.png)




## Enjoy your Raspberry Pi!!!
















