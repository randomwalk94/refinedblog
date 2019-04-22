+++
title = "awk"
author = ["Kaushal Modi"]
description = "Collection of `awk` examples."
date = 2018-05-02
tags = ["awk"]
categories = ["unix"]
draft = true
creator = "Emacs 27.0.50 (Org mode 9.1.14 + ox-hugo)"
+++

<div class="ox-hugo-toc toc">
<div></div>

<div class="heading">Table of Contents</div>

- [Simple example](#simple-example)
- [The AWK Programming Language](#the-awk-programming-language)
    - [An AWK Tutorial](#an-awk-tutorial)
        - [Getting Started](#getting-started)
        - [Simple Output](#simple-output)
        - [Fancier Output](#fancier-output)
        - [Selection](#selection)
        - [Computing with AWK](#computing-with-awk)
        - [Control-Flow Statements](#control-flow-statements)

</div>
<!--endtoc-->



## Simple example {#simple-example}

```awk
BEGIN { print 42 }
```

```text
42
```


## The AWK Programming Language {#the-awk-programming-language}

This section contains awk examples and my notes from the _The AWK
Programming Language_ book by Alfred V. Aho, Brian W. Kernighan and
Peter J. Weinberger.


### An AWK Tutorial {#an-awk-tutorial}

<a id="code-snippet--emp-data"></a>
```text
Beth    4.00   0
Dan     3.75   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--emp-data">Code Snippet 1</a></span>:
  Example Input used for examples
</div>


#### Getting Started {#getting-started}

<a id="code-snippet--1-1--1"></a>
```awk
$3 > 0 { print $1, $2 * $3 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-1--1">Code Snippet 2</a></span>:
  Print total salary only for the employees who have worked for non-zero hours
</div>

```text
Kathy 40
Mark 100
Mary 121
Susie 76.5
```

The `,` between `$1` and `$2` renders as a space in the output by default. That can be changed.

<a id="code-snippet--1-1--2"></a>
```awk
$3 == 0 { print $1 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-1--2">Code Snippet 3</a></span>:
  Print employees who did not work
</div>

```text
Beth
Dan
```


##### The Structure of an AWK Program {#the-structure-of-an-awk-program}

Each awk program in this chapter is a sequence of one or more pattern-action statements:

```text
pattern { action }
pattern { action }
...
```

Either the _pattern_ or the _action_ (but not both) in a
pattern-action statement may be omitted. If a pattern has no action as
in [Code Snippet 4](#code-snippet--1-1--3), then each line that the pattern matches is printed.

<a id="code-snippet--1-1--3"></a>
```awk
$3 == 0
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-1--3">Code Snippet 4</a></span>:
  Pattern without action
</div>

```text
Beth    4.00   0
Dan     3.75   0
```

And if there is an action with no pattern, then the action is performed for every input line.

<a id="code-snippet--1-1--4"></a>
```awk
{ print $1 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-1--4">Code Snippet 5</a></span>:
  Action without pattern
</div>

```text
Beth
Dan
Kathy
Mark
Mary
Susie
```


#### Simple Output {#simple-output}


##### Printing Every Line {#printing-every-line}

<a id="code-snippet--1-2--1"></a>
```awk
{ print }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--1">Code Snippet 6</a></span>:
  Printing every line &#x2013; 1
</div>

```text
Beth    4.00   0
Dan     3.75   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```

<a id="code-snippet--1-2--2"></a>
```awk
{ print $0 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--2">Code Snippet 7</a></span>:
  Printing every line &#x2013; 2
</div>

```text
Beth    4.00   0
Dan     3.75   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```


##### Printing Certain Fields {#printing-certain-fields}

<a id="code-snippet--1-2--3"></a>
```awk
{ print $1, $3 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--3">Code Snippet 8</a></span>:
  Printing certain fields
</div>

```text
Beth 0
Dan 0
Kathy 10
Mark 20
Mary 22
Susie 18
```


##### `NF`, the Number of Fields {#nf-the-number-of-fields}

<a id="code-snippet--1-2--4"></a>
```awk
{ print NF, $1, $NF }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--4">Code Snippet 9</a></span>:
  Print number of fields, first field and <i>last field</i> for each input line
</div>

```text
3 Beth 0
3 Dan 0
3 Kathy 10
3 Mark 20
3 Mary 22
3 Susie 18
```


##### Computing and Printing {#computing-and-printing}

<a id="code-snippet--1-2--5"></a>
```awk
{ print $1, $2 * $3 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--5">Code Snippet 10</a></span>:
  Do computations on field values
</div>

```text
Beth 0
Dan 0
Kathy 40
Mark 100
Mary 121
Susie 76.5
```


##### Printing Line Numbers {#printing-line-numbers}

<a id="code-snippet--1-2--6"></a>
```awk
{ print NR, $0 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--6">Code Snippet 11</a></span>:
  <code>NR</code>, Number of lines Read
</div>

```text
1 Beth    4.00   0
2 Dan     3.75   0
3 Kathy   4.00   10
4 Mark    5.00   20
5 Mary    5.50   22
6 Susie   4.25   18
```


##### Putting Text in the Output {#putting-text-in-the-output}

<a id="code-snippet--1-2--7"></a>
```awk
{ print "total pay for", $1, "is", $2 * $3 }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-2--7">Code Snippet 12</a></span>:
  Concatenating text in the output
</div>

```text
total pay for Beth is 0
total pay for Dan is 0
total pay for Kathy is 40
total pay for Mark is 100
total pay for Mary is 121
total pay for Susie is 76.5
```


#### Fancier Output {#fancier-output}

-   The `print` statement is for quick and easy output.
-   The `printf` statement is used if you need to format the output exactly the way you want.


##### Lining Up Fields {#lining-up-fields}

With `printf`, no blanks or newlines are produced automatically; you
need to create them yourself. _Note the `\n` in the `printf` statement
in [Code Snippet 13](#code-snippet--1-3--1)._

<a id="code-snippet--1-3--1"></a>
```awk
{ printf("total pay for %s is $%.2f\n", $1, $2 * $3) }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-3--1">Code Snippet 13</a></span>:
  <code>printf</code> example
</div>

```text
total pay for Beth is $0.00
total pay for Dan is $0.00
total pay for Kathy is $40.00
total pay for Mark is $100.00
total pay for Mary is $121.00
total pay for Susie is $76.50
```

<a id="code-snippet--1-3--2"></a>
```awk
{ printf("%-8s $%6.2f\n", $1, $2 * $3) }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-3--2">Code Snippet 14</a></span>:
  Justification using <code>printf</code>
</div>

```text
Beth     $  0.00
Dan      $  0.00
Kathy    $ 40.00
Mark     $100.00
Mary     $121.00
Susie    $ 76.50
```


#### Selection {#selection}


##### Selection by Comparison {#selection-by-comparison}

<a id="code-snippet--1-4--1"></a>
```awk
$2 >= 5
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--1">Code Snippet 15</a></span>:
  awk program with just a comparison pattern
</div>

```text
Mark    5.00   20
Mary    5.50   22
```


##### Selection by Computation {#selection-by-computation}

<a id="code-snippet--1-4--2"></a>
```awk
$2 * $3 > 50 { printf("$%.2f for %s\n", $2 * $3, $1) }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--2">Code Snippet 16</a></span>:
  Print details only for employees making more than $50
</div>

```text
$100.00 for Mark
$121.00 for Mary
$76.50 for Susie
```


##### Selection by Text Content {#selection-by-text-content}

<a id="code-snippet--1-4--3"></a>
```awk
$1 == "Susie"
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--3">Code Snippet 17</a></span>:
  Literal string match
</div>

```text
Susie   4.25   18
```

<a id="code-snippet--1-4--3--2"></a>
```awk
/y/
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--3--2">Code Snippet 18</a></span>:
  Regular expression match &#x2013; 1
</div>

```text
Kathy   4.00   10
Mary    5.50   22
```

It looks like regular expressions cannot be specified in relation to
field variables like `$1`, `$2`, etc. But I am most likely wrong. For
instance, the `/y.*4/` in [Code Snippet 19](#code-snippet--1-4--3--3) does a match across fields.

<a id="code-snippet--1-4--3--3"></a>
```awk
/y.*4/
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--3--3">Code Snippet 19</a></span>:
  Regular expression match &#x2013; 2
</div>

```text
Kathy   4.00   10
```


##### Combinations of Patterns {#combinations-of-patterns}

Patterns can be combined with parentheses and the logic operators `&&` (_and_), `||` (_or_) and `!` (_not_).

<a id="code-snippet--1-4--4"></a>
```awk
$2 >= 4 || $3 >= 20
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--4">Code Snippet 20</a></span>:
  Logical operators in patterns
</div>

```text
Beth    4.00   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```

Above, the lines that match both `$2>=4` and `$3>=20` conditions are
printed just once. But in the case of [Code Snippet 21](#code-snippet--1-4--5), where _multiple_
patterns are specified, the program prints a line twice if that line
matches both the conditions.

<a id="code-snippet--1-4--5"></a>
```awk
$2 >= 4
$3 >= 20
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--5">Code Snippet 21</a></span>:
  Multiple patterns
</div>

```text
Beth    4.00   0
Kathy   4.00   10
Mark    5.00   20
Mark    5.00   20
Mary    5.50   22
Mary    5.50   22
Susie   4.25   18
```

[Code Snippet 22](#code-snippet--1-4--6) is a De Morgan's law variant of [Code Snippet 20](#code-snippet--1-4--4). Note that
the results are the exact same.

<a id="code-snippet--1-4--6"></a>
```awk
!($2 < 4 && $3 < 20)
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--6">Code Snippet 22</a></span>:
  Logical operators in patterns
</div>

```text
Beth    4.00   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```


##### Data Validation {#data-validation}

When doing data validation, the lines are printed only when they do not match the desirable properties. Think of this use as that of assertions in SystemVerilog. Below, as any of the lines in the example input do not match the failure conditions, there is no output.

<a id="code-snippet--1-4--7"></a>
```awk
NF != 3   { print $0, "number of fields is not equal to 3" }
$2 < 3.35 { print $0, "rate is below minimum wage" }
$2 > 10   { print $0, "rate exceeds $10 per hour" }
$3 < 0    { print $0, "negative hours worked" }
$3 > 60   { print $0, "too many hours worked" }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--7">Code Snippet 23</a></span>:
  Data validation or Assertions
</div>


##### BEGIN and END {#begin-and-end}

-   The special pattern `BEGIN` matches **before the first line** of the first input file is read.
-   `END` matches **after the last line** of the last file has been processed.

<a id="code-snippet--1-4--8"></a>
```awk
BEGIN { print "NAME    RATE   HOURS"; print "" }
      { print }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-4--8">Code Snippet 24</a></span>:
  Using <code>BEGIN</code> to print heading
</div>

```text
NAME    RATE   HOURS

Beth    4.00   0
Dan     3.75   0
Kathy   4.00   10
Mark    5.00   20
Mary    5.50   22
Susie   4.25   18
```

As noted from [Code Snippet 24](#code-snippet--1-4--8),

-   You can put several statements on a single line if you separate them by semi-colons.
-   The `print ""` prints a blank line.
-   Plain `print` prints the **whole** line.


#### Computing with AWK {#computing-with-awk}


##### Counting {#counting}

-   The user-created variables are not declared; you just use them.
-   The default initial value of variables used as numbers (`awk` auto-detects that) is 0.

<a id="code-snippet--1-5--1"></a>
```awk
$3 > 15 { emp = emp + 1 }
END     { print emp, "employees worked more than 15 hours" }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--1">Code Snippet 25</a></span>:
  User-created variables
</div>

```text
3 employees worked more than 15 hours
```


##### Computing Sums and Averages {#computing-sums-and-averages}

<a id="code-snippet--1-5--2"></a>
```awk
END { print NR, "employees" }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--2">Code Snippet 26</a></span>:
  Print the number of lines
</div>

```text
6 employees
```

<a id="code-snippet--1-5--3"></a>
```awk
    { pay = pay + $2 * $3 } # Nothing is printed by this line; only calculation happens
END { print NR, "employees"
      print "total pay is", pay
      print "average pay is", pay/NR
    }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--3">Code Snippet 27</a></span>:
  Using <code>NR</code> to compute the average pay
</div>

```text
6 employees
total pay is 337.5
average pay is 56.25
```


##### Handling Text {#handling-text}

<a id="code-snippet--1-5--4"></a>
```awk
$2 > maxrate { maxrate = $2; maxemp = $1 } # Here maxrate and maxemp variables are updated conditionally; nothing is printed
END          { print "highest hourly rate:", maxrate, "for", maxemp }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--4">Code Snippet 28</a></span>:
  Find the employee who is paid the most per hour
</div>

```text
highest hourly rate: 5.50 for Mary
```


##### String Concatenation {#string-concatenation}

<a id="code-snippet--1-5--5"></a>
```awk
    { names = names $1 " " }
END { print names }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--5">Code Snippet 29</a></span>:
  Concatenate strings with spaces in-between
</div>

```text
Beth Dan Kathy Mark Mary Susie
```

Awk automagically figures out that here the `names` variable is used to hold string and sets its initial value to a _null_ or empty string.


##### Printing the Last Input Line {#printing-the-last-input-line}

-   Although `NR` retains its values in an `END` action, `$0` **does not**.

So in the below code snippet, we use a user-defined variable `last` to store the `$0` value of the last line read.

<a id="code-snippet--1-5--6"></a>
```awk
    { last = $0 }
END { print last }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--6">Code Snippet 30</a></span>:
  Print the last line
</div>

```text
Susie   4.25   18
```


##### Built-in Functions {#built-in-functions}

<a id="code-snippet--1-5--7"></a>
```awk
{ print $1, length($1) }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--7">Code Snippet 31</a></span>:
  In-built function <code>length</code>
</div>

```text
Beth 4
Dan 3
Kathy 5
Mark 4
Mary 4
Susie 5
```


##### Counting Lines, Words and Characters {#counting-lines-words-and-characters}

<a id="code-snippet--1-5--8"></a>
```awk
    { nc = nc + length($0) + 1 # the trailing "+ 1" is to count the newline character for each line
                               # $0 does not include the newline
      nw = nw + NF
    }
END { print NR, "lines", nw, "words", nc, "characters" }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-5--8">Code Snippet 32</a></span>:
  Count lines, words, chars
</div>

```text
6 lines 18 words 106 characters
```


#### Control-Flow Statements {#control-flow-statements}

**The control flow statements can be used only in actions.**


##### If-Else Statement {#if-else-statement}

[Code Snippet 33](#code-snippet--1-6--1) is similar to [Code Snippet 27](#code-snippet--1-5--3), but with an `if` to protect
against division by zero when computing average.

<a id="code-snippet--1-6--1"></a>
```awk
$2 > 6 { n = n + 1; pay = pay + $2 * $3 }
END    { if (n > 0)
           printf("%d employees, total pay is %.2f, average pay is %.2f",
                  n, pay, pay/n) # Note that we can continue a long statement over several lines
                                 # by breaking it after a comma.
         else
           print "no employees are paid more than $6/hour"
       }
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-6--1">Code Snippet 33</a></span>:
  Sum and average pay of employees making more than $6/hr
</div>

```text
no employees are paid more than $6/hour
```


##### While Statement {#while-statement}

<a id="table--interest1-inp"></a>
<div class="table-caption">
  <span class="table-number"><a href="#table--interest1-inp">Table 1</a></span>:
  Input for interest1 program
</div>

| 1000 | .06 | 5 |
|------|-----|---|
| 1000 | .12 | 7 |

<a id="code-snippet--1-6--2"></a>
```awk
# interest1 - compute compound interest
#  input: amount rate years
#  output: compounded value at the end of each year
{ i = 1
  printf("Amount = %.2f, Rate = %.2f, Years = %.2f\n", $1, $2, $3)
  while (i <= $3) {
    printf("\tYear %d: %.2f\n", i, $1 * (1 + $2) ^ i)
    i = i + 1
  }
  print ""
}
```

<div class="src-block-caption">
  <span class="src-block-number"><a href="#code-snippet--1-6--2">Code Snippet 34</a></span>:
  Calculate compound interest
</div>

```text
Amount = 1000.00, Rate = 0.06, Years = 5.00
	Year 1: 1060.00
	Year 2: 1123.60
	Year 3: 1191.02
	Year 4: 1262.48
	Year 5: 1338.23

Amount = 1000.00, Rate = 0.12, Years = 7.00
	Year 1: 1120.00
	Year 2: 1254.40
	Year 3: 1404.93
	Year 4: 1573.52
	Year 5: 1762.34
	Year 6: 1973.82
	Year 7: 2210.68

```

[//]: # "Exported with love from a post written in Org mode"
[//]: # "- https://github.com/kaushalmodi/ox-hugo"

