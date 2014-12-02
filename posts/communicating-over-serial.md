<!-- 
.. title: Communicating over Serial
.. slug: communicating-over-serial
.. date: 2014-12-02 14:12:46 UTC-08:00
.. tags: arduino,serial,LEDs,command line
.. link: 
.. description: 
.. type: text
.. author: pengor
-->

Today we got a basic serial communication setup between our Arduino and a command line running through Linux. The code for the demo is available in our Hardware Demos GitHub repository. This is important for the project because it enables us to begin connecting the two main aspects of the project, the rover and the Emotiv EPOC headpiece. In the demo we pass RGB decimal values from the command line to the Arduino and it returns the corresponding hexadecimal color code.