+++
title = "Introduction"
weight = 1
+++

Scripts provide a powerful way to change the way Mobius behaves.  They can be used for many things, some of the most common are:

* Emulate the way footswitch buttons behave on a familiar hardware looper
* Combine a complex sequence of commands into one button press
* Buttons that do different things each time you press them
* Adjusting multiple tracks at exactly the same time
* Waiting until the loop reaches a certain state before doing something

Scripting is a complex topic that may seem intimidating at first, but it is well worth the time to learn.   Scripts may be written by others and shared, so even if you do not wish to write your own scripts, you should be familar with the ways scripts are installed and used.  Start by reviewing the examples in this introductory section to get an idea of what scripts can do and what they look like.  

### What Are Scripts?

Scripts are short text files containing instructions for Mobius to follow.  These instructions are written in a language called Mobius Scripting Language or MSL for short.  Because scripts are files, you can create them with any text editor, though the examples here will use the *Script Editor* that is built in to Mobius.  If you have used simple text editors like **Notepad** on Windows or **TextEdit** on Mac, you should be able to use the Script Editor.  You *should not* use word processors like *Word* or *Pages* to create script files.

### Where Are Scripts?

Script files are normally stored in a special folder within the Mobius installation folder.  You can keep them in other places as well, but it is recommended that you use the standard folder to make them easy to find.  If you use the Script Editor, it automatically knows where this folder is so you can let it handle the details.

For more information about how script files can be managed see the [File Management]({{% relref "../files" %}}) chapter.

### How Are Scripts?

Once you have a script file installed, you need to tell Mobius when that script should be used.  The process of using a script may be written about using several terms, I usually try to use "running a script" or "executing a script".  In some of the more technical discussions you may also see the terms "calling", "invoking", or "evaluating".  These all mean essentially the same thing.  You're making the script go.

There are two ways that scripts can be run: manual or automatic.  By far the most common way to use scripts is manual.  You do something that causes the script to run like pressing a button on a MIDI footswitch or clicking something in the user interface.

In order to use a script manually, you always create a **binding**.  A binding is the association between an external event such as a MIDI note, keyboard key, or UI button click and the script you want to run.  This is the same process that you would use to create bindings for the built-in functions like *Record* and *Overdub*.  

Automatic scripts are run as a side effect of something that happens within Mobius.  This is a complex and evolving topic that I won't go into detail about right now, but you may have seen some chatter about "event scripts" online.  The most common example of this is sending out a MIDI event to change a light on a control surface whenever Mobius goes in and out of a recording mode.

### The Examples

Read through each of the examples before diving into the other chapters.  They will introduce terminology and parts of the application you will need to know before reading the rest.









