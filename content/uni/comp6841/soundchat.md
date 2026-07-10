---
title: soudnchat
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

Before I go out and buy the hardware I need, I first need to learn about [[Digital Signal Processing]], and [[Microcontrollers]].

I currently have an [Arduino Nano](https://docs.arduino.cc/hardware/nano), which only has a 16 MHz processor, which according to Gemini will only let me handle small bleeps of sound, through techniques such as [DTMF](https://www.youtube.com/watch?v=bAbNl8O6sSY) (think a phone number pad sound). However, I'm looking to hide messages into more of a bird's song, and so it recommended me [[Duinotech ESP32 Main Board]] due to its complex math capabilities.

## Week 3

I think I am sidetracking quite a bit. I've dived into microcontrollers to have a client device to talk to, but ideally I wanted another user to respond using that device, therefore the microcontroller also needs to handle keyboard input. Given that I haven't started the actual protocol yet, I've decided to abandon the idea of building a microcontroller as a client, and rather using a different machine like another laptop to do the same job.

## Week 4

I initially wanted to write the script in C, but considering the time constraints of the course, I instead decided to use Python because of its easy to use libraries for recording and playing sound - sounddevice, and its additional DSP abilities through numpy. I then started thinking about what could be a way to communicate a message through sound, without using words, and concluded that a possibility could be morse code, since it's efficient, and because its data is binary, it would make it easier to capture the message through noise.

## Week 5

I first looked into how I could implement a morse code system in Python, mapping morse code to text, and I came across the Python library pymorsed, which came with functions for encoding and decoding text to morse, and converting to audio. I played around building a few different iterations of converting plain text to morse code, and then to audio, and it worked well!

## Week 6

I realised I couldn't just type text, turn it into morse code, play it out loud, and manually do this with another person. It wouldn't be the easy interface I was planning to create. So, I started thinking about how I could implement a communication protocol, and decided that there would be a host who initiated a chat connection, and a client who would connect to the host. I also thought about there being more than one chat within a room, so there would be morse code coming from every direction. For that reason, I thought of isolating chats by filtering sound through pitch, and since in western music there are only 12 notes, there could only be a maximum of 12 chats per room.

### Marco Polo

The host creates a connection by playing the morse code audio version of "MARCO", and then waiting and recording for 10 seconds. Meanwhile, the client looks for a connection by waiting and recording for 10 seconds, looking for "MARCO". Once found, the client responds with "POLO". The host then hears this, and responds with "START", in a specific pitch chosen by the host. The client hears "START", and plays the first message using that pitch, and from then on filters the audio received to only hear that pitch.

#### Testing Marco Polo

After implementing this, I tried testing it with my Mac Mini as client, and my ThinkPad laptop as host. 

##### Issues

One issue I found testing the initial connection was that the host played "MARCO", and waited for 10 seconds. Meanwhile the client waited 10 seconds, and if it heard "MARCO" it would return "POLO" and continue to do so after 10 seconds. This however, proved to be quite challenging when trying to get the client to hear the full word "MARCO" without cutting out because of the 10 second interval.

Here is the bigger issue. The thinkpad would play "MARCO" in morse code, and the host picked up chunks of the message. However, the input for the Mac Mini was a good analog microphone going into a sound interface, meaning I could control the exposure to the sound input such that the recorded signal wasn't distorted. This still didn't work at times - there were only a few times when the client picked up "MARCO". Doing it the other way proved to be much harder, when the mac mini played "MARCO" and my thinkpad tried to pick it up, it couldn't pick up any morse code at all. I inspected the wav file and found out that there was quite a bit of echo and slight distortion in the audio. I suspect this is the issue - the microphone built into my laptop, alongside the speakers connected to the host, are creating distortion, and this noise is making it hard for the function in pymorsed to decode the morse code. I realised that with this setup, I would essentially need to have a very quiet environment, with good microphones and speakers to communicate the morse code. Since I want this project to be useful in the real world, I decided this wasn't good enough, and wouldn't be a possibility even for my own testing purposes. From here, I decided there were two paths I could go down:

1. Improve the decoding function such that it can distinguish the morse code through noise.
2. Use an easier, shorter sound signal to communicate this.

Since the first option seems challenging to do, I figured I would try the second first.

## 00 and 11

shorter initiation message

## Filtering noise / amplifying signal

optimising the input for the decoding function