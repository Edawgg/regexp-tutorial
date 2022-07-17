# Title (*about*Regex- Tutorial for Junior Developers)

Introductory paragraph  (Regex, short for Regular Expressions is defined as a sequence of symbols and characters expressing a string or pattern to be searched for within a longer piece of text. Simply put, it is a tool with multiple uses that is highly recommended to learn if becomming an advanced level coder is your goal. Bellow is a tutorial to the basics of regex, by: Ethan McCann.)

## Summary

Regular Expressions are used in various ways to help make our lives easier. Regex can be used in all scripting languages as well as most general purpose languages. Not only is it designed for searching for specific characters, it can help with pattern identification, text-mining, and/or input validation. Regex isnt a programming language but it has its own syntax as well as reserved characters which will be included in this beginners guide. For the examples of code, JavaScript will be used, so be sure to reference the correct language.

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

### Anchors

    Anchors are 'reserved' or 'special' characters that hold meaning in regex. Specifically they communicate a special way, not by matching a character like other techniques but they match the position                                                                                  
    
    ^ ('Caret') anchor matches the beginning of the text.
    $ ('The Dollar') anchor matches the end of the text.

* Example 

    let str = 'random';
    console.log(/^r/.test(str));

    output: true

* using the console we test str to have the value of the first position match /^r/ so that would mean the same string could be tested to have /f$/ match the last position of the text and return false... keep an eye on the placement of the character when its a carat or a dollar anchor.

    let str = 'random';
    console.log(/f$/.test(str));

    output: false

### Quantifiers

    Quantifiers specify the amount of instances of a character, character group, or character class must be present in the input for a match to be found. By default quantifiers are known as 'greedy' and will return with as many matches as possible, thus appending the ? makes it 'lazy' which forces to match as few as possible. More on greedy and lazy will be broken down later on.

        *	*?	Match zero or more times.
        +	+?	Match one or more times.
        ?	??	Match zero or one time.
    
    You may also specify the exact number of times

        { n }	{ n }?	Match exactly n times.
        { n ,}	{ n ,}?	Match at least n times.
        { n , m }	{ n , m }?	Match from n to m times.

*  Example -in this example we use /\d to match 'digits'

        let str = 'the author was born in 1996';
        let re = /\d{4}/;

        let result = str.match(re);

        console.log(result)

        output: ["1996"]

    range matches a character or character class from n to m times. In the example g represents global.

        let str = 'The official DOB of E.M. is Jan 17, 1996';
        let re = /\d{2,4}/g;

        let result = str.match(re);
        
        console.log(result)

        output: [17 , 1996]

    there are shorthands for quantifiers

        + which is for {1, } one or more
        ? which is {0, 1} it will match with or without specific value
        * zero or more    

### OR Operator

    Alternation is the term in regular expression that is actually a simple “OR”.
In a regular expression it is denoted with a vertical line character |. It could be said an alternation is used when there is more than one alternative to the string you want to match. Having multiple alternative its often compared with the character class using parenthesis.

    For sale: cat|dog|mouse|snake|bird food

    "For sale: cat"
    "dog"
    "mouse"
    "snake"
    "bird food"

    For sale: (cat|dog|mouse|snake|bird) food

    "For sale: cat food"
    "For sale: dog food"
    "For sale: mouse food"
    "For sale: snake food"
    "For sale: bird food"

### Character Classes

    A character class is a special notation that matches any symbol from a certain set. For the start the “digit” class it’s written as \d and corresponds to any single digit for instance, finding the first digit in a phone number:

* Example

        let str = "+1(480)-123-4567";

        let rslt = /\d/;
        console.log(rslt);

        output: 1

    That was a character class for digits. There are other character classes as well.
    Most used are:

    \d (“d” is from “digit”)
    A digit: a character from 0 to 9.
    
    \s (“s” is from “space”)
    A space symbol: includes spaces, tabs \t, newlines \n and few other rare characters, such as \v, \f and \r.
    
    \w (“w” is from “word”)
    A “wordly” character: either a letter of Latin alphabet or a digit or an underscore _. Non-Latin letters (like cyrillic or hindi) do not belong to \w.


### Flags

    If specified, flags is a string that contains the flags to add. Alternatively, if an object is supplied for the pattern, the flags string will replace any of that object's flags (and lastIndex will be reset to 0) (as of ES2015). If flags is not specified and a regular expressions object is supplied, that object's flags (and lastIndex value) will be copied over.

    flags may contain any combination of the following characters:

    d (indices)- Generate indices for substring matches.

    g (global match)- Find all matches rather than stopping after the first match.

    m (multiline)- Treat beginning and end characters (^ and $) as working over multiple lines. In other words, match the beginning or end of each line (delimited by \n or \r), not only the very beginning or end of the whole input string.

    s ("dotAll")- Allows . to match newlines.

    u (unicode)- Treat pattern as a sequence of Unicode code points..

    y (sticky)- Matches only from the index indicated by the lastIndex property of this regular expression in the target string. Does not attempt to match from any later indexes.



### Grouping and Capturing

    A part of a pattern can be enclosed in parentheses (...). This is called a “capturing group”.

    That has two effects:

    It allows to get a part of the match as a separate item in the result array.
    If we put a quantifier after the parentheses, it applies to the parentheses as a whole.

* Example 

    without parentheses, the pattern go+ means g character, followed by o repeated one or more times. For instance, goooo or gooooooooo.

    Parentheses group characters together, so (go)+ means go, gogo, gogogo and so on.

    The method str.match(regexp), if regexp has no flag g, looks for the first match and returns it as an array:

    At index 0: the full match.
    At index 1: the contents of the first parentheses.
    At index 2: the contents of the second parentheses.
    …and so on…


### Bracket Expressions

    A bracket expression (an expression enclosed in square brackets, "[]" ) is an regex that shall match a specific set of single characters, and may match a specific set of multi-character collating elements, based on the non-empty set of list expressions contained in the bracket expression. A bracket expression is either a matching list expression or a non-matching list expression. A matching list expression specifies a list that shall match any single character that is matched by one of the expressions represented in the list.

    Special characters lose their special meaning inside bracket expressions.

    ‘]’ ends the bracket expression if it’s not the first list item. So, if you want to make the ‘]’ character a list item, you must put it first.

    ‘[.’ represents the open collating symbol.

    ‘.]’ represents the close collating symbol.

    ‘[=’ represents the open equivalence class.

    ‘=]’ represents the close equivalence class.

    ‘[:’ represents the open character class symbol, and should be followed by a valid character class name.

    ‘:]’ represents the close character class symbol.

    ‘-’ represents the range if it’s not first or last in a list or the ending point of a range.

    ‘^’ represents the characters not in the list. If you want to make the ‘^’ character a list item, place it anywhere but first.


### Greedy and Lazy Match

    Quantifiers are very simple from the first sight, but in fact they can be tricky.We should understand how the search works very well if we plan to look for something more complex than /\d+/. In the greedy mode (by default) a quantified character is repeated as many times as possible. The lazy mode of quantifiers is an opposite to the greedy mode. It means: “repeat minimal number of times”. usually a question mark ? is a quantifier by itself (zero or one), but if added after another quantifier (or even itself) it gets another meaning – it switches the matching mode from greedy to lazy.

    Alternative approach with regexps, there’s often more than one way to do the same thing. In our case we can find quoted strings without lazy mode using the regexp "[^"]+":   Please note, that this logic does not replace lazy quantifiers! It is just different. There are times when we need one or another.


### Boundaries

    A word boundary \b is a test, just like ^ and $. When the regexp engine (program module that implements searching for regexps) comes across \b, it checks that the position in the string is a word boundary. There are three different positions that qualify as word boundaries:

    At string start, if the first string character is a word character \w.

    Between two characters in the string, where one is a word character \w and the other is not.

    At string end, if the last string character is a word character \w.

    We can use \b not only with words, but with digits as well. For example, the pattern \b\d\d\b looks for standalone 2-digit numbers. In other words, it looks for 2-digit numbers that are surrounded by characters different from \w, such as spaces or punctuation (or text start/end).

### Back-references

    Backreferences in pattern: \N and \k<name>  
    We can use the contents of capturing groups (...) not only in the result or in the replacement string, but also in the pattern itself.

    Backreference by number: \N
    A group can be referenced in the pattern using \N, where N is the group number.

    Backreference by name: \k<name>
    If a regexp has many parentheses, it’s convenient to give them names. To reference a named group we can use \k<name>. If the group with quotes is named ?<quote>,  the backreference is \k<quote>:

### Look-ahead and Look-behind


    Sometimes we need to find only those matches for a pattern that are followed or preceded by another pattern. There’s a special syntax for that, called “lookahead” and “lookbehind”, together referred to as “lookaround”.

    Lookahead
    The syntax is: X(?=Y), it means "look for X, but match only if followed by Y". There may be any pattern instead of X and Y.

# Example
        More complex tests are possible, e.g. A(?=B)(?=C) means:

        Find A.
        Check if B is immediately after A (skip if isn’t).
        Check if C is also immediately after A (skip if isn’t).
        If both tests passed, then the A is a match, otherwise continue searching.


    Let’s say that we want a quantity instead, not a price from the same string. That’s a number \d+, NOT followed by €. For that, a negative lookahead can be applied. The syntax is: X(?!Y), it means "search X, but only if not followed by Y". Lookahead allows to add a condition for “what follows”.

    Lookbehind is similar, but it looks behind. That is, it allows to match a pattern only if there’s something before it. The syntax is:

    Positive lookbehind: (?<=Y)X, matches X, but only if there’s Y before it.
    Negative lookbehind: (?<!Y)X, matches X, but only if there’s no Y before it.

    For example, let’s change the price to US dollars. The dollar sign is usually before the number, so to look for $30 we’ll use (?<=\$)\d+ – an amount preceded by $:


## Author

    A short section about the author with a link to the author's GitHub profile (My name is Ethan McCann I am 26 years old and in the beginning stages of learning how to become a full-stack developer. My journey thus far has had its ups and downs but what I can take from what I have learned this far is to never give up and devote as much time as you can because this feild is always changing and the demand for coders will continue to grow. If you would like to see my work so for please check out my github profile. https://github.com/edawgg)
