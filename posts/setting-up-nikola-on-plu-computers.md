<!-- 
.. title: Setting up Nikola on PLU computers
.. slug: setting-up-nikola-on-plu-computers
.. date: 2014-10-09 16:38:18 UTC-07:00
.. tags: PLU computers,nikola,python,python3
.. link: 
.. description: 
.. type: text
-->

We set up our site for our github page last night using a Linux computer that already had nikola installed. Since we also needed to work on the site at school, we also had to set nikola up on school computers. To do this, we had to run the following commands:

1. Install most of the dependencies using pip
```\Python34\Scripts\pip install --root=/path/to/destdir nikola```
1. Install nikola using the [github version](https://github.com/getnikola/nikola)
1. [Edit C:\Python34\Lib\distutils\msvc9compiler.py at line 294 to hardcode 12.0 as the MSVC version](http://stackoverflow.com/a/23397327)
1. [Remove all instances of -mcygwin from C:\Python34\Lib\distutils\cygwinccompiler.py](http://stackoverflow.com/a/6035864)
1. Install lxml using [the official instructions for MS Windows](http://lxml.de/installation.html) and specify the path to install like in step 1.
1. Install blinker, six, markupsafe, logbook, natsort, yapsy, and pyrss2gen manually with pip
1. Construct a shell script file to automagically set environment variables to make manually copying nikola to a location where the executable can be run a lot less painful (as in, no need to type out extremely long path names): 
~~~
if test -d /cygdrive;then
	#export PYPREFIX="/cygdrive/x/Apps/pylibs"
	export PYPREFIX="/cygdrive/c/Users/PLUCSCE/Downloads/pylibs"
else
	#export PYPREFIX="/x/Apps/pylibs"
	export PYPREFIX="/c/Users/PLUCSCE/Downloads/pylibs"
fi

export PYTHONPATH="${PYPREFIX}/Python34:${PYPREFIX}/Python34/lib:${PYPREFIX}/Python34/lib/site-packages"
export PATH="${PYPREFIX}/Python34/Scripts:${PATH}"
~~~

With the installation complete, all we had to do was keep a copy on our x drives before copying it to the Downloads folder and source the script file before continuing to work with our site.