
# hexregexgist

How to validate Hexadecimal color codes with regex (Regular Expression)

## Summary

This is a tutorial that will cover the validating Regex Expression for a Hexadecimal code. It will break down parts of the code and what they mean and do.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

    /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

### Anchors

The anchors for this expression are both: ^ and $ -- they will be found bewteen the /'s

The starting anchor is: ^
The ending anchor is: $

### Quantifiers

There are two quanitfiers for a hexadecimal regex.
1. {6} to quantify for the length of alpha and/or numeric characters that follow the "#"
2. {3} to quanitfy for the alternative value of alpha and/or numeric characters to follow "#" 


### OR Operator

The expression will accept a length of 6 char or 3 char as valid given the "|" which behaves as the or statement

### Character Classes

The defined set of characters that wil fulfill the expression is also referred in the "Bracket Expressions" portion of this document. 

        [a-f0-9]
        
(allows lowercase characters between a-f and numbers 0-9)

### Flags

There are no flags for Hexidecimal regex validations, though 

        i
        
can be used to let the validating expression accept uppercaseletters

ex.: 
        /[a-f0-9]{3}/i 
        /[a-f0-9]{6}/i


### Grouping and Capturing

        #[a-f0-9]{6}
        #[a-f0-9]
        #[a-f0-9]{3}
        
the # is a literal character that must appear to validate a hexadecimal.

### Bracket Expressions

In the brackets for alpha characters, all lowercase characters/letters between [a-f] are accepted. 
As for the numerical portion, [0-9] are accepted numerical values.
In order to validate the regex expression inside of the brackets, "[a-f0-9]", any characters between those paramaters will not be null.

ex: [ff0089] valid or [f01] would be valid.
null would look such as, [aaaa789] or [HF33087] (the first example has 7 characters and the second has uppercase alpha characters which are not valid.

As long as the characters in the brackets match the requirement of a-f and 0-9, it will be accepted (remember there is a min qty of 3 and max of 6, as well as they need to all begin with #)

    valid: #ff0087
    valid: #000
    null: #G78
    null: #AAAAAA
    null: #aB0009
    valid: #777af1

### Greedy and Lazy Match

Given that a Hexadecimal code has a fixed value of 3 or 6 digits, the greeedy and/or lazy matches do not make too much of a difference; however, if we do want to try matching we can use the "?" to make the quanitfier lazy.

    #[a-f0-9]{3,6}?
    
this will match the shortest length of characters (which is 3) and will make a match.

### Boundaries

line boundary for Hexidecimal codes:

    ^#[a-f0-9]{3}$
    ^#[a-f0-9]{6}$
    
"^" and "$" are the bounaries for the line of the code. "^" is the beginning and "$" is the end.

### Back-references

This will allow us to reference a previously accepted code:

   ^#([a-f0-9]{6})\b.*\b\1\b
   ^#([a-f0-9]{3})\b.*\b\1\b
   
 the integer, 1, references the last code/ instance accepted in the first group, whereas \b.*\b will matcg all/any characters between the value, 1.
    
### Look-ahead and Look-behind

    look ahead: (?<=#) [#hexcode]{3,6}
    look behind: (?<!\w) [#hexcode]{3} (?!\w)
    
 The look ahead will help with specifying that the pattern needs to be followed by another pattern with a similar match of characters and lengeth in the quantifier. The look behind example provided will ensure that the preeding code matches the value of 3.
 In short, they help with recognizing patterns to get more precise validations.

## Author

Jennifer Mejia

GitHub Profile: [jjjgm](https://github.com/jjjgm)

Repository Link: [Hex Regex](https://github.com/jjjgm/hex-regex-sansrejects)



Link to the gist:
[hexregexgist.md](https://gist.github.com/jjjgm/1c61f713cde710cc1c30f66749fd0bee)
