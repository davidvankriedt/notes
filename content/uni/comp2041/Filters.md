---
title: Filters
draft: false
tags:
  - computer-science
---
 
A [[filter]] is a program that transforms a byte stream.

On UNIX systems they:
- Read bytes from their standard input or given file.
- Perform useful transformations on the stream.

```
filter < input.txt > output.txt
```

In isolation --> useful
In combination --> __VERY__ powerful

Normally used in combination via a pipeline:

```
filter1 | filter2 | ...  | filterN === filter1 --> filter2 --> ... --> filterN
```

It's a similar pattern to function composition.

```
filter data1 #OR filter < data1
```
The extract above displays two ways for a [[filter]] to read from the file data1.

[[Command line options]] give [[Filters]] variation:
- short form: `-v`
- verbose: `--example`

[[cat]] - the __simplest__ filter: Copies its input to output unchanged (identity filter)

## Regular Expressions (Regex)

[[Regex]] is a language developer for finding substrings of a string.

__Basics__:
```
a = a     # Unless there's special meaning, a character matches itself.
b* = "", b, bb, bbb, ... # matches 0 to infinite repetitions.
b+         # matches to one or more repetitions.
b{n}       # Matches to n repetitions.
p{n,m}     # Matches from n to m repetitions
p{n,}      # Matches to n or more.
p{,m}      # Matches to m or less.
pattern1 | pattern2    # Union of both patterns.
c(,c)*     # Parenthesis are used for grouping
\          # Backslash removes special meaning of following character.
```

__Regex for matching single characters:__
```
. (dot)  # Matches any single character.
[aeiou]       # For any one of a set of characters.
 
```

. (dot) - Matches any single character.
[aeiou] - For any one of a set of characters.
- shorthand [first - last], e.g. [a-z]
[^aeiou] - Anything outside of those characters.
[^X]*X - Matches any char up to and including first X.

__Anchoring Matches__:

Start of string denoted by ^
Ending of string denoted by $

"cat$" matches cat at the end of a string.
"^cat.*dog$" matches with cat and any string starting with cat and ending with dog.

---

For more [[Regex]] formation visit [regex101](https://regex101.com) and [regexr](https://regexr.com).
