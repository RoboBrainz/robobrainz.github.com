<!-- 
.. title: Installing the Emotiv SDK
.. slug: installing-the-emotiv-sdk
.. date: 2014-10-18 12:20:54 UTC-07:00
.. tags: emotiv,sdk,please package properly,requirements,PKGBUILD,linux
.. link: 
.. description: 
.. type: text
-->

So we ordered the device this Saturday after the scholarship money came in... which'll take about two weeks from today. In the mean time, Joan downloaded the SDK to see how it's installed. Judging by a certain [forum post on Emotiv's forums](http://emotiv.co/forum/messages/forum15/topic3749/message17131/?sphrase_id=7902#message17131), I wasn't the only one shocked by how they provided the packaging. They provided an installer that downloads an installer to do the actual installer in an unsafe manner. Thankfully I knew enough about packaging to wrap it up in a much saner manner. You can find the PKGBUILD [here](https://github.com/RoboBrainz/Emotiv-Epoc-SDK-PKGBUILDs).

On my list of things to do is to minimize the references to extra copies of the libraries as much as possible. Second on my list of things to do is to make a proper *.spec file for Fedora installs.
