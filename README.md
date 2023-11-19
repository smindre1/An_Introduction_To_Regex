# An Introduction To Regex

Regex, short for 'regular expression', is a syntax that allows you to match strings with specific patterns. You can imagine it as a text search that can become very advanced & specific depending on how many filters, Regex Components, are added.

## Summary

I will be explaining Regex used in a Javascript enviornment. Any and all examples of Regex that utilize code will have been written in JS. By the end of this article, I hope you will have enough information to setup Regex Syntax in your own coding programs.

## Regex Components

- List all the components here

## Getting Started

This is an example of using the Regex constructor function. This should only be used when you know that the pattern will be changing or that the pattern will be based on user input.

```
let pattern = new RegExp("hello");
let input = "hello world";
let result = pattern.test(input);   //This tests to see if the pattern exists within the input text
console.log(result);

//Returns 'true' because the Regex pattern exists within the input.
```

This is an example of literal notation (where instead of declaring something is a Regex expression, you use syntax notation to have javascript automatically perceive it as regex):

```
let pattern = /hello/;
let input = "hello world";
let result = pattern.test(input);
console.log(result);
```

`**A forward slash ('/') denotes both the start and end of a string in regex`

## Anchors

Anchors have special meaning in regex (regular expressions). They do not match any character. Instead, they match a position before or after a string, characters, or line:

- `^` - The carot anchor matches the begining of a text.
- `$` - The dollar sign anchor matches the end of a text.

```
let string = 'Javascript';
let pattern = /^J/;
let result = pattern.test(string);
console.log(result);

//Because the string starts with a 'J', the console logs 'true'
```

`**Regex is case sensitive, so if you are looking for a capital 'J', then it will not accept a lowercase 'j'.`

```
let string = 'Javascript';
let pattern = /t$/;
let result = pattern.test(string);
console.log(result);

//Because the string ends in a 't', the console logs 'true'
```

`**These regex searches currently only find the first pattern that matches in the string. That's fine right now since we are only testing if it exists within the string. However, when we start trying to record every matching pattern in the string, that is when we will need to start including quantifiers and flags.`

### Quantifiers

Quantifiers indicate how many times a character, group, or pattern should be matched in a string. However, unless it is formatted to refer to a group or pattern, a quantifier by default will refer to the first character that preceeds it. So, if you were to setup a regex like `/ghost{3,}/` then the quantifier will only apply to the 't' in 'ghost'. This particular example will look for the first pattern in a string that has the string 'ghos' with three or more t's following it.

There are several types of quantifiers in regex, which are:

**`Question Mark (?)`** - Indicates that the target is optional and can have 0 or 1 occurrence.

**`Asterisk (*)`** - 0 or more occurrences.

**`Plus Sign (+)`** - 1 or more occurrences.

**`Curly Brackets ({m, n})`** - m to n occurrences.

- `{m}` - Matches exactly m occurences.
- `{m,}` - Matches m or more occurences.

### Grouping Constructs

As a regular expression (regex) becomes more intricate, you may often find yourself needing different parts of a string to fit specific criteria. For example, an email is something you would break up into the username like portion, the @ symbol, and the type of email such as gmail.com, yahoo.com, etc... Defining these section is where Grouping Constructs come into play. To define a section in regex you need to utilize parentheses `()`, with each section within a parentheses being known as a `subexpression`.

- `**Unlike bracket notation which will be mentioned later, subexpressions look for exactly what is in them.`

**Subexpressions**: have two primary states, a `capturing group` state and a `non-capturing group` state. A **capturing group** has something called a backreference immediately following it. A backreference is a backslash followed by a number, like so: '\1'. A backreference exists so that when the capturing group records a matched character sequence it can be reused by utilizing the backreference. The number used for the backreference can start at 1 and be any integer as high as the number of subexpressions that are present. Now, a **non-capturing group** is a subexpression with a question mark and colon placed before the pattern, like so: `(?:pattern)`.

### Bracket Expressions

Anything within brackets represents a range of characters that we are attempting to match. If we for example had a bracket expression like `[abc]`, then we would be searching for a string that begins with either 'a', 'b, or 'c'. We can also set the bracket expression as `[a-c]` for the exact same result. Now as a reminder, regex is very strict with lowercase and capitalize letters and in order to include them you need to do something like `[a-zA-Z]` or `[a-cB-Q]`.

- `[0-9]` will match a string that contains the numbers zero through nine.
- `[-_]` The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. With this bracket expression we are saying we need a string that includes either '-' or '\_'. It's important to note that the hyphen here is not the same hyphen that we used in our alphanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric character ranges within the brackets.

-`**The order within a bracket expression does not matter.` -`**A bracket expression can be turned into a negative character group by adding a carrot (^) first within it. (ex: [^aeiou] will exclude the listed characters).`

### Character Classes

A `character class` in a regex defines a set of characters, any one of which can occur in an input string to fulfill a match. The positive and negative bracket expressions are also considered character classes.

Some common character classes to know are:

- `.` - This will match any character except the new line character (`\n`).
- `\d` - This will matche any Arabic numeral digit. This class is equivalent to the bracket expression `[0-9]`.
- `\w` - This matches any alphanumeric character from the basic Latin alphabet, including the underscore `_`. This class is equivalent to the bracket expression `[A-Za-z0-9_]`.
- `\s` - This matches a single whitespace character, including tabs and line breaks.

- `**Each of these classes can also perform the opposite where they exclude their specific characters from matching. All that's needed is to capitalize the class, so for example '\d' can be capitalized to '\D' and will match every character EXCEPT the digits 0-9.`

More character classes can be found here: [**Other Character Classes**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Character_classes)
