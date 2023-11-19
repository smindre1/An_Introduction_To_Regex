# An Introduction To Regex

Regex, short for 'regular expression', is a syntax that allows you to match strings with specific patterns. You can imagine it as a text search that can become very advanced & specific depending on how many filters, Regex Components, are added.

## Summary

I will be explaining Regex used in a Javascript enviornment with all declarations of variables and commands being in JS, however, the Regex notation itself is a universal language that can be applied to many different coding languages. By the end of this article, I hope you will have enough information to setup Regex Syntax in your own coding programs.

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

- `^` - The carot anchor matches the begining of a text.
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

Quantifiers indicate how many times a character, group, or pattern should be matched in a string. However, unless it is formatted to refer to a group or pattern, a quantifier by default will refer to the first character that preceeds it. So, if you were to setup a regex like `/ghost{3,}/` then the quantifier will only apply to the 't' in 'ghost'. This particular example will look for the first pattern in a string that has the string 'ghos' with three or more t's following it.

There are several types of quantifiers in Regex, which are:

**`Question Mark (?)`** - Indicates that the target is optional and can have 0 or 1 occurrence.

**`Asterisk (*)`** - 0 or more occurrences.

**`Plus Sign (+)`** - 1 or more occurrences.

**`Curly Brackets ({m, n})`** - m to n occurrences.

- `{m}` - Matches exactly m occurences.
- `{m,}` - Matches m or more occurences.

## Grouping Constructs

As a regular expression (Regex) becomes more intricate, you may often find yourself needing different parts of a string to fit specific criteria. For example, an email is something you would break up into the username like portion, the @ symbol, and the type of email such as gmail.com, yahoo.com, etc... Defining these section is where Grouping Constructs come into play. To define a section in Regex you need to utilize parentheses `()`, with each section within a parentheses being known as a `subexpression`.

- `**Unlike bracket notation which will be mentioned later, subexpressions look for exactly what is in them.`

**Subexpressions**: have two primary states, a `capturing group` state and a `non-capturing group` state. A **capturing group** has something called a backreference immediately following it. A backreference is a backslash followed by a number, like so: '\1'. A backreference exists so that when the capturing group records a matched character sequence it can be reused by utilizing the backreference. The number used for the backreference can start at 1 and be any integer as high as the number of subexpressions that are present. Now, a **non-capturing group** is a subexpression with a question mark and colon placed before the pattern, like so: `(?:pattern)`.

## Bracket Expressions

Anything within brackets represents a range of characters that we are attempting to match. If we for example had a bracket expression like `[abc]`, then we would be searching for a string that begins with either 'a', 'b, or 'c'. We can also set the bracket expression as `[a-c]` for the exact same result. Now as a reminder, Regex is very strict with lowercase and capitalize letters and in order to include them you need to do something like `[a-zA-Z]` or `[a-cB-Q]`.

- `[0-9]` will match a string that contains the numbers zero through nine.
- `[-_]` The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. With this bracket expression we are saying we need a string that includes either '-' or '\_'. It's important to note that the hyphen here is not the same hyphen that we used in our alphanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric character ranges within the brackets.

-`**The order within a bracket expression does not matter.` -`**A bracket expression can be turned into a negative character group by adding a carrot (^) first within it. (ex: [^aeiou] will exclude the listed characters).`

## Character Classes

A `character class` in a Regex defines a set of characters, any one of which can occur in an input string to fulfill a match. The positive and negative bracket expressions are also considered character classes.

Some common character classes to know are:

- `.` - This will match any character except the new line character (`\n`).
- `\d` - This will matche any Arabic numeral digit. This class is equivalent to the bracket expression `[0-9]`.
- `\w` - This matches any alphanumeric character from the basic Latin alphabet, including the underscore `_`. This class is equivalent to the bracket expression `[A-Za-z0-9_]`.
- `\s` - This matches a single whitespace character, including tabs and line breaks.

- `**Each of these classes can also perform the opposite where they exclude their specific characters from matching. All that's needed is to capitalize the class, so for example '\d' can be capitalized to '\D' and will match every character EXCEPT the digits 0-9.`

More character classes can be found here: [**Other Character Classes**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Character_classes)

## The OR Operator

Within bracket expressions we are given options of characcters to match, such as how [a-z0-9] asks for the character to match either a lowercase letter from a to z **OR** a digit from zero to nine. The `OR Operator` is taking this concept and applying it in places like subexpressions using the '`|`' symbol. An example of this would be **(cat|dog)**, here we are looking for a pattern of 'cat' **OR** 'dog' to be present within a text. There is also no real limit to adding the OR Operator so you can cutomize many optional patterns.

## Flags

**Flags** are like a set of instructions that change the behavior of a regular expression (Regex).

Some flags are as follows:

- `g` - **Global Search**: This makes it so that the Regex will be tested against all possible matches in a string. Without this the Regex will stop searching after finding it's first match, even if there are mnay more matches later in the string/text.
- `i` - **Case Insensitive Search**: This makes it so that lowercase and uppercase should be treated the same when looking through the string/text for a pattern.
- `m` - **Multi Line Search**: This eneables a multiline mode within Regex, affecting the `^` and `$` anchors. In the multiline mode they match not only at the beginning and the end of the string, but also at start/end of line. An example can be seen below:

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

- `**As a side note, any special characters, including the backslash, within a bracket expression will automatically lose their special significance and will be treated as a character to match within the text.`

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
