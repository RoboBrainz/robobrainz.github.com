<!-- 
.. title: Running the OpenBCI GUI
.. slug: running-the-openbci-gui
.. date: 2014-12-23 11:06:04 UTC-08:00
.. tags: openbci,software,gui
.. link: 
.. description: 
.. type: text
.. author: phora
-->

We recently just tested running the OpenBCI GUI according to the [docs]().

However, what the documentation neglected to mention is that if you run the binary
from the archive without changing into the directory where it and its libraries are held,
then you will get the following output on the console and a nonfunctional GUI:

```
The font "Raleway-SemiBold.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
The font "Raleway-Regular.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
The font "Raleway-SemiBold.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
ControlP5 2.2.2 infos, comments, questions at http://www.sojamo.de/libraries/controlP5
Exception in thread "Animation Thread" java.lang.RuntimeException: java.lang.NullPointerException
	at com.jogamp.common.util.awt.AWTEDTExecutor.invoke(AWTEDTExecutor.java:58)
	at jogamp.opengl.awt.AWTThreadingPlugin.invokeOnOpenGLThread(AWTThreadingPlugin.java:103)
	at jogamp.opengl.ThreadingImpl.invokeOnOpenGLThread(ThreadingImpl.java:206)
	at javax.media.opengl.Threading.invokeOnOpenGLThread(Threading.java:172)
	at javax.media.opengl.Threading.invoke(Threading.java:191)
	at javax.media.opengl.awt.GLCanvas.display(GLCanvas.java:541)
	at processing.opengl.PJOGL.requestDraw(PJOGL.java:688)
	at processing.opengl.PGraphicsOpenGL.requestDraw(PGraphicsOpenGL.java:1651)
	at processing.core.PApplet.run(PApplet.java:2256)
	at java.lang.Thread.run(Thread.java:745)
Caused by: java.lang.NullPointerException
	at controlP5.ControlFont.checkFontSize(Unknown Source)
	at controlP5.ControlFont.<init>(Unknown Source)
	at controlP5.Label.setFont(Unknown Source)
	at controlP5.Textfield.setFont(Unknown Source)
	at OpenBCI_GUI$DataLogBox.<init>(OpenBCI_GUI.java:2892)
	at OpenBCI_GUI$ControlPanel.<init>(OpenBCI_GUI.java:2445)
	at OpenBCI_GUI.setup(OpenBCI_GUI.java:281)
	at processing.core.PApplet.handleDraw(PApplet.java:2361)
	at processing.opengl.PJOGL$PGLListener.display(PJOGL.java:862)
	at jogamp.opengl.GLDrawableHelper.displayImpl(GLDrawableHelper.java:665)
	at jogamp.opengl.GLDrawableHelper.display(GLDrawableHelper.java:649)
	at javax.media.opengl.awt.GLCanvas$10.run(GLCanvas.java:1289)
	at jogamp.opengl.GLDrawableHelper.invokeGLImpl(GLDrawableHelper.java:1119)
	at jogamp.opengl.GLDrawableHelper.invokeGL(GLDrawableHelper.java:994)
	at javax.media.opengl.awt.GLCanvas$11.run(GLCanvas.java:1300)
	at java.awt.event.InvocationEvent.dispatch(InvocationEvent.java:302)
	at java.awt.EventQueue.dispatchEventImpl(EventQueue.java:733)
	at java.awt.EventQueue.access$200(EventQueue.java:103)
	at java.awt.EventQueue$3.run(EventQueue.java:694)
	at java.awt.EventQueue$3.run(EventQueue.java:692)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$1.doIntersectionPrivilege(ProtectionDomain.java:76)
	at java.awt.EventQueue.dispatchEvent(EventQueue.java:703)
	at java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:242)
	at java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:161)
	at java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:150)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:146)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:138)
	at java.awt.EventDispatchThread.run(EventDispatchThread.java:91)
RESIZED
The font "Raleway-SemiBold.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
The font "Raleway-Regular.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
The font "Raleway-SemiBold.otf" is missing or inaccessible, make sure the URL is valid or that the file has been added to your sketch and is readable.
Exception in thread "AWT-EventQueue-0" java.lang.NullPointerException
	at controlP5.ControlFont.checkFontSize(Unknown Source)
	at controlP5.ControlFont.<init>(Unknown Source)
	at controlP5.Label.setFont(Unknown Source)
	at controlP5.Textfield.setFont(Unknown Source)
	at OpenBCI_GUI$DataLogBox.<init>(OpenBCI_GUI.java:2892)
	at OpenBCI_GUI$ControlPanel.<init>(OpenBCI_GUI.java:2445)
	at OpenBCI_GUI.setup(OpenBCI_GUI.java:281)
	at processing.core.PApplet.handleDraw(PApplet.java:2361)
	at processing.opengl.PJOGL$PGLListener.display(PJOGL.java:862)
	at jogamp.opengl.GLDrawableHelper.displayImpl(GLDrawableHelper.java:665)
	at jogamp.opengl.GLDrawableHelper.display(GLDrawableHelper.java:649)
	at javax.media.opengl.awt.GLCanvas$10.run(GLCanvas.java:1289)
	at jogamp.opengl.GLDrawableHelper.invokeGLImpl(GLDrawableHelper.java:1119)
	at jogamp.opengl.GLDrawableHelper.invokeGL(GLDrawableHelper.java:994)
	at javax.media.opengl.awt.GLCanvas$11.run(GLCanvas.java:1300)
	at javax.media.opengl.Threading.invoke(Threading.java:193)
	at javax.media.opengl.awt.GLCanvas.display(GLCanvas.java:541)
	at javax.media.opengl.awt.GLCanvas.paint(GLCanvas.java:595)
	at sun.awt.RepaintArea.paintComponent(RepaintArea.java:264)
	at sun.awt.X11.XRepaintArea.paintComponent(XRepaintArea.java:73)
	at sun.awt.RepaintArea.paint(RepaintArea.java:240)
	at sun.awt.X11.XComponentPeer.handleEvent(XComponentPeer.java:591)
	at java.awt.Component.dispatchEventImpl(Component.java:4948)
	at java.awt.Component.dispatchEvent(Component.java:4698)
	at java.awt.EventQueue.dispatchEventImpl(EventQueue.java:735)
	at java.awt.EventQueue.access$200(EventQueue.java:103)
	at java.awt.EventQueue$3.run(EventQueue.java:694)
	at java.awt.EventQueue$3.run(EventQueue.java:692)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$1.doIntersectionPrivilege(ProtectionDomain.java:76)
	at java.security.ProtectionDomain$1.doIntersectionPrivilege(ProtectionDomain.java:87)
	at java.awt.EventQueue$4.run(EventQueue.java:708)
	at java.awt.EventQueue$4.run(EventQueue.java:706)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$1.doIntersectionPrivilege(ProtectionDomain.java:76)
	at java.awt.EventQueue.dispatchEvent(EventQueue.java:705)
	at java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:242)
	at java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:161)
	at java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:150)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:146)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:138)
	at java.awt.EventDispatchThread.run(EventDispatchThread.java:91)
X11Util.Display: Shutdown (JVM shutdown: true, open (no close attempt): 1/1, reusable (open, marked uncloseable): 0, pending (open in creation order): 1)
X11Util: Open X11 Display Connections: 1
X11Util: Open[0]: NamedX11Display[:0, 0x7f79186a7620, refCount 1, unCloseable false]
```

After we ran it from the commandline in the directory where the executable was held,
we were able to run the GUI.
