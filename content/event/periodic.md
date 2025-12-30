+++
title = "Periodic Scripts"
+++

*Periodic Scripts* will be run automatically and continuously at defined intervals.  These are often used to monitor something in the system that is changing constantly such as the playback position of a loop.  Because playback position will change on every audio block, you can't use *event scripts* to detect those changes because they would running constantly which could degrade performance.  Periodic scripts are limited to running at reasonable intervals, as low as every 1/10th of a second.  TRhis is usually enough to make smooth and meaningful updates to a control surface or external display that is showing the loop position.

Periodic scripts aren't limited to just playback position, any system state that is accessible through script variables may be monitored and converted into MIDI events that update an external display.  You can even use them as an alternative to *event scripts* for detecting changes in loop modes, though event scripts are simpler and designed for that purpose.

Event scripts must be *registered* in the Session before they will start running.  Bring up the *Session Edit* window, click on the *Globals* tab, and click on the *Scripts* category.  Up to three periodic scripts may be registered, labeled *Low*, *Medium*, and *High*.

Each script may define the frequency that it runs in units of 1/10th of a second, but only the *High* script is allowed to run faster than every 1/2 second.   This is to prevent overloading the system with high frequency scripts that may degrade performance.

In order to be selected as a periodic script in the session editor, the script must declare itself as a periodic script.  This is done with the *#meta* declaration in the script body.

```plaintext
#name My Periodic Script
#meta periodic 5

```

The number after the *periodic* keyword defines the frequency of the script in 1/10th second units.  In this example 5 means it will run every 1/2 second.

The most common use case for periodic scripts is sending MIDI events to a control surface so that it may display the location of a loop that is playing.  The next example shows how to do that and makes use of a few advanced script features that may be unfamiliar.

```plaintext
#name PeriodicMidiTest

// this defines the script as a periodic script and
// sets the refresh interval to 1 tenths of a second
#meta periodic 5

// This is a track variable that remembers the last loop position
// that was analyzed
track variable lastLoopFrame = 0

// This variable remembers the last scaled value that was sent.
// Due to rounding, the same scaled value may apply over several
// periods, so avoid duplicate sends if it is the same as it was
// the last period.
track variable lastScaledSent = 0

// did the loop location change in the selected track?
if (loopFrame != lastLoopFrame) {

  // remember where we were
  lastLoopFrame = loopFrame

  // scale the loop location into a smaller range from 0 to 127
  var scaled = ScaleRange(loopFrame loopFrames 127)

  // send if the scaled down value was different than the last time
  if (scaled != lastScaledSent) {
    print("Scaled" scaled)
    lastScaledSent = scaled
  }

}
```

The first unusual feature in this script is the use of *track variables*.  A track variable is a *static* variable which means it will retain its value when the script is not running.  See the section <section> below for more information about track variables if you are unfamilar with them.

The second unusual feature is the use of the system library function *ScaleRange*.  This does some simple math to convert the loop location which may be a very large number into a smaller number that can be sent in a MIDI event.  See the section <section> below for more about this.

The final thing to note is that this example doesn't actually send any MIDI events.  It uses the *print* statement to display the results in the Script Console window.  I recommend that you try this first so you can verify that the script is actually installed and working properly before you make it generate MIDI.

Once you have this script registered as the *High* periodic script, select a track and record something into one of the loops.  As soon as the recording finishes, you should start seeing numbers scrolling by in the console window.  If you do, you win and can move on to the next step.

### Sending MIDI Events

MIDI events are sent using the library function *MidiOut*.  The MidiOut argument signature is:

```plaintext
  MidiOut(status channel number velocity)
```

The *status* argument is a string with one of these names:

```plaintext
  note
  noteon
  noteoff
  control
  cc
  program
  pgm
  start
  continue
  stop
```

In periodic scripts, *status* will usually be "control", but it will depend entirely on what
the receiving device needs.

The *channel* argument is the MIDI channel from 0 to 15.

The *numberd* argument will be the note, control, or program number from 0 to 127.

The *velocity* argument is either the note velocity if you are sending notes, or the continuous controller value if you are sending CCs.   It is not used if you are sending program change events.

Let's assume you have a control surface that will display a rectangular thermometer representing the loop position whenever it receives a CC number 42 on channel 5.  You would change the *print* statement in the original example to this:

```plaintext
  MidiOut("control" 5 42 scaled)
```

Where the event actually goes will depend on your Mobius *MIDI Devices* configuration.   If you are running standalone, you must have at least one MIDI output device configured, and it must have the **Export** box checked.

If you are running as a plugin, you may also configure a MIDI export device, but this is optional.  If there is no export device, the MIDI event will be sent to the host application, and you will need to configure the host to pass it to the MIDI device.

### ScaleRange Library Function

This function can be used to convert a value in a large range into a proportional value within
a smaller range.  It is most often used to convert loop playback locations into MIDI note or CC
values which are limited to a range of 0 to 127.

The variables *loopFrame* and *loopFrames* have values that are sample positions in the loop.  At a typical sample rate of 48000, a 4 second loop will contain 192,000 frames.  These numbers are much too large to use with MIDI events which are mostly limited to a value between 0 and 127.  What you need to do is generate a value to include in a MIDI note or CC event that represents the same proportion that the loop frame has within the loop.  For example if the loop is 192,000 frames long, and current playback frame is 96,000, this is exactly in the center of the loop.  The value in the MIDI event needs to be 64 which is in the middle of the allowable MIDI event range of 128.  The arguments to the function are:

```plaintext
   ScaleRange(inputValue inputMax resultMax)
```

In this case, we are passing *loopFrame* as the inputValue and *loopFrames* as the inputMax.  The resultMax is 127 which is the largest number that can be placed in a MIDI Note or CC event.  The return value of the function is a number between 0 and 127 that represents the same proportion that loopFrame has within loopFrames.  If you are a programmer and can't sleep until you see the actual
math, it is this:

```plaintext
        float proportion = (float)inValue / (float)inMax;
        result = (int)((float)resultMax * proportion);
```

You might be wondering if you could just write that in MSL.  Well you can't right now
because MSL doesn't do floats very well.  It may someday, but this is still a common enough
calculation I decided to add it to the standard library.

### Static and Track Variables


The first unusual feature in this script is the use of *track variables*.  A track variable is a *static* variable which means it will retain its value when the script is not running.  What makes track variables different from other static variables, is that each track maintains it's own copy of that variable.  




