+++
title = "Language Essentials For Programmers""
+++

If you are a programmer with experience in at least one C-like language (C, C++, Java, Javascript) this chapter will hit the language highlights as quickly and with as few words as possible.  For some, this may be all you need.  For everyone, this can serve as a quick reference once you have a better understanding of how scripts work.

MSL is an interpreted language loosly based on <code>Lisp</code> but using a C-style *infix* notation for expressions.

Statements and expressions are effectively the same thing, all expressions return a value which may or may not be used by the containing expression.

### Literals

The usual string, integer, and float literals are supported.  Boolean values are represented with the keywords <code>true</code> and <code>false</false>.

Strings must be surrounded by double quotes.  There is limited support for "escape characters".  There are no character constants.

In practice, almost all literals will be small positive or negative integers and short strings.

The concept of a "null" value is supported but is not often used.  When necessary nullness is written
with the keyword <code>null</code>.

### Keywords

The language has a small number of keywords that cannot be used as the names of functions or variables.
Some of these may be abbreviated, and some are aliases of another.  

The keywords are:

* init
* variable
* var
* function
* func
* proc
* if
* else
* case
* end
* wait
* print
* echo
* trace
* context
* in
* public
* export
* global
* static
* track
* scope
* persistent
* and
* or
* not
* eq
* equal
* equals
* neq

### Context Specific Keywords

Each of the above keywords defines the beginning of a statement which may in turn allow context
specific keywords valid within that statement.   While the following keywords are allowed as object names
outside of these statements, it is recommended that you do not use them to avoid confusion.

* type
* on
* off
* low
* high
* shell
* kernel
* audio
* ui
* for
* number
* subcycle
* cycle
* loop
* beat
* bar





