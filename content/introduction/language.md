+++
title = "Language Essentials"
+++

There are a few fundamental concepts that you will need to understand in order to read and write scripts.  Anyone with some programming experience will find these concepts familiar.  But since most people that will use Mobius scripts are not programmers, it is difficult to write about scripting without using terms and jargon that some may not know.

If you are not a programmer, read through this chapter to at least become aquainted with the terms.  Early sections should be easy to understand, later sections will not, but don't worry.  They will be covered in more detail in the examples.

If you *are* a programmer, much of this will seem obvious, but I still recommend you skim it.  Some things may seem strange or "loose" compared to other languages you may know.  Keep in mind that the language was designed to be used by people that are *not* programmers.

### Characters and Lines

Scripts are files containing text characters: alphabetic letters, numeric digits, spaces, and punctation that must be organized according to a few rules.  These rules are called the language's **syntax**.

Characters are combined to form words or numbers that must be separated from each other using spaces or punctuation marks.

The file may contain multiple **lines** of text.  The end of each line is called the "line break" which is what you get when you press the *enter* or *return* key.

If you are familar with scripting in the original Mobius 2.x release, the way line breaks are treated is different in Mobius 3.   Line breaks are *not significant* in the syntax.   You can put as much as you want on a few lines, or split the code up into many lines to make it more readable.

Spaces and indentation are also not significant, except when at least one space is required to
separate words.

### Numbers

There are two types of numbers: *integer* and *float*.

An *integer* is any sequence of characters containing only the decimal digits, 0 through 9.
Integers may optionally begin with a minus character to indicate that it is negative.   Numbers
seen in Mobius scripts will *almost always* be small positive integers.

Some examples of integers:

```plaintext
  1
  -1
  256
  -128
```

A *float* is a sequence of digits that also includes the period character.  Floating point
numbers are very rarely used in MSL.  Like integers, floats may start with a minus
character to indiciate that it is negative.

Some examples of floats:

```plaintext
  1.0
  .5
  3.14159
  -0.5
  -.3
```

Programmers may wonder if *scientific notation* is allowed.  It is, but I will not be discussing
it since there is no current need for it.

### Strings

A *string* is any sequence of characters surrounded by double quotes.

```plaintext
  "this is a string"
  "123"
```

Strings are relatively rare in MSL, they are most often used to define a message you would want
displayed in the UI, or to represent a file name.

### Symbols

A *symbol* is a sequence of characters that begins with at least one alphabetic letter and contains
only letters and digits.  Symbols may contain both upper and lower case letters.  

Examples of symbols:
```plaintext
  Record
  SomethingIMadeUp
  foo
  A123
```

Symbols can be thought of as names of things you can use in a script.  Most symbols will be
the names of *functions* or *variables*.

### Keywords

A *keyword* is similar to a symbol, but they have a special meaning within the language.  They are
not names of things.  They are what programmers call "reserved words" that always mean the same thing.

Some examples of keywords:
```plaintext
  if
  else
  true
  false
  variable
  function
  wait
  in
```

Keywords are used to build complex *statements*.

### Variables

It is easiest to think of a *variable* as a type of symbol that contains a value.  It has a name and is able to hold onto a value, and this value can be looked at to make a decision, or
the value can be changed.  The value may be a number, a string, or the boolean keywords *true* and *false*.

In the main Mobius documentation, you will see the term *parameter* used for named values.   You can think of an MSL variable and a Mobius parameter as being the same thing.  There are differences but those are not worth dwelling on now.   Essentially all Mobius parameters are accessed in MSL as variables, but not all MSL variables are Mobius parameters.  This will become clearer in the examples.

### Operators and Expressions

Most programming languages need a way to express math (add, subtract) or logic (and, or).

Even non-programmers should be familar with basic math expressions like this:

```plaintext
   x + 1
   level / 2
   volume = 11
```

The characters <code>+</code>, <code>/</code>, and <code>=</code> are called *operators*.  They are special punctuation characters you combine with numbers and symbols to form *expressions*.

To avoid writing paragraphs about expression syntax, I'm going to assume everyone is familar with
basic high school math and will understand things like *operator precedence* and the use of *parenthesis*.  I'll only say that MSL does math expressions like pretty much all other languages, using <code>+=*/</code> operators, numbers, and variable names.

Logic expressions may be less familar to non-programmers, but are still commonly known.  Like most languages, MSL uses <code>||</code>, <code>&&</code> and <code>==</code>, but it also allows the more readable words *or* and *and* and *equals*.

Some examples of logic expressions:
```plaintext
  output == 127
  output equals 127
  mode == "Record" || mode == "Reset"
  mode equals "Record" or mode equals "Reset"
```

Now we get to what is often a hard thing for non-programmers to understand.  What is up with that double <code>==</code> to mean *equals*.   Why can't I just write single <code>=</code> like you see in math books?

The reason is because in almost all programming languages, the single <code>=</code> character means **assignment of a value** not **comparison to a value**.  So this...

```plaintext
  output == 127
```

...is testing whether the value of the *output* variable is equal to the number 127 while this...

```plaintext
  output = 127
```

...is **changing** the value of the *output* variable to **be** 127.

Forgetting to use <code>==</code> insteead of <code>=</code> is a common error when writing scripts, so for those new to programming I recommend you use the words <code>equal</code> or <code>equals</code> instead.  Note that either <code>equal</code> or <code>equals</code> may be used if you prefer the way one reads over the other.

### Functions

A *function* has several meanings when discussing MSL scripts, but all are fundamentally ways to make Mobius **do** something.  They are the *commands* or *actions* of Mobius.

Mobius has many functions with names like *Record*, *Overdub*, and *Reset*.  Causing that function
to happen is referred to as "running", "calling", or "executing" the function.  Outside of scripts,
you run functions by creating a *binding* between the function and a MIDI event or keyboard key.

You can also run Mobius functions within an MSL script.  To do that, you need to know the name of the Mobius function, and you would write that with an MSL symbol.

```plaintext
   Record
```

These are called the *built-in functions*.  You don't need to do anything special to use
them, every Mobius function will be automatically accessible from within a script.

You can also define your own functions whose behavior is defined with the MSL language.  These
are called *user defined functions*.    

Functions differ from *variables* in that they do not have a value that you can test and set.  Instead, they do something and *return* a result value.  This value may then be stored somewhere
or used in an expression.

Writing functions that return values is an advanced topic that will be discussed later.  Just know that when I talk about functions, they can either be the built-in Mobius functions or functions you create.

### Statements

Exactly what a *statement* is, is another thing that is hard to describe both accurately and briefly.

Think of a statement as a combination of keywords, symbols, and numbers that performs a useful action.   A script file is a list of statements, and each statement is *evaluated* in order from top to bottom.

A simple statement may be to cause the Mobius *Record* function to happen.   This statement
is written as a single symbol in the script file:

```plaintext
  Record
```  

A more complex statement would be to make *Record* happen but only if the current loop mode is "Reset".

```plaintext
  if mode equals "Reset" then Record
```

A statement often begins with a keyword such as *if* and we'll refer to that as an *if statement*.  To know what the statement does, you need to understand not only what the *if* keyword means, but how all the other words after it are used.

This is going to sound confusing, but will become clearer as you read the examples.

Statements have a beginning and an end, and it is important to understand where one statement ends and the next one begins.  Unlike other languages, line breaks are not considered *statement delimiters*.  The end of a statement is determined by whether or not it is considered *complete*, meaning it has all that it needs to do something.  To help make scripts more readable, statemments may be broken up into multiple lines with indentation.  How exactly you do this is personal preference.  Some prefer to break statements up so each component is on it's own line, and others prefer short scripts with as much on one line as possible.  

This is is an example <code>if</code> statement spread over several lines:

```plaintext
  if mode equals Reset
     Record
  else if mode equals Record
     Overdub
```

This is the same statement all on one line.

```plaintext
  if mode equals Reset Record else if mode equals Record Overdub
```

### Blocks

Often you need to group together several statements so they are all evaluated one after the other.  This is especially common when using the <code>if</code> statement.  Blocks are written using a pair of punctaion characters, the ones you will see most often are curly braces <code>{ }</code> and parenthesis <code>( )</code>.

This is an example of a *code block* within an <code>if</code> statement.

```plaintext
  if mode equals Reset {
     Record
     Reverse
  }     
```

The reason the {} block characters are necessary here will be described in detail later, for now
just know that seeing {} surrounding a group of statements is something you will see frequently.

The other common block is called an *argument block* and is used to pass extra information when you run a function.  They look like this:

```plaintext
  SelectTrack(3)
```

Argument blocks are surrounded by parenthesis and are written immediately after the name
of the function you want to call.  In this example the argument block contains the number 3
and the function *SelectTrack* uses that to know which track you want to select.

### Comments

A *comment* is a free-form line of text that you may include in the script to provide
documentation, or point out something that readers of the script need to know.  Within any line of text, if you write two forward shash characters <code>//</code> then all text after those characters on the same line are ignored.

```plaintext
//
// This script just runs the Record function
// I wrote it myself
//
Record
```

An entire line may be a comment, but you can also put comments on the same line as other statements.

```plaintext
SelectTrack(3) // this will select track number 3
```

The previous script will run the function *SelectTrack* and pass it the argument number 3, but everything after the <code>//</code> is ignored.

### Declarations

A *declaration* is used to tell the script interpreter things about how the script should be used.  They are not *statements* that cause things to happen, they just tell the system interesting things about what the script will do and how it should be shown in the UI.  Declarations start with the <code>#</code> character and are followed by a name.  The one you will see frequently is this.

```plaintext
  #name Track3
  
  SelectTrack(3)
```

The <code>#name</code> declaration is used to give the script a name that you want to see when you create a binding or a UI button.   If #name is not inccluded, then the name of the script will be the name of the file containing the script which is sometimes not what you want to see.   Using #name allows you to choose any name you want for the script.

Declarations may appear anywhere in the script, in any order, but they are usually written at the very top of the file.


  