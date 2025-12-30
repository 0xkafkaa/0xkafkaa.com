+++
title = "Exploring Microcontrollers"

[taxonomies]
tags = ["microcontrollers", "hacking", "tinkering"]

[extra]
toc = false
+++

I have always been curious about Microcontrollers and IOT in general ever since I got interested in the hacking culture. The beauty of the computation which happens in a cute litte component always makes me appreciate it further more.

<div class="center">
<img src="/img/blogs/mc.jpg" alt="microcontroller">
</div>

[Project IGOR](https://github.com/UrbanCircles/igor) by [Urban Circles](https://www.youtube.com/@UrbanCircles) felt like a great place to start. In a world full of distractions, build with overly engineered products for productivy finding something which does only one simple task could be challenging. This is what [Project IGOR](https://github.com/UrbanCircles/igor) tries to solve. I just love the philosophy on which its built on.

<blockquote>
"Do one thing and do it well."
- Doug McIlroy
</blockquote>

[Project IGOR](https://github.com/UrbanCircles/igor), an open-source focus timer project using an ESP8266, an OLED display, and a rotary encoder. Igor is designed to provide an intuitive way to manage focus sessions. The rotary encoder is used to set the time, and the OLED display provides real-time feedback. The ESP8266 acts as the brain of the system, handling user inputs and updating the display.

The firmware is written in Arduino using the Adafruit SSD1306 and Rotary Encoder libraries. The main logic involves:

- Reading the rotary encoder to adjust the timer.
- Displaying the timer on the OLED screen.
- Starting a countdown and updating the display.
- Triggering an alert or indication when the session ends.

I messed up a few components during soldering them since I am all new to this but it was a fun little project. Implementing Igor was an exciting journey into embedded development, combining hardware interfacing, real-time input handling, and display manipulation.
