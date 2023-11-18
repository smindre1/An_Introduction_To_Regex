# An Introduction To Regex

Regex, short for 'regular expression', is a syntax that allows you to match strings with specific patterns. You can imagine it as a text search that can become very advanced & specific depending on how many filters, Regex Components, are added.

## Summary

I will be explaining Regex used in a Javascript enviornment. Any and all examples of Regex that utilize code will have been written in JS. By the end of this article, I hope you will have enough information to setup Regex Syntax in your own coding programs.

## Regex Components

- List all the components here

## Getting Started

This is an example of using Regex without utilizing it's literal notation.

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
