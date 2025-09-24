+++
title = "Language Essentials"
+++

There are a few fundamental concepts that you will need to understand in order to read and write scripts.  Anyone with some programming experience will find these concepts familiar.  But since most people that will use Mobius scripts are not programmers, it is difficult to write about scripting without using terms and jargon that some may not know.

If you are not a programmer, I'll try to introduce terms gradually and explain in detail what they are.  The rest of the documentation will use these terms without explanation so it is important to
read the introductory sections first.

If you *are* a programmer, much of this will seem obvious, but I still recommend you skim it.  Some things may seem strange or "loose" compared to other languages you may know.  Keep in mind that the language was designed to be used by people that are *not* programmers.

### Characters and Lines

Scripts are files containing text characters: alphabetic letters, numeric digits, spaces, and punctation that must be organized according to a few rules.  These rules are commonly called the language's **syntax**.

Characters are combined to form words or numbers that must be separated from each other using spaces or punctuation marks.

The file may contain multiple **lines** of text.  The end of each line is called the "line break" which is what you get when you press the *enter* or *return* key.

### Numbers

An *integer* is any sequence of characters containing only the decimal digits, 0 through 9.
Integers may optionally begin with a minus character to indicate that it is negative.   Numbers
in MSL are *almost always* small positive integers.

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
the names of *functions* and *parameters* in Mobius.

### Keywords

A *keyword* is similar to a symbol, but it has a special meaning within the language.  They are
not names of things.  It is difficult to describe exactly what they are without descending
into jargon, but think of them as words in the language that will always mean the same thing.

MSL is a language that can be used by other applications besides Mobius.  Symbols like *Record* may mean different things in different applications.  But keywords like *if* and *else* will always mean the same thing in any application.

Some examples of keywords:
```plaintext
  if
  else
  variable
  function
  wait
  in
```

### Variables

It is easiest to think of a *variable* as a type of symbol that contains a value.  It has a name and is able to hold onto a value, and this value can be looked at to see what it is, or
the value can be changed.  The value may be a number or a string.

In the documentation, you will see the terms *variable*, *symbol*, and *parameter* used in confusing ways as if they were all the same thing.  Describing exactly what the difference between them is requires a lot of words, and is frankly rather boring.  Most of the time, you can think of an MSL variable and a Mobius parameter as being the same thing.  And a symbol is how you refer to that parameter in an MSL script.

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
basic high school math and will understand things like *operator precedence* and the use of *parenthesis*.  I'll only say that MSL does math expressions like pretty much all other languages, using <code>+=*/</code> operators and numbers.  What math writing would call a *variable* is an MSL *symbol*.

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

...is testing whether the value of the *output* is equal to the number 127 while this...

```plaintext
  output = 127
```

...is **changing** the value of the *output* to **be** 127.

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

Functions differ from *variables* or *parameters* in that they do not have a value that you can test and set.  Instead, they do something and *return* a value.  This value may then be stored somewhere
or used in an expression.

Writing functions that return values is an advanced topic that will be discussed later.  Just know that when I talk about functions, they can either be the built-in Mobius functions or ones you create.

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

### Comments

### Declarations
