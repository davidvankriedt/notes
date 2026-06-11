---
title: Birdsong
draft: false
tags:
  - computer-science
  - cybersec
  - embedded-systems
---
This is my project for COMP6841, my research and progress will live here.

# Aim

I want to build a communication protocol that uses sound waves to transmit an encrypted message. Alongside this protocol, I'll build a device with a speaker and microphone that can send and receive messages, and a client software that will live on my laptop.

## Week 2

Before I go out and by the hardware I need, I first need to learn about [[Digital Signal Processing]], and [[Microcontrollers]].

I currently have an [Arduino Nano](https://docs.arduino.cc/hardware/nano), which only has a 16 MHz processor, which according to Gemini will only let me handle small bleeps of sound, through techniques such as [DTMF](https://www.youtube.com/watch?v=bAbNl8O6sSY) (think a phone number pad sound). However, I'm looking to hide messages into more of a bird's song, and so it recommended me [[Duinotech ESP32 Main Board]] due to its complex math capabilities.