![js-dates.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1618296129/js_dates_ebca0a0677.jpg)
In this article , we will learn all the important topics related to dates in javascript with help of proper examples.\
`Date` objects contain a `Number` that represents milliseconds since 1 January 1970 UTC.
## Creating A Date Object
We can create a `Date` object using `Date()` constructor with the following syntaxes - 
```js
new Date() //current date and time as of the time of instantiation.
new Date(value) // value is an integer value representing the number of milliseconds since January 1, 1970, 00:00:00
new Date(dateString) // A string value representing a date
new Date(year, monthIndex [, day [, hours [, minutes [, seconds [, milliseconds]]]]]) //Give at least a year and month
```

#### Examples
```js
let today = new Date();
console.log(today);
let myDay = new Date('January 16, 2001 05:39:00');
console.log(myDay);
myDay = new Date('2001-01-16T05:39:00');
console.log(myDay);
myDay = new Date(2001, 0, 16); // the month is 0-indexed
console.log(myDay);
myDay = new Date(1995, 0, 16, 5, 39, 0);
console.log(myDay);
```
#### Output
>2021-04-12T19:46:14.180Z\
2001-01-16T00:09:00.000Z\
2001-01-16T00:09:00.000Z\
2001-01-15T18:30:00.000Z\
1995-01-16T00:09:00.000Z

## Important Instance Methods
### getDate()
Returns the day of the month (1–31) for the specified date according to local time.
```js
console.log(myDay.getDate());
```
#### Output
>16

### getDay()
Returns the day of the week (0–6) for the specified date according to local time.
```js
console.log(myDay.getDay());
```
#### Output
>1

### getFullYear()
Returns the year (4 digits for 4-digit years) of the specified date according to local time.
```js
console.log(myDay.getFullYear());
```
#### Output
>1995

### getHours()
Returns the hour (0–23) in the specified date according to local time.
```js
console.log(myDay.getHours());
```
#### Output
>5

### getMinutes()
Returns the minutes (0–59) in the specified date according to local time.
```js
console.log(myDay.getMinutes());
```
#### Output
>39

### getSeconds()
Returns the seconds (0–59) in the specified date according to local time.
```js
console.log(myDay.getSeconds());
```
#### Output
>0

### getMonth()
Returns the month (0–11) in the specified date according to local time.
```js
console.log(myDay.getMonth());
```
#### Output
>0

***We also have similar methods with UTC as `getUTCDate()`,`getUTCDay()`,`getUTCFullYear()`,`getUTCHours()`,`getUTCMilliseconds()`,`getUTCMinutes()`,`getUTCMonth()` and `getUTCSeconds()` which will give similar results but according to universal time.***

***We also have similar setter methods with local time as well as with UTC which are `setUTCDate()`,`setUTCDay()`,`setUTCFullYear()`,`setUTCHours()`,`setUTCMilliseconds()`,`setUTCMinutes()`,`setUTCMonth()` and `setUTCSeconds()` which will set the particular parameters according to universal time. While `setDate()`,`setDay()`,`setFullYear()`,`setHours()`,`setMilliseconds()`,`setMinutes()`,`setMonth()` and `setSeconds()` will set the parameters according to lacale time.***


## Important Methods To Convert Date To String
### toDateString()
Returns the "date" portion of the Date as a human-readable string like `Tue Apr 13 2021`.

### toISOString()
Converts a date to a string following the ISO 8601 Extended Format like`1995-01-16T00:09:00.000Z` .

### toUTCString()
Converts a date to a string using the UTC timezone like `Mon, 16 Jan 1995 00:09:00 GMT`.

### toLocaleString()
Returns a string with a locality-sensitive representation of this date like `1/16/1995, 5:39:00 AM`.

### Calculating Elapsed Time
```js
let start = new Date()
// The event to time goes here:
doSomethingForALongTime()
let end = new Date()
let elapsed = end.getTime() - start.getTime() // elapsed time in milliseconds
```

### Get the number of seconds since the ECMAScript Epoch
```js
let seconds = Math.floor(Date.now() / 1000)
```

So , that is it for this article 😀. I hope you understand how to manipulate dates in javascript. And lastly as always , Thank You for reading.