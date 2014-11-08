<!-- 
.. title: Installing Arch Linux in the Morken 212A Lab
.. slug: installing-arch-linux-in-the-morken-212a-lab
.. date: 2014-11-03 19:22:30 UTC-08:00
.. tags: arch linux,linux,workspace preparation,faculty meeting,group meeting,emotiv
.. link: 
.. description: 
.. type: text
.. author: phora
-->

This took a while to document since I spread the installation out over three days (Monday, Tuesday, and Thursday specifically). The first few hours were spent trying to figure out why the 
LiveUSB's Arch Linux installer wouldn't boot. After inspecting the specs for all of the desktops, turns out it was just the computers' fault. The rest of the time was spent waiting for the packages to finish installing. The reason why we installed Arch Linux on these computers was:

1. Ready access to the software we need (Arduino SDK and several dependencies for the Emotiv EPOC SDK) through the AUR
2. phora has experience with Arch Linux packaging since she has an Arch Linux desktop
3. It is easy to install only the packages needed

And the packages and packages we installed on the machines were:

* base{,-devel} - Required for all Arch Linux machines. base-devel is an assumed prerequisite for using the AUR.
* kdebase - Easy to set up, ultra-customizable GUI
* kdegraphics-{gwenview,okular} - Basic needs (image viewing, pdf viewing)
* gimp - For editing our concept art
* dia - For editing our concept diagrams
* android-sdk{,-platform-tools} - In case we need to develop any android applications
* eclipse-android - In case we need to develop any android applications
* arduino - To start programming basic functionality in the robot
* qtcurve - To keep all GUI widget themes consistent (this is important for the accessibility problems mentioned in [Emotiv EPOC SDK Experiments](/posts/emotiv-epoc-sdk-experiments/)). Also makes changing the color and styling without much technical knowhow.
* kde-gtk-config - To keep all GUI widget themes consistent (this is important for the accessibility problems mentioned in [Emotiv EPOC SDK Experiments](/posts/emotiv-epoc-sdk-experiments/)). Also makes changing the color and styling without much technical knowhow.
* firefox - Basic needs (browsing)

In other news, an email just came in on 2014-11-07 stating that there was an unexpected turn of circumstances that provided. I applied for the refund, especially. This will mean we have to look at alternate hardware while waiting for it to come in and/or develop any demo code for the EEG device earlier than expected.
