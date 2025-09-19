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

To use the script, you must now create a *binding*.  Scripts will almost always be used with MIDI bindings, for for examples and testing, I like to use UI Buttons.  From the top menu select *Display* then *Edit Buttons*.   In the target tree open the *Scripts* item and look through the sub-items for one that has the name of the file you entered in the script editor.  Click and hold the mouse over this name, and drag it onto the table on the right.  Finally, click Save on the button editor popup window.  You should now see a button at the top of the UI with the name *HelloWorld* (or whatever file name you entered).

### The Console

You will notice that when you click this button nothing happens.  Messages from the *print* function will not appear in the UI by default, instead they sent to a special tool used for script debugging called the *Console*.  From the top menu select *Scripts* and then *MSL Console*.  The console window will pop up over the main Mobius UI.  Now click the new HelloWorld button, and you should see the words "Hello World!" added to the console window.

Return to the *Script Editor* window and change the text between the two double quotes, then click Save.   When you click the HelloWorld button you should now see the modified message in the console.

When a script is finished and working properly it will usually not contain any *print* statements.  It does what it does silently.  But if the script isn't doing what you think it should, using *print* with the console can help you understand what is going wrong.

