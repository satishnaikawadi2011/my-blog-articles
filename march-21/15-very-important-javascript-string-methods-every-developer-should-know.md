Manipulation of javascript strings are very important in most of the  web development projects. So , in this post we will take a look 😍 at some important and frequently used string methods in javascript. Below are the strings which we will used to learn this methods with.
```js
var stringOne = "Let's learn important javascript string methods."
var stringTwo = "Also we will see their examples."
```
## charAt()
The `String` object's `charAt()` method returns a new string consisting of the single UTF-16 code unit located at the specified offset into the string.If the `index` cannot be converted to the integer or no `index` is provided, the default is `0`, so the first character of string is returned.
```js
const index = 4;
console.log(`Character at index ${index} in stringOne is ${stringOne.charAt(index)}`);
```
**Output**
>Character at index 4 in stringOne is s

## concat()
The `concat()` method concatenates the string arguments to the calling string and returns a new string. If the arguments are not of the type string, they are converted to string values before concatenating.
```js
console.log(stringOne.concat(stringTwo));
console.log(stringOne.concat('And ', stringTwo));
```
**Output**
>Let's learn important javascript string methods.Also we will see their examples.
Let's learn important javascript string methods.And Also we will see their examples.

## endsWith()
The `endsWith()` method determines whether a string ends with the characters of a specified string, returning `true` or `false` as appropriate. This method is case-sensitive. If second argument provided, it is used as the `length` of string. Defaults to `string.length`.
```js
console.log(stringOne.endsWith('methods.'));
console.log(stringOne.endsWith('javascript'));
console.log(stringOne.endsWith('javascript', 32));
```
**Output**
>true
false
true

## includes()
The `includes()` method performs a case-sensitive search to determine whether one string may be found within another string, returning `true` or `false` as appropriate. The second argument is position within the string at which to begin searching for searchString. (Defaults to 0.)
```js
console.log(stringOne.includes("Let's"));
console.log(stringOne.includes("Let's", 1)); //Start searching from first index
console.log(stringOne.includes("let's")); //Case sensitive
```
**Output**
>true
false
false

## indexOf()
The `indexOf()` method returns the index within the calling String object of the first occurrence of the specified value, starting the search at `fromIndex`. Returns `-1` if the value is not found. `fromIndex` is the second argument which is an integer representing the index at which to start the search. Defaults to 0.
```js
console.log(stringOne.indexOf('a'));
console.log(stringOne.indexOf('a', 15)); //Start searching from index 15
```
**Output**
>8
18

## lastIndexOf()
The `lastIndexOf()` method is same as `indexOf()` method only difference is instead of first occurence it search for last occurence of a given string. It returns the `index` of the last occurrence of searchValue; `-1` if not found. 
```js
console.log(stringOne.lastIndexOf('a'));
```
**Output**
>25

## replace()
The `replace()` method returns a new string with some or all matches of a `pattern` replaced by a replacement. The pattern can be a `string` or a `RegExp`, and the replacement can be a `string` or a `function` to be called for each match. If pattern is a string, only the first occurrence will be replaced.
The original string is left unchanged.
```js
console.log(stringOne.replace('methods', 'functions'));
console.log(stringOne.replace('important', 'must know'));
const regex = /Javascript/i;
console.log(stringOne.replace(regex, 'JS'));
```
**Output**
>Let's learn important javascript string functions.
Let's learn must know javascript string methods.
Let's learn important JS string methods.

**`replaceAll()` is also a similar method only difference is instead of replacing first match it will replace every match in the string.**

## startsWith()
The `startsWith()` method determines whether a string begins with the characters of a specified string, returning `true` or `false` as appropriate.The second argument is `position` in this string at which to begin searching for searchString. Defaults to 0.
```js
console.log(stringOne.startsWith("Let's"));
console.log(stringOne.startsWith("Let's", 5)); // Start searching from position at index 5
```
**Output**
>true
false

## slice()
The `slice()` method **extracts a section of a string** and returns it as a new string, without modifying the original string. Its first argument is `beginIndex` - the zero-based index at which to begin extraction. And second srgument is `endIndex` - the zero-based index before which to end extraction. **The character at `endIndex` will not be included.**
If any or both of the two `endIndex` and `beginIndex` are negative, then they are treated as `str.length + endIndex` and `str.length + beginIndex` . (For example, if endIndex is -3, it is treated as str.length - 3.)
```js
console.log(`Length of stringOne is ${stringOne.length}`);
console.log(stringOne.slice(6, 22)); // Start at index 6 and extract upto index 22 not including 22
console.log(stringOne.slice(6, -9)); // Start at index 6 and extract upto index 48 - 9 = 39 not including 39
console.log(stringOne.slice(6)); // Start at index 6 and extract whole string
console.log(stringOne.slice(50)); // As startIndex is greater than length return empty string
```
**Output**
>Length of stringOne is 48
learn important 
learn important javascript string
learn important javascript string methods.

## split()
The `split()` method divides a `String` into an ordered list of substrings, puts these substrings into an `array`, and returns the `array`.
```js
console.log(stringOne.split(' '));
console.log(stringOne.split('learn'));
```
**Output**
>[ "Let's", 'learn', 'important', 'javascript', 'string', 'methods.' ]
[ "Let's ", ' important javascript string methods.' ]

## substr()
The `substr()` method returns a portion of the string, starting at the specified index and extending for a given number of characters afterwards.
```js
console.log(stringOne.substr(6)); // Start at index 6 and extract whole remaining string
console.log(stringOne.substr(6, 34)); // Start at index 6 and extract next 34 characters.
```
**Output**
>learn important javascript string methods.
learn important javascript string

## trim()
The `trim()` method removes whitespace from both ends of a string. Whitespace in this context is all the whitespace characters (space, tab, no-break space, etc.) and all the [line terminator characters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar) (LF, CR, etc.).
```js
var stringThree = '       remove whitespaces       ';
console.log(stringThree.trim());
```
**Output**
>remove whitespaces

**The `trimEnd()` and `trimStart()` are similar methods which removes whitespace from the end and start of the string respectively.**

## match()
The `match()` method retrieves the result of matching a string against a regular expression. You can learn about regular expression [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) .
```js
const regex = /[A-Z]/g; // regex for capital characters
console.log(stringOne.match(regex));
```
**Output**
>[ 'L' ]

## toLowerCase()
The `toLowerCase()` method returns the calling string value converted to lower case.
```js
var stringThree = 'THIS IS DEMO STRING';
console.log(stringThree.toLowerCase());
```
**Output**
>this is demo string

## toUpperCase()
The `toUpperCase()` method returns the calling string value converted to upper case.
```js
var stringThree = 'this is demo string';
console.log(stringThree.totoUpperCase()());
```
**Output**
>THIS IS DEMO STRING

And that is it for this article. You can visit [satishnaikawadi.me](https://satishnaikawadi.me/posts) for more articles related to programming.Thanks for reading 😇 .

