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

---

##### grep

It stands for "Globally search with Regular Expressions and Print". It copies stdout lined that match the specified regular expression.

###### Useful options:
`-E` use extended regex syntax (almost always needed to use regex syntax)
`-i` ignore case
`-v` only display lines that don't match the pattern
`-c` print count of matching lines
`-w` only match if it makes a complete word
`-x` only match if it makes a complete line

##### wc

It stands for "Word Count". It summarises its input as a single line.

###### Useful options:
`-c` print char num
`-w` print word num
`-l` print line num

By default, it prints the number of lines, words, and characters.

##### tr

It stands for transliterate characters. It reads & write characters, mapping some characters with others.

`tr [sourceChars] [destChars]`

__Example:__
`tr 'abc' '123' < someText`

In this case a-->1, b-->2, c-->3.

If there isn't enough characters in destChars to map all characters from sourceChars, the last character in destChars is simply repeated for any outstanding characters.

###### Useful options:
`-d` delete all characters that are in sourceChars

Since __tr__ is so old, file reading isn't supported, so it only uses stdin for input. This means when using it to read a file, we have to do it like `tr [sourceChars] [destChars] < file1.txt`

##### head
Prints the first n lines of input.

##### tail
Prints the last n lines of input.

###### Options for head & tail:
`-n` changes the number of lines they print (10 lines by default). `tail -n 30 file` would print the last 30 lines of "file".

Combine them for a range of lines:
`head -n 100 | tail -n 20` would print lines 81-100.

##### cut

It is a vertical slicer, it prints selected parts of input lines. It can select fields in a table, where it would separate columns by tab (default). It can also select a range of character positions.

###### Useful options:
`-f[listofCols]` print only specified fields (tab separated) on output
`-c[listofCols]` print only characters in specified columns
`-d[c]` use the character 'c' as the field separator

Lists in this case can be specified as ranges (e.g. 1-5) or comma-separated (e.g. 2, 4, 5).

##### sort

It copies input to output but ensures that output is arranged in some particular order of lines.

###### Useful options:
`-r` reverse sort
`-n` sort numerically instead of lexicographically (default)
`-d` dictionary order
`-tc` use character 'c' to separate columns
`-kn` sort on column n


##### uniq

It removes all but one copy of adjacent identical lines. It is typically used after __sort__, since that filter would make all copies adjacent to each other.

###### Useful options:
`-c` print number of duplicates
`-d` only print the duplicates (one copy)
`-u` only print lines that occur uniquely


