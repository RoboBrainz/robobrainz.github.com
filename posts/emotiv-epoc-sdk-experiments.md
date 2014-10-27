<!-- 
.. title: Emotiv EPOC SDK Experiments
.. slug: emotiv-epoc-sdk-experiments
.. date: 2014-10-26 14:58:12 UTC-07:00
.. tags: emotiv,sdk,linux,usability
.. link: 
.. description: 
.. type: text
.. author: phora
-->

So I started playing around with the SDK and the SDK's provided tools. I've kept some [screenshots](/galleries/Emotiv_EPOC_SDK/) to highlight some of the usability problems I encountered. The first two screenshots highlight aesthetic usability issues in EmoComposer since it tries to stick out with its widgets. The same could be said for the EmotivControlPanel, which also sticks out due to the custom styling on the buttons and other widgets. While I do have experience with writing [Qt Style Sheets](http://qt-project.org/doc/qt-4.8/stylesheet.html) and the EmotivControlPanel even supports loading a custom stylesheet, this functionality is useless without documenting the widgets used to construct the interface. I'd recommend the Emotiv developers document what widgets the users need to write the stylesheets for for their SDK tools and/or remove all custom styling except for the custom widgets should they stick with a proprietary model. Personally, I'd prefer a combination of both so the Emotiv developers can keep their custom styling with a stylesheet, but allow the users to turn this off in case they can't easily read the interface.

Other than that, the EmotivControlPanel works just as expected when tested with the EmoComposer, even though I frequently confused the "Push Skill" slider with carrying out the "Push" outside of training mode for the Affectiv Suite. The documentation does not mention that the EmoComposer can't save user profiles to it. Trying to do so will cause the EmotivControlPanel to freeze, requiring the user to manually kill the application.

Surprisingly, the EmoKey and the TestBench software don't stick out as much. The only issues I encountered with it were not triggering when the blink button was pressed in EmoComposer, not fully closing even after "Quit" is clicked on the system tray (which again, requires the application to be killed manually), and not launching keybindings such as Alt+F3 (which brings up the window management menu for me) and Ctrl+Space (which launches Kupfer). Even with the QListView's row coloring, the custom colors are done correctly since it defines both a foreground color and a background color. This makes the software more accessible to people with unusual color schemes.

I haven't been able to test the TestBench software since it has no ability to connect with the EmoComposer. Hopefully this'll change in the future, but I don't know what changes will be necessary to do this. At least it closes properly when Application → Quit is selected.

I will also be documenting any experiences I have with Emotiv's developers in the future. So far, the support's been pretty responsive.
