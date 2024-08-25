---
layout: post
title: Linux Driver Adventures with Alpha Network Cards
subtitle: My personal vendetta with Alpha Network Cards
tags: tech, network, linux
---

# Intro
Over the past two years, I have had difficulty with finding inspiration for a project to do in my own free time. That mostly occured due to having very little time outside of my univeristy life but I also had no clue **what** to do even if I did have the time.

Inspiration struck during a 2 month internship at a cybersecurity company. I spent a large amount of time during my internship working on network security and that meant a lot of intimate time with Alfa Network Cards. Alfa Network Inc is a company which provides external network adapters with lots of fancy antennas which are great for intercepting, modifying and capturing network traffic.

The problem, however, is that a large amount of the adapters use chipsets which do not have in-built support for the linux kernel. This often means that plugging in the adapter is not good enough, you need to find a working driver from some repository on the internet, hope you are not installing malware and pray that you do not brick your machine.

[This README](https://github.com/morrownr/USB-WiFi/blob/main/home/USB_WiFi_Adapter_out-of-kernel_drivers_for_Linux.md) explains very well what the problem is with wifi card chipsets and linux drivers.

When visiting the driver support page for a certain wifi adapter, Alfa Network will point you to a repository which is out of date for the kernel version you have running and will do nothing at best or crash your network manager at worst. At one point, it occured to me that it would be cool to get into the very centre of the linux kernel and see if I can fix or improve the drivers for these chipsets.

I have some experience with linux and have a decent understanding of the operating system, however I would still say I am not anywhere close to the required knowledge for developing and working on a linux driver.

# The Setup
The Alfa adapter that I struggled the most with was the Alfa AWUS036ACH. This uses the RTL8812au chipset and as you can see on the [support page for linux](https://docs.alfa.com.tw/Support/Linux/RTL8812AU/), points to two different driver repositories which you can download and compile from source. I ordered the Alfa card for my personal use and in the meantime started researching on how to get started on developing linux drivers.


