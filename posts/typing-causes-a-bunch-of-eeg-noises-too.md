<!-- 
.. title: Typing causes a bunch of EEG noises too
.. slug: typing-causes-a-bunch-of-eeg-noises-too
.. date: 2015-04-26 21:22:15 UTC-07:00
.. tags: openbci,EEG
.. category: 
.. link: 
.. description: 
.. type: text
.. author: phora
-->

**[EDIT 2015-04-29]:** So I ran a few tests with my dad and had him wiggle his fingers and do typing 
without a computer screen. Turns out that after inspecting the waveforms with dad typing, 
the OpenBCI picked up on the difference between typing that has an emotional connection to 
it and normal typing. I noticed this after I asked dad to think angry, sad, and happy thoughts 
and noticed similar waveforms to the ones I saw when I was typing while doing my normal computer activities.

As the title says, apparently typing a lot causes EEG signals to trigger. The initial 
plan was to lazily tag my mood while I was browsing the internet, coding, or doing art
using the application that I wrote to live tag it so extracting the relevant data snippets
for each mood would be easy. It turns out that this plan would fail fantastically since
typing generates a lot of EEG noise. Even after the bandpass filter limiting the frequencies
to the beta and gamma frequencies using the GUI (since I wanted to test first with the GUi
to check if the connections were snug), there was a lot of activity in that range
when I started typing. This'd make grabbing the test data for the emotions hard even though
most of the activity is sedentary.
