<!-- 
.. title: Advisor Meeting 1
.. slug: advisor-meeting-1
.. date: 2014-10-20 10:59:13 UTC-07:00
.. tags: emotiv,sdk,faculty meeting,robot,requirements,linux,robot parts,nikola
.. link: 
.. description: 
.. type: text
.. author: phora
-->

We met with our advisor today from 10:20-10:50 and reported our progress. Here were the major points of the meeting:
# Joan
* Packaged the Fedora version of the Research SDK for Arch Linux.
* Found the most of the dependencies for the SDK. Still don't know what package provides libmkl_rt.
* Emailed the support team about the packaging of the SDK so the developer team could fix this.
* There's a fake data generator in the SDK lite for Windows and Mac (That's free!). So try to find the equivalent in the Linux SDK version.
* Finish work on not referencing the static copies of the library when possible.
* Found a bug in nikola\plugins\task\sitemap\__init__.py. It wasn't checking if directories were directories in a cross-platform manner. Will report this to the developers with an official patch.

# Drew
* Order the parts from SparkFun.
* Chassis has built in motors.
* We may need a separate shield for driving the wheels?
* Probably going to drive the motors with DC.
* Settled on multicolor LEDs because single color LEDs can get confusing for debugging.
