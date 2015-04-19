<!-- 
.. title: Spring Semester - A whole bunch of TODOs
.. slug: spring-semester-a-whole-bunch-of-todos
.. date: 2015-03-10 19:28:37 UTC-07:00
.. tags: arduino,rfduino,sdk,group meeting,faculty meeting,linux,fft,openbci
.. link: 
.. description: 
.. type: text
.. author: phora
-->

Spring semester's a month in and we hadn't updated the blog until now. Part of
this was due to needing to find a new meeting time to meet with our advisor,
polishing what we had for the cart, understanding how to denoise data using
the FFT transformation of said data, and thumbing through the source code for
the OpenBCI boards.

There a few things that we discovered about using the OpenBCI boards in our project:

* We'd need to find a way to install the RFDuino library so the Arduino IDE
can access it and properly program the dongle and the board.
* We had to resort to stitching some vinyl onto some velcro to make applying the 
electrodes to ourselves a lot easier.
* Our master plan of powering the OpenBCI dongle with 3V from the Arduino pin
didn't work. However, using a cut USB female cord does work to power it.
* At some point, we need to solder the headers for the OpenBCI boards.
* We'd need to find a way to write the firmware for the dongle so it can still talk
to the OpenBCI GUI when plugged in. We're planning to have the dongle talk to the OpenBCI
board as a middle man so the rover can receive data from the board wirelessly. This
will be done over a serial established with two of the free pins on the dongle.
* If the FFT calculations prove to be too much for the OpenBCI dongle, OpenBCI board,
or the Arduino driving the cart, then we might need to get specialized hardware to do
the FFT calculations. Chances of this are pretty slim though since we have plenty of Arduinos.
