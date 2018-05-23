# Regex Tutorial
Short Notes on Regular Expressions

The first thing to recognize when using regular expressions is that everything is essentially a character.Patterns are written to match a specific sequence of characters. Mostly normal ASCII is used, but unicode characters can also be used to match international text. Patterns created for regex are case-sensitive.<br>

Forward slash(\\) will be used to create metacharacters. Metacharacters are characters that have special meaning for regex engine.
### digits
**\d** can be used to replace any digit from 0 to 9.
All these texts will match this simple expression, as these sequences of characters have digits:
```text
ABc234adf
var g=0
```

### wildcards
As Joker in a deck of cards can represent any card, dot(.) can be used to match any character, be it alphanumeric, symbol or whitespace. This metacharacter ovverrides period. To match a period, it needs to be escaped using a slash **\\.** 

### matching specific characters
Specific character can be matched by defining them inside square brackets[]. E.g. **[abc]**. This will match only a, b or c and nothing else.
```text
match 	can 	
match 	man 	
match 	fan 	
skip 	dan 	
skip 	ran 	
skip 	pan
Corresponding regex: [cmf]a
```

### excluding specific characters
Specific characters can be excluded using square brackets and hat(^). E.g. **[^abc]** will match any character except letters a,b, or c.
```text
match 	hog 	
match 	dog 	
skip 	bog
Corresponding regex: [^b]o
```

### character ranges
If a set of sequential characters are to be denoted, inside square brackets, character range can be defined. E.g. **[a-z]** this will include any lowercase letter from a to z. Suppose you need to exclude a range of characters: E.g. **[^n-p]**. Multiple character ranges can also in included in a single bracket set. **[A-Z0-9a-z]** This includes all alphanumeric characters.

### catching repetitions
Curly braces{} are used to denote how many repetitions of a character is required. E.g. **a{3}** This denotes _a_ repeated thrice. A range of repetitions can also be declared. E.g. **a{1,3}** meaning _a_ will be matched atleast once and no more than 3 times. This notation can be used with any character or metacharacters.
```text
match 	wazzzzzup
match 	wazzzup
skip 	wazup
Corresponding regex: z{3,6}
```

### Kleene star and Kleene plus
This is a powerful concept in regular expressions with the ability to match an arbitrary number of charcaters. Let's understand the two terms through examples.
**Kleene star**: Meaning 0 or more. <br>
**\d*** => match any number of digits in the sequence, maybe zero.
**Kleene plus**: Meaning 1 or more. <br>
**\d+** => match any number of digits in the sequence, atleast one.<br><br>
These can be used with any character and metacharacters.
```text
match 	aaaabcc
match 	aabbbbc
match 	aacc
skip 	a
Corresponding regex: c+
```
### optional characters
The metacharacter question mark(?) denotes **optionality**. This metacharacter matches either zero or one of the preceding character or group. For example, the pattern **ab?c** will match either the strings "abc" or "ac" because the b is considered optional. Similar to the dot metacharacter, the question mark is a special character and it has to be escaped using a slash **\?** to match a plain question mark character in a string.
```text
match 	1 file found?
match 	2 files found?
match 	24 files found?
skip 	No files found.
Corresponding regex: \d+ files? found\?
```
### whitespaces
Whitespaces include space(\_), tab(\t), newline(\n) and carriage return(\r). Apart from these metacharacters, \s covers all whitespaces.
```text
match 	1.   abc
match 	2.	abc
match 	3.           abc
skip 	4.abc
Corresponding regex: \d\.\s+abc
```

### starting and ending
It is best practice to write as specific regular expressions as possible to ensure that false positivesdo not creep in. E.g. search for 'success' in a file also taking into account 'Error: unsuccessful attempt'. To tighten patterns, **(^)hat** and **($)dollar** signs are used to mark the start and end of a line. ***Note***: This hat sign is different from the one used earlier in this tutorial to exclude characters.
```text
match 	Mission: successful
skip 	Last Mission: unsuccessful
skip 	Next Mission: successful upon capture of target
Corresponding regex: ^Mission: successful$
```

### match groups
Regular expressions allow information extraction for further processing. This is done by defining groups of characters and capturing them using the special parentheses **(** and **)** metacharacters. Any subpattern inside a pair of parentheses will be captured as a group. For example, **^(IMG\d+\.png)$** will capture and extract the full image filename, but if extension is not required, the pattern will be **^(IMG\d+)\.png$** which only captures the part before the period.
```text
capture 	file_record_transcript.pdf 	-> file_record_transcript
capture 	file_07241999.pdf -> file_07241999
skip 	testfile_fake.pdf.tmp
Corresponding regex: ^(file.+)\.pdf$
```

### nested groups
Nested groups can be used to extract multiple layers of information. Using previous example,the filename and the picture number both can be extracted using the same pattern by writing an expression like **^(IMG(\d+))\.png$**. The nested groups are read from left to right in the pattern, with the first capture group being the contents of the first parentheses group, etc.
```text
capture 	Jan 1987 -> Jan 1987 1987
capture 	May 1969 ->	May 1969 1969
capture 	Aug 2011 ->	Aug 2011 2011
Corresponding regex: (\w+\s(\d+))
```

### conditionals
The **| (logical OR, aka. the pipe)** is used to denote different possible sets of characters. Example, "Buy more (milk|bread|juice)" will match only the strings _Buy more milk_, _Buy more bread_, or _Buy more juice_. 
```text
match 	I love cats
match 	I love dogs
skip 	I love logs
skip 	I love cogs
Corresponding regex: I love (cats|dogs)
```

### back referencing and other special characters
Back referencing varies depending on the implementation. However, many systems allow to reference captured groups by using **\0** (usually the full matched text), **\1** (group 1), **\2** (group 2), etc. For example, **"\2-\1"** to put the second captured data first, and the first captured data second.
Additionally, there is a special metacharacter \b which matches the boundary between a word and a non-word character. It's most useful in capturing entire words (for example by using the pattern \w+\b).

## Recaptulation
<table>
  <tr> <td>abc…</td><td>Letters</td> </tr>
  <tr> <td>123…</td><td>Digits</td> </tr>
  <tr> <td>\d</td><td>Any Digit</td> </tr>
  <tr> <td>\D</td><td>Any Non-digit character</td> </tr>
  <tr> <td>.</td><td>Any Character</td> </tr>
  <tr> <td>\.</td><td>Period</td> </tr>
  <tr> <td>[abc]</td><td>Only a, b, or c</td> </tr>
  <tr> <td>[^abc]</td><td>Not a, b, nor c</td> </tr>
  <tr> <td>[a-z]</td><td>Characters a to z</td> </tr>
  <tr> <td>[0-9]</td><td>Numbers 0 to 9</td> </tr>
  <tr> <td>\w</td><td>Any Alphanumeric character</td> </tr>
  <tr> <td>\W</td><td>Any Non-alphanumeric character</td> </tr>
  <tr> <td>{m}</td><td>m Repetitions</td> </tr> 
  <tr> <td>{m,n}</td><td>m to n Repetitions</td> </tr> 
  <tr> <td>*</td><td>Zero or more repetitions</td> </tr>
  <tr> <td>+</td><td>One or more repetitions</td> </tr> 
  <tr> <td>?</td><td>Optional character</td> </tr> 
  <tr> <td>\s</td><td>Any Whitespace</td> </tr>
  <tr> <td>\S</td><td>Any Non-whitespace character</td> </tr>
  <tr> <td>^…$</td><td>Starts and ends</td> </tr>
  <tr> <td>(…)</td><td>Capture Group</td> </tr>
  <tr> <td>(a(bc))</td><td>Capture Sub-group</td> </tr>
  <tr> <td>(.*)</td><td>Capture all</td> </tr>
  <tr> <td>(abc|def)</td><td>Matches abc or def</td> </tr>
</table>
