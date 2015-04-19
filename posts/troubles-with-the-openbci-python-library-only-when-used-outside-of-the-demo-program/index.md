<!-- 
.. title: Troubles with the OpenBCI Python library only when used outside of the demo program
.. slug: troubles-with-the-openbci-python-library-only-when-used-outside-of-the-demo-program
.. date: 2015-04-18 19:37:28 UTC-07:00
.. tags: arduino,openbci,linux,python,rubix
.. category: 
.. link: 
.. description: 
.. type: text
.. author: phora
-->

Unfortunately, the project seems to drift farther and farther away even though
we're sure of the algorithms we will use to implement our robot. There's a [draft EEG waveform processor](https://github.com/RoboBrainz/OpenBCI_EEG_Classifier) that will most likely be using [a bandpass filter in SciPy](http://wiki.scipy.org/Cookbook/ButterworthBandpass) 
to reduce as much noise as possible from the outside by limiting the data to 
**12.5 Hz** to **30.0 Hz** for the sensors that take EEG asymmetry into account for certain emotions (like sad
evoking beta waves primarily on the left and happy evoking beta waves primarily on the right). The other sensors will most likely read facial gestures to further narrow the idenitified emotion. Alternatively, more
complex classification trends can be found at an [10-20 function map](https://sites.google.com/site/biofeedbackpages/function-map).

While we're working out the EEG classification, we've also started drafting skeleton code for the
[cart AI](https://github.com/RoboBrainz/Thought-Reactive-Robot-Friend/blob/master/ActionDBTest/ActionDBTest.ino) 
making use of the [EDB](https://code.google.com/p/arduino-edb/) library to persistently store scores for action/response pairs. Currently the available actions for the robot haven't been merged into the main code yet.

However, the draft tool for [quickly marking the OpenBCI board's data with emotion labels](https://gist.github.com/phora/331728d46e3dcd0e3200#file-manually_labeled_waveforms-py) 
is refusing to store any of the packets that're retrieved through the [OpenBCI Python API](https://github.com/OpenBCI/OpenBCI_Python). 
This is troublesome because the draft classifier uses the same library as the small tool for manually marking
the data before we store those into a folder that can be easily copied into the [Rubix A-10 board](http://smartrubix.com/start-here/) so the EEG classification data can be easily modified. 
Additionally, working with the A-10 also allows us to not worry as much about RAM constraints for processing the data.

Currently, here's the terminal output for our program.

```
python2 manually_labeled_waveforms.py /dev/ttyUSB0 
@Connecting to /dev/ttyUSB0
@Serial established...
@ADS1299 Device ID: 0x3E
@LIS3DH Device ID: 0x33
@Free RAM: 447
@$$$
Warning: Warning: Unexpected END_BYTE found <97> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <109> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <32> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <116> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <105> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <109> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <101> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <100> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <32> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <111> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <117> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <116> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <13> instead of <192>,            discarted packet with id <79>
Warning: Warning: Unexpected END_BYTE found <10> instead of <192>,            discarted packet with id <79>
```
The @'d lines only occur if the board is turned on precisely when the program starts.
After this, the program would write a file that contained none of the packets it tried to pick up.


Compare this to the terminal output from [the demonstration program that came with the library](https://github.com/OpenBCI/OpenBCI_Python/blob/master/user.py)
```
$ python2 ../OpenBCI_Python/user.py -p /dev/ttyUSB0 --add csv_collect

			USER.py

------------SETTINGS-------------
Notch filtering: True

-------INSTANTIATING BOARD-------
Connecting to /dev/ttyUSB0
Serial established...
No daisy: 8 EEG channels and 3 AUX channels at 250.0 Hz.

------------PLUGINS--------------
Found plugins: [ print ] [ udp_server ] [ csv_collect ] [ streamer_tcp ] [ sample_rate ]

Activating [ csv_collect ] plugin...
Will export CSV to: 2015-4-18_19-40-21.csv
Plugin [ csv_collect ] added to the list
--------------INFO---------------
User serial interface enabled...
View command map at http://docs.openbci.com.
Type /start to run -- and /stop before issuing new commands afterwards.
Type /exit to exit. 
Board outputs are automatically printed as: 
%  <tab>  message
$$$ signals end of message

-------------BEGIN---------------

--> /start
Warning: Skipped 158 bytes before start found
�
--> Warning: Warning: Unexpected END_BYTE found <160> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <1> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <130> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <243> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <224> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <130> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <252> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <246> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <129> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <124> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <148> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <128> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <130> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <228> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <157> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <130> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <240> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <154> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <129> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <90> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <200> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <128> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>
Warning: Warning: Unexpected END_BYTE found <0> instead of <192>,            discarted packet with id <0>

--> /exit
Warning: Stopping streaming...
Wait for buffer to flush...
Warning: Closing Serial...
Deactivating Plugins...
Closing, CSV saved to: 2015-4-18_19-40-21.csv
User.py exiting...

$ ls
total 848K
428K 2015-4-18_14-15-19.csv  4.0K CHANGELOG.md     12K open_bci_v3.pyc      4.0K plugin_interface.pyc  8.0K README.md  4.0K TODO.md  4.0K waveform_classify.py
348K 2015-4-18_19-40-21.csv   16K open_bci_v3.py  4.0K plugin_interface.py  4.0K plugins/              4.0K scripts/   8.0K user.py
```

As the output of ls shows, the data is successfully written to the file with the program that came with the library.
