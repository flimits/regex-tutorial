# Regex Tutorial Starter Code

A regular expression, also known as reg-ex, is a sequence of characters that are designed to search for a specific pattern of text in a document. The document being, a web page, email, search bar, or coding of some kind.


There are literal characters and meta characters that you use to create these regex's. The literal character is just that, literally something like an alphanumeric character, such as
* an 'a' or 'b' or 'Hello'
* a '9', '5aH'

That is, it can be a capital letter, or lower case, a combination letters and numbers and so on.

Meta characters are characters that have special meaning when used in regex and can be used to single out something you are looking for, or be more broad and grab a bigger scope of characters/words/etc. As an example, 
* the '.' is a meta character that means match "any" character (like ... any character, including a period) 
* The '*' is a wild card characters which means "any amount of characters"
* The '?' would mean, match zero or more characters ... (like I want to match an 's' in it or not: ie beans? would match "bean" or "beans")

You can also have positional characters in regex that help to mark where in the string you are targeting the search. Example of position characters are:
* '^' which marks the start at beginning string
* '$' would mark the start at end of the string

(This is not exhaustive, there are many meta characters. Look at this [Cheat Sheet Here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet) for more examples of meta characters in regular expressions from Mozilla).

If used in combination, the ".*" would mean I'm looking for absolutely everthing from this point on.

There are <ins>single character</ins> ways to match, <ins>quatifiers</ins> that are meant to modify the previous single character trajectory in saying "how many of those do you want and in what direction?", and then there are <ins>position</ins> which matches where in a string you want to find.


There is a <ins>Character Class</ins>, which are search for "things" in between the '[]' characters, but be OR'd (like this OR that, examples to follow). Something like, if there is a ...
* [abc], it would mean match on an 'a' character OR a 'b' character OR a 'c' character
* [a-z], the dash here means, match one of any of the characters from a through z, a OR b OR c OR d...etc to z
* [^abc], if in the '[]' means NOT one of the following, like NOT either an 'a' or NOT a 'b' or NOT a 'c'
* [-.], however, if - is not inbetween words, it is a literal '-'. same with the '.' 

Alternations AND or OR searches


and example of getting a phone number is

      <ins>'\(?\d{3}[-.)]\d{3}[-.]\d{4}'</ins>

this is saying, is, machine a '(' or not, followed by 3 digits, then either a '-' OR a '.' OR a ')', followed by 3 digits, followed by a '-' OR a '.', followed by 4 more digits.