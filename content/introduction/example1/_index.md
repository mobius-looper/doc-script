+++
title = "1: Hello World"
+++

The first example will not be musically useful, but it covers several important
topics you should understand in order to use and write scripts.

* The Script Editor to write and install scripts
* The Binding Editors to create bindings to run scripts
* The Mobius Console to see what scripts are doing

Whether you write your own scripts, or get them from somone else, you will need to 
install them into Mobius.  There are several ways to do this, in this example
we will use the *Script Editor*.  To start, we need a script.  If you have any experience
with programming languages you will know that we are required by law to begin with
an example affectionally known as *Hello World*.

Here is such a script:

```
print "Hello World!"
```

### Script Editor

I won't be describing what those words mean just yet, for now let's focus on how to get
this script into Mobius and make it do something.   First bring up the *Script Editor*.  Go to the top menu and select the *Scripts* item, then select *Script Editor*.  The script editor window will pop up to the side of the main Mobius window.

At the bottom of the script editor is a row of buttons, click *New*.  The large area in the center is where you will put the body of the script. It is a simple text editor that should behave like Notepad on Windows or TextEdit on Mac.  When you have finished entering the script text, click the *Compile* button at the bottom.   Between the text area and the button row is an area for messages, you should see the message "Compile Sucessful".  Now click the *Save* button.

At this point, you should see a standard file saving dialog window pop up.  There is more to say about this, but for now, just understand that scripts must be saved in files on the file system, and those files must be given a name.  The file will be stored in a special folder within the Mobius installation folder, *do not* change the destination folder, only enter a file name.   The name can be anything as long as it is unique within this folder.  Assuming you have not yet installed any scripts, enter the name "HelloWorld" and click the Save button on the file chooser window.  The script is now installed and ready for use.

### Bindings

To use the script, you must now create a *binding*.  Scripts will almost always be used with MIDI bindings, but for examples and testing, I like to use UI Buttons.  From the top menu select *Display* then *Edit Buttons*.   In the target tree open the *Scripts* item and look through the sub-items for one that has the name of the file you entered in the script editor.  Click and hold the mouse over this name, and drag it onto the table on the right.  Finally, click Save on the button editor popup window.  You should now see a button at the top of the UI with the name *HelloWorld* (or whatever file name you entered).

### The Console

You will notice that when you click this button nothing happens.  Messages from the *print* function will not appear in the UI by default, instead they sent to a special tool used for script debugging called the *Console*.  From the top menu select *Scripts* and then *MSL Console*.  The console window will pop up over the main Mobius UI.  Now click the new HelloWorld button, and you should see the words "Hello World!" added to the console window.

Return to the *Script Editor* window and change the text between the two double quotes, then click Save.   When you click the HelloWorld button you should now see the modified message in the console.

When a script is finished and working properly it will usually not contain any *print* statements.  It does what it does silently.  But if the script isn't doing what you think it should, using *print* with the console can help you understand what is going wrong.

### More Fun With Print

This simple script contains a single line.  The first part is the word *print* which is the name of a built-in function.  The second part is a text string surrounded by double quotes, this is called the *argument* to the function.  The *print* function will take whatever it is given as an argument and display it in the console window.

A sequence of characters surrounded by double quotes is called a *literal string* or simply a *string*.  It is *literal* because exactly this sequence of characters is what will be displayed.

If you forgot the quotes and did this instead:

```
print Hello World!
```

You would see errors when you compile the script.  This is because words that are not surrounded by quotes are called *symbols*.  When *print* is given an argument that is a symbol, it will display the *value* of the symbol, not the symbol name.  Since there is nothing in the system with the name *Hello*, the symbol is *unresolved* and will cause an error. 

There are many symbols defined in Mobius that you can reference in a script.  All configuration parameters you can set in the *Session Editor* are accessible as script symbols.  There are also many *system variables* that hold information about what Mobius is doing when the script runs.  Here's a simple example:

```
print trackNumber
```

*trackNumber* is the name of a system variable whose value is the number of the active track.  The active track (sometimes called the *focused* track) is the one that has a white box drawn around it in the UI.  Change the example script we've been working on and replace *"Hello World!"* with *trackNumber* and run the script.  You should see a number being added to the console window.  Now click on a different track to make it active and run the script again, the script will print a different number in the console.

As you start writing more complex scripts, you might have several things you want to print and just seeing raw numbers in the console can be confusing.  You can combine variable values with literal text to add more context to your console messages.

```
print "I am in track"
print trackNumber
```

Assuming the first track is active, this would display

```
I am in track
1
```

That's all well and good, but it would look nicer if the text and the number were displayed on the same line.  Let's improve the script like this:

```
print ("I am in track" trackNumber)
```

Note the addition of the parenthesis around the two things we want to print.   This is an *argument block*.   Argument blocks are used when you need to pass more than one thing to a function.  The *print* function will accept any number of arguments, it will merge them all into a single line of text and display the result.  Now the script will display this in the console:

```
I am in track 1
```

Here is a longer argument block containing four things to say:

```
print ("I am in track" trackNumber "and the loop mode is" mode)
```

### Why Would I Want Any Of this?

As you start writing more complex scripts, it is easy to misspell a name or make an error that
causes the script to either not do anything, or do something you don't expect.  Putting *print*
statements in between the lines of your script can help you see what decisions the script is making
when it runs.

If you don't see any *print* results in the console, it could mean that the binding is wrong, or the script file was moved or deleted accidentally.

Among programmers, using *print* statements like this is called "debug logging" and is a common
technique to find problems in a program.  One day Mobius may have fancy debugging tools like the
grown up languages use, but until then, *print* is your friend.

Debugging techniques are discussed in more detail in later chapters.

























