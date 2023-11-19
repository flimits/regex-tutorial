# Regular Expression Matching a Web Address

This document is a tutorial on how you can use regular expressions (a.k.a. regex) to examine if you have a properly formed web address or not.


## Summary

In short, after reading this you should be able to apply this knowledge to code your own web address regex string and no longer have an improperly formed web address.

What is a webaddress? It is a string of characters you use to enable you browser to communicate with a site somewhere to get back all the contents necessary to view and interact with the other site. An example would be to type in https://www.google.com and you will get Google's search bar and start searching. But what if you type in htttp:/w.gogole.cam ... you will get an error. After this document, you will no longer have that problem.

## Table of Contents

- [Regex Components](#regex-components)
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

### Anchors
Ah, anchors. These operators do not actually mach any characters, but only where to start within a sentence. Here are a few:
* '^' marks the beginning of the sentence where to start "^(If|The) man hit a ball". 
 * Would search for any sentence starting with either an 'If' or a 'The' string literal (followed by "man hit the ball").
* '$' marks the end of a sentence: "in a barn$" ...
 * would match a sentence that ends in "Horse and cows in a barn", but not "Was Sarah in a barn with her  horse?" because barn is at the end in the first part.

 NOTE: You would use anchors, like this /^a6.*ah$/ when looking for a specific pattern in a word element (llike if the password or user name must start with 'a6', followed by some or no characters, and end with 'ah').

### Quantifiers
A quantifier is used to define the number of characters (or expressions) you want to match. An example of this is to search for, say a 4 letter word. You could use something like \w{4} which would man, match any character string that is 4 characters long (surrounded by some non-character).

### OR Operator
There is an OR operation that you can do within regular expressions that allows you to choose between one or many sets of characters using the the '|' within the paranthesis (). Such as 
* "I am looking for a (cat|dog) that ate my pizza on the porch". This will match either a cat OR a dog. You can add multiple '|' to OR multiple sets of charactes. 

* "My web address can be found with (http|https)://somewebsite.(com|net)." 

Which could be any combination of
* http://somewebsite.com
* http://somewebsite.net
* https://somewebsite.com
* https://somewebsite.net

### Character Classes
The Character Classes are, also called "character sets", used to find one of several characters you are searcing for using the square brackes '[]'. Like if you want to find something with either and 'f' or a 'g' in part of the string, You would use the [fg], 
* "The gr[ae]y dog was had a [fg]ang that was white and black". 
This would match for either the word 'grey' or 'gray', and either a 'fang' or 'gang' in that sentence.

This is not all, there are so many more hting syou can do with the Character Class of []. You can also search for a series of different characters by using a range of characters which are denoted by using the '-' symbol. An example:
* [a-z0-9][4-6] Allows you to search for any two characters that looks like ..
 * Either a lower case character OR any number from 0 to 9 ...
 * AND any number from 4-6.
 <br>
* An example would be, it would match on 'The flight b577 leaves before flight cc33, but not after A352'. It would match on 'b5' AND '57'; then on 'c3' but not '33; would not on 'A3' (beause of capital 'A'), but would on '35' because it is 'any number' AND 'a number between 4 and 6.

Crazy things about these: the '-' symbol is only a character, if you put in in the [] by themself, otherwise might be interpreted as a range if not. Example:
* [-6a.] The '-' here is just a character (it is looking for '-' OR '6' OR 'a" OR '.', when in '[]')
* [7-9] Is a range of 7 to 9. 

### [Flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions#advanced_searching_with_flags)
The default for regular expressions is to stop after the first match and give that to you. However, if you use flags (or options) they can also provide a range or special function to a regex string. 
* Such as a 'g' flag, at the end means to iterate globally through a sentence, document or word instead of stopping at the first match.
* 'i' flag would mean to ignore case

To use them in a sentance "Jane did not like the spaghetti, because it had olives and had onions and had hotdogs in it".
* The regex of '/and had/g' would find "and had" two times. If the 'g' is removed it would match only the first instance of "and had".


### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match
Greedy matche are regex characters that can find one or more objects, indefinitely. The wildcard "*" is one such greed match. The "." would match any one character at this spot. If you put the two together, you will match everything from the '.' and on, like this:
* "I want a .*" would match anything and everything after "I want a ".

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
