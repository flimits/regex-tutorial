# Regular Expression Matching a Web Address

This document is a tutorial on how you can use regular expressions (a.k.a. regex) to examine if you have a properly formed web address or not.

NOTE: For examples below, we are going to assume i'm looking for a simple HTML site like https://www.google.com, unless otherwise stated. Also, the javascript matching statement will be something like

let simpleUrl = "http://www.google.com";
let simpleRegex = /\w+/g; // Change this line
let result = simpleUrl.match(simpleRegex);
console.log(result)

Where you will be updating what is in in between the '/ / 'on the right of the '=.'


## Summary

In short, after reading this you should be able to apply this knowledge to code your own web address regex string and no longer have an improperly formed web address.

What is a web-address? It is a string of characters you use to enable you browser to communicate with a site somewhere to get back all the contents necessary to view and interact with the other site. An example would be to type in https://www.google.com and you will get Google's search bar and start searching. But what if you type in http:/www.google.cam ... you will get an error. After this document, you will no longer have that problem.

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
* '^' marks the beginning of the sentence where to start "/^(If|The) man hit a ball/". 
 * Would search for any sentence starting with either an 'If' or a 'The' string literal (followed by "man hit the ball").
* '$' marks the end of a sentence: "/in a barn\$/" ...
 * would match a sentence that ends in "Horse and cows in a barn", but not "Was Sarah in a barn with her  horse?" because barn is at the end in the first part.

 NOTE: You would use anchors, like this /^a6.*ah\$/ when looking for a specific pattern in a word element (like if the password or user name must start with 'a6', followed by some or no characters, and end with 'ah').

### Quantifiers
A quantifier is used to define the number of characters (or expressions) you want to match. An example of this is to search for, say a 4 letter word. You could use something like /\w{4}/ which would man, match any character string that is 4 characters long (surrounded by some non-character).

### OR Operator
There is an OR operation that you can do within regular expressions that allows you to choose between one or many sets of characters using the the '|' within the parenthesis (). Such as 
* "I am looking for a (cat|dog) that ate my pizza on the porch". This will match either a cat OR a dog. You can add multiple '|' to OR multiple sets of characters. 

* "My web address can be found with (http|https)://somewebsite.(com|net)." 

Which could be any combination of
* http://somewebsite.com
* http://somewebsite.net
* https://somewebsite.com
* https://somewebsite.net

### Character Classes
The Character Classes are, also called "character sets", used to find one of several characters you are searching for using the square brackets '[]'. Like if you want to find something with either and 'f' or a 'g' in part of the string, You would use the [fg], 
* "The gr[ae]y dog was had a [fg]ang that was white and black". 
This would match for either the word 'grey' or 'gray', and either a 'fang' or 'gang' in that sentence.

This is not all, there are so many more things you can do with the Character Class of []. You can also search for a series of different characters by using a range of characters which are denoted by using the '-' symbol. An example:
* [a-z0-9][4-6] Allows you to search for any two characters that looks like ..
 * Either a lower case character OR any number from 0 to 9 ...
 * AND any number from 4-6.
 <br>
* An example would be, it would match on 'The flight b577 leaves before flight cc33, but not after A352'. It would match on 'b5' AND '57'; then on 'c3' but not '33; would not on 'A3' (because of capital 'A'), but would on '35' because it is 'any number' AND 'a number between 4 and 6.

Crazy things about these: the '-' symbol is only a character, if you put in in the [] by themselves, otherwise might be interpreted as a range if not. Example:
* [-6a.] The '-' here is just a character (it is looking for '-' OR '6' OR 'a" OR '.', when in '[]')
* [7-9] Is a range of 7 to 9. 

### [Flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions#advanced_searching_with_flags)
The default for regular expressions is to stop after the first match and give that to you. However, if you use flags (or options) they can also provide a range or special function to a regex string. 
* Such as a 'g' flag, at the end means to iterate globally through a sentence, document or word instead of stopping at the first match.
* 'i' flag would mean to ignore case

To use them in a sentence "Jane did not like the spaghetti, because it had olives and had onions and had hotdogs in it".
* The regex of '/and had/g' would find "and had" two times. If the 'g' is removed it would match only the first instance of "and had".


### Grouping and Capturing

Grouping is a way  to take a full match of "something" you were searching for, and then breaking it down into smaller sub groups you can do "something" with it: matches, or searches ... etc. The first group is numbered 1; the second is 2, and so on. As an example, if you just take a url "http://www.google.com", the first group match if ```(\w{4}:\/\/\w+\.\w+\.\w+)``` is considered group 1. If you added parenthesis around each section of it, then you would for a group 2, and a group 3 within the first group: 
* ```(\w{4}:\/\/\w+\.\w+\.\w+)``` is group 1
* ```(\w{4}:\/\/(\w+\).(\w+\).(\w+))```  you would then be adding group 2, which is "www", then group 3, which is "google" and so on.

### Bracket Expressions

In this section, we will look at '[],' '{}' and '()' and how they operate in regex.

1. Brackets '[]' a character or set of characters to match. A hyphen (-) used in here represents a series (as explained above in character class). Thus, /[a-z]/ would represent to match one of the letters 'a' to 'z'. And if you use the caret '^' in the brackets at the beginning, it means to NOT, or negate the search. So ... "anything except what is in here" (like /[^a-z] would mean any character except either 'a' to 'z' characters)
2. Curly braces '{}' are used to specify an exact amount of things to search for, like 3 of something or 6 of something. Lets say you are searching for a repeating number of '10' 3 times, then you'd use /10{3}/ and it would match something like 5620.7661.31010108 (which is 101010).
3. The parentheses '()' refers to a block of something you can match on, and can contain all kinds of meta and literal characters to represent you of match. An example is, if you want to match a phone number, you could use
* ```\(\d{3}\)\s?(\d{3})\-(\d{4})``` which would match something like (213)655-5555. Where the () are escaped around \d{3}, which matches exactly 3 digits. Then, same with the next and the last matches 4 digits.


### Greedy and Lazy Match
Greedy matches are regex characters that can find one or more objects, indefinitely. The wildcard "*" is one such greed match. The "." would match any one character at this spot. If you put the two together, you will match everything from the '.' and on, like this:
* "I want a .*" would match anything and everything after "I want a ".

One other greedy meta-character is the '+', it matches one or more characters. If used with, say, the \w+, like this, then it will match one character and then then next character, and then the next until it hits a non-alphanumeric character. An example is:

* "The HTML I will use is ```http://www.google.com"..match(/\w+/)``` will actually show you "The". If you use a global option, like /\w*/g, it will show you all words in the sentence, like
 * [
  'The',    'HTML',
  'I',      'will',
  'use',    'is',
  'http',   'www',
  'google', 'com'
]

### Boundaries
There a word boundaries in regex that say "the start of this boundary is starting at a word, and the character before is not a word". This is denoted by '\b'. So if you want boundaries around words, you would start it with a '\b' and end it with a '\b'. .. If you wish to negate the search, then use '\B'. Here is an example:
* If your string is "The bands URL they use is  http://www.myband.com and not https", and your regex is /\b(bands)\b/g, you would get one [ 'bands' ]. However,
* If your search was only for /\b(band)\b/g, it would give you null because there just isn't a "word" band in the string.

### Let's look at some examples of searching for URLs.

A typical URL is like this 'https://www.example.com'. The string that would match this (or anything like it) would be
1. ```/http?:\/\/\w+\.\w+\.(com|net|org)/``` would give you back 'https://www.example.com'
If all you want is 'example' from this URL, then you'd do something like
2. The pattern match is more of a script:
```js
var myUrl = 'https://www.example.com';
var myMatch = myUrl.match(/^https:\/\/www\.([a-zA-Z0-9]+)\.com$/);
console.log(myMatch[1])
```
3. If you want more complication ... You can also get more specific, like the www could be a 3 letter word, the root of the URL being 3 characters and the domain of the URL cannot start with a number, and can be either http or https.
```js
var myUrl = 'https://www.4exa2mple.com'; // would not work but exa2mpe would work.
var myMatch = myUrl.match(/^http(s)?:\/\/\w{3}\.([a-zA-z][a-zA-Z0-9]+)\.\w{3}$/);


if (myMatch) {
    var extractedWord = myMatch[2];
    console.log(extractedWord); // Output: example
} else {
    console.log('No match found');
}```


## Author

| Name      |Email      | Github    | Portfolio |
|-----------|-----------|-----------|-----------|
|Jason       |flimits@gmail.com|https://github.com/flimits|https://github.com/flimits/my-portfolio/|
