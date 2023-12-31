# An Introduction To Regex

Regex, short for 'regular expression', is a syntax that allows you to match strings with specific patterns. You can imagine it as a text search that can become very advanced & specific depending on how many filters, Regex Components, are added.

## Summary

I will be explaining Regex used in a Javascript environment with all declarations of variables and commands being in JS, however, the Regex notation itself is a universal language that can be applied to many different coding languages. By the end of this article, I hope you will have enough information to set up Regex Syntax in your own coding programs.

## Table of Contents

- [Getting Started](#getting-started)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [Destructuring a Regex](#destructuring-a-regex)
- [Author](#author)
- [Additional Resources](#additional-resources)

## Getting Started

This is an example of using the `Regex constructor function`. This should only be used when you know that the pattern will be changing or that the pattern will be based on user input.

```c
let pattern = new RegExp("hello");
let input = "hello world";
let result = pattern.test(input);   //This tests to see if the pattern exists within the input text
console.log(result);

//Returns 'true' because the Regex pattern exists within the input.
```

This is an example of `literal notation` (where instead of declaring something is a Regex expression, you use syntax notation to have javascript automatically perceive it as Regex):

```c
let pattern = /hello/;
let input = "hello world";
let result = pattern.test(input);
console.log(result);
```

`**A forward slash ('/') denotes both the start and end of a string in Regex`

## Anchors

Anchors have special meaning in Regex (regular expressions). They do not match any character. Instead, they match a position before or after a string, characters, or line:

- `^` - The carrot anchor matches the beginning of a text.
- `$` - The dollar sign anchor matches the end of a text.

```c
let string = 'Javascript';
let pattern = /^J/;
let result = pattern.test(string);
console.log(result);

//Because the string starts with a 'J', the console logs 'true'
```

`**Regex is case sensitive, so if you are looking for a capital 'J', then it will not accept a lowercase 'j'.`

```c
let string = 'Javascript';
let pattern = /t$/;
let result = pattern.test(string);
console.log(result);

//Because the string ends in a 't', the console logs 'true'
```

`**These Regex searches currently only find the first pattern that matches in the string. That's fine right now since we are only testing if it exists within the string. However, when we start trying to record every matching pattern in the string, that is when we will need to start including quantifiers and flags.`

## Quantifiers

Quantifiers indicate how many times a character, group, or pattern should be matched in a string. However, unless it is formatted to refer to a group or pattern, a quantifier by default will refer to the first character that precedes it. So, if you were to set up a regex like `/ghost{3,}/` then the quantifier will only apply to the 't' in 'ghost'. This particular example will look for the first pattern in a string that has the string 'ghos' with three or more t's following it.

There are several types of quantifiers in Regex, which are:

**`Question Mark (?)`** - Indicates that the target is optional and can have 0 or 1 occurrence.

**`Asterisk (*)`** - 0 or more occurrences.

**`Plus Sign (+)`** - 1 or more occurrences.

**`Curly Brackets ({m, n})`** - m to n occurrences.

- `{m}` - Matches exactly m occurrences.
- `{m,}` - Matches m or more occurrences.

## Grouping Constructs

As a regular expression (Regex) becomes more intricate, you may often find yourself needing different parts of a string to fit specific criteria. For example, an email is something you would break up into the username like portion, the @ symbol, and the type of email such as gmail.com, yahoo.com, etc... Defining these sections is where Grouping Constructs come into play. To define a section in Regex you need to utilize parentheses `()`, with each section within a parentheses being known as a `subexpression`.

- `**Unlike bracket notation which will be mentioned later, subexpressions look for exactly what is in them.`

**Subexpressions**: have two primary states, a `capturing group` state and a `non-capturing group` state. A **capturing group** has something called a backreference immediately following it. A backreference is a backslash followed by a number, like so: '\1'. A backreference exists so that when the capturing group records a matched character sequence it can be reused by utilizing the backreference. The number used for the backreference can start at 1 and be any integer as high as the number of subexpressions that are present. Now, a **non-capturing group** is a subexpression with a question mark and colon placed before the pattern, like so: `(?:pattern)`.

## Bracket Expressions

Anything within brackets represents a range of characters that we are attempting to match. If we for example had a bracket expression like `[abc]`, then we would be searching for a string that begins with either 'a', 'b, or 'c'. We can also set the bracket expression as `[a-c]` for the exact same result. Now as a reminder, Regex is very strict with lowercase and capitalized letters, thus, in order to include them you need to do something like `[a-zA-Z]` or `[a-cB-Q]`.

- `[0-9]` will match a string that contains the numbers zero through nine.
- `[-_]` The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. With this bracket expression we are saying we need a string that includes either '-' or '\_'. It's important to note that the hyphen here is not the same hyphen that we used in our alphanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric character ranges within the brackets.

- `**The order within a bracket expression does not matter.`
- `**A bracket expression can be turned into a negative character group by adding a carrot (^) first within it. (ex: [^aeiou] will exclude the listed characters).`

## Character Classes

A `character class` in a Regex defines a set of characters, any one of which can occur in an input string to fulfill a match. The positive and negative bracket expressions are also considered character classes.

Some common character classes to know are:

- `.` - This will match any character except the new line character (`\n`).
- `\d` - This will match any Arabic numeral digit. This class is equivalent to the bracket expression `[0-9]`.
- `\w` - This matches any alphanumeric character from the basic Latin alphabet, including the underscore `_`. This class is equivalent to the bracket expression `[A-Za-z0-9_]`.
- `\s` - This matches a single whitespace character, including tabs and line breaks.

- `**Each of these classes can also perform the opposite where they exclude their specific characters from matching. All that's needed is to capitalize the class, so for example '\d' can be capitalized to '\D' and will match every character EXCEPT the digits 0-9.`

More character classes can be found here: [**Other Character Classes**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Character_classes)

## The OR Operator

Within bracket expressions we are given options of characters to match, such as how [a-z0-9] asks for the character to match either a lowercase letter from a to z **OR** a digit from zero to nine. The `OR Operator` is taking this concept and applying it in places like subexpressions using the '`|`' symbol. An example of this would be **(cat|dog)**, here we are looking for a pattern of 'cat' **OR** 'dog' to be present within a text. There is also no real limit to adding the OR Operator so you can customize many optional patterns.

## Flags

**Flags** are like a set of instructions that change the behavior of a regular expression (Regex).

Some flags are as follows:

- `g` - **Global Search**: This makes it so that the Regex will be tested against all possible matches in a string. Without this the Regex will stop searching after finding its first match, even if there are many more matches later in the string/text.
- `i` - **Case Insensitive Search**: This makes it so that lowercase and uppercase should be treated the same when looking through the string/text for a pattern.
- `m` - **Multi Line Search**: This enables a multiline mode within Regex, affecting the `^` and `$` anchors. In the multiline mode they match not only at the beginning and the end of the string, but also at start/end of line. An example can be seen below:

```c
let str = '1st place Winnie,
2nd place Piglet,
3rd place: Eeyore';

console.log( str.match(/^\d/gm) );
// This results in: 1, 2, 3
```

`**Flags will always be placed after the end slash of a Regex literal notation and as the second argument within a Regex constructor function`

```c
//Regex literal notation.

regexp = /pattern/;   // no flags
regexp = /pattern/gmi;   // with flags g,m and i

//Regex constructor function.

regexp = new RegExp("pattern", "flags");

```

## Character Escapes

In a regular expression (Regex), a string will begin and end with a forward slash (`/`). Everything within it will be either a part of the pattern or a search filter such as the quantifiers, bracket expressions, character classes, etc. However, what if you want to include one of the special characters used in the search filter as a part of the pattern string? This is where the character escape comes into play. A `backslash` (`\`), will treat the following character as a part of the string before continuing on with the Regex as normal.

- `**As a side note, any special characters, including the backslash, within a bracket expression will automatically lose their special significance and will be treated as a character to match within the text if preceded by a backslash. The exceptions for this are character classes that require a backslash to operate.`

```c
//This will not try and match a backslash (\)
let pattern = /[\]/
//This will try and match a backslash (\) because the first backslash is turning the second backslash into a character
let pattern = /[\\]/

//This is a character class that already possesses a backslash (\) so it operates as it's intended character class
let pattern = /[\d]/

```

## Destructuring a Regex

Now that we have gone through all the parts of a regular expression (Regex), let's practice by destructuring one.

This here is a Regex used for matching an Email:
`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

```c
//First, this is a literal notation Regex. So, working outwards in we would check for flags, which are not present
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ // <-- A flag should be after the ending forward slash

//Next, We can take off the start and end forward slashes that denote this as a Regex string.
^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$

//To destructure it further let's break it into sections to see what and how it is matching strings.
^([a-z0-9_\.-]+)
@
([\da-z\.-]+)
\.
([a-z\.]{2,6})$
```

`^([a-z0-9_\.-]+)`

```c
//Moving outward in, we come across the carrot symbol (^) just outside a grouping construct of a subexpression.
//This indicates that the subexpression is the search filter for the first character of the pattern.
([a-z0-9_\.-]+)

//Once we move further in however we come across a plus sign (+) indicating that this subexpression can have more than one occurrence.
//More specifically, since we had a carrot symbol it means this filter will occur for each character until we run into the next part of the Regex (which is the @ symbol).
[a-z0-9_\.-]

//Lastly, we have a bracket expression which defines what the specific characters the filter is looking to match.
//This specific bracket expression is looking for any lowercase letters from a to z, any digit from 0 to 9, an underscore, a period (which is utilizing a character escape), or a dash.
```

`@`

```c
//After the first part of the Regex, we move onto the next which is just a straightforward character
@

//This is saying that after the first grouping construct is fulfilled there must be an @ character.
```

`([\da-z\.-]+)`

```c
//The next portion of the regex is another grouping construct of a subexpression.
//This indicates that the subexpression is the search filter for the first character of the pattern.
([\da-z\.-]+)

//Once we move further in however we come across a plus sign (+) indicating that this subexpression can have more than one occurrence.
[\da-z\.-]

//Lastly, we have a bracket expression which defines what the specific characters the filter is looking to match.
//This specific bracket expression is looking for any digit from 0 to 9 using the character class (\d), any lowercase letters from a to z, a period (which is utilizing a character escape), or a dash.
```

`\.`

```c
//The following portion is a filter searching for a period (.) character to match. Since a period is a character class it requires a character escape (\) in order to lose its properties as a special character.
\.
```

`([a-z\.]{2,6})$`

```c
//The last portion of this regex is signified by the dollar sign ($) that appears behind the group construct. It defines the end of the pattern/text.
([a-z\.]{2,6})$

//Within the group construct is the subexpression split in two parts, the first is a bracket expression. The bracket expression limits the ending character(s) to be either lowercase letters from a to z or a period (which is utilizing a character escape).
[a-z\.]

//The second portion of this subexpression is the range of matches/occurrences that the bracket expression can express.
```

## Author

I, `Shane Mindreau`, wrote this article as a means to both learn and teach regular expressions (Regex). It is a very helpful tool to utilize when coding and I hope this article has helped you learn enough to use it within your own projects.

To see more of my work and projects visit my `GitHub Repository` or my `personal portfolio page`:

[Shane Mindreau's GitHub Repository](https://github.com/smindre1?tab=repositories)

[Shane Mindreau's Portfolio Page](https://smindre1.github.io/shane-mindreau-portfolio/)

## Additional Resources

[What is Regex?](https://www.variables.sh/what-is-regex/#:~:text=Regexes%20are%20composed%20of%20several,classes%2C%20quantifiers%2C%20and%20alternation)

[Regular Expression's Tutorial](https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)

[Regular Expression: Anchors](https://www.javascripttutorial.net/regular-expression-anchors/)

[Unlock The Power Of Regex! JS tutorial](https://www.youtube.com/watch?v=5vmhTcJ3KGI)

[Regex Syntax Cheatsheet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet)
