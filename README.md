# An Introduction To Regex

Regex, short for 'regular expression', is a syntax that allows you to match strings with specific patterns. You can imagine it as a text search that can become very advanced & specific depending on how many filters, Regex Components, are added.

## Summary

I will be explaining Regex used in a Javascript enviornment. Any and all examples of Regex that utilize code will have been written in JS. By the end of this article, I hope you will have enough information to setup Regex Syntax in your own coding programs.

## Regex Components

- List all the components here

### Getting Started

This is an example of using Regex without utilizing it's literal notation.

```
let pattern = new RegExp("hello");
let input = "hello world";
let result = pattern.test(input);
console.log(result);

//Returns 'true' because Regex is being tested to see if that pattern exists within the input.
```

This is an example of literal notation (where instead of declaring something is a Regex expression, you use syntax notation to have javascript automatically perceive it as regex):

```
let pattern = /hello/;
let input = "hello world";
let result = pattern.test(input);
console.log(result);
```

`**A forward slash ('/') denotes both the start and end of a string in regex`
