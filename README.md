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
