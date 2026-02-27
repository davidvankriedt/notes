---
title: Plant Music
draft: false
tags:
  - computer-science
date: 28/02/2025
---
My idea for this project was to replicate [PlantWave](https://plantwave.com/en-au?srsltid=AfmBOopjlESxv4CwsNnEa6Gf5gXxGjZcrTY2EeklbxnKSF7H9SFa1J5X)'s device, a [[biodata sonification]] device, which is basically measuring changes on a plant's surface, and turning it into computer-readable data, in this case MIDI, and then mapping it to a synth that outputs sound, all in real time. They explain it much better [here](https://electricityforprogress.com/).

## Thoughts

This is my first time experimenting with micro-controllers, and really building any hardware. So I think there is quite a learning curve ahead of me before I can make anything viable.

## Components

#### 555 Timer IC

__NE555P__

| **Pin** | **Name**      | **What it does for your Plant**                                        |
| ------- | ------------- | ---------------------------------------------------------------------- |
| **1**   | **GND**       | Connects to the ground (negative) of your Arduino.                     |
| **2**   | **Trigger**   | Starts the timing cycle. Connected to Pin 6.                           |
| **3**   | **Output**    | **Crucial:** This sends the square wave signal to the Arduino.         |
| **4**   | **Reset**     | Connect to 5V to keep the chip "on."                                   |
| **5**   | **Control**   | Connect your **Ceramic Cap** here to ground to keep the signal stable. |
| **6**   | **Threshold** | Monitors the charge on your capacitor.                                 |
| **7**   | **Discharge** | This is where the plant and resistors "drain" the charge.              |
| **8**   | **VCC**       | Connect to 5V from your Arduino.                                       |