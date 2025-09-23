+++
title = "Language Essentials"
+++

There are a few fundamental syntax elements that you need to understand in order to read or write scripts.

For non-programmers "syntax" means the way that the text in a script file must be organized to form words, numbers, lines, and what certaion punctuation characters mean.

### Numbers

An *integer* is any sequence of characters containing only decimal digits, 0 through 9.  Integers may 
optionally begin with a minus character to indicate that it is negative.   Numbers in MSL are *almost
always* small positive integers.

Some examples of integers:

```plaintext
  1
  -1
  256
  -128
```

A *float* is a sequence of digits that also includes the period or "dot" character.  Floating point
numbers are very rarely used in MSL.  Like integers, floats may be immediately preceeded by a minus
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
it since it has no current use.

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
only letters and digits.  Strings may contain both upper and lower case letters.  

Examples of symbols:
```plaintext
  Record
  SomethingIMadeUp
  foo
  A123
```



  


### Keywords

### Spaces and Lines

### Blocks

### Operators

