![js-array-methods.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1615701416/js_array_methods_48cf5bebc3.jpg)


In this article , we will see 10 important javascript array methods which almost needed everywhere in javascript projects. We will quickly take a look at each method with example. Below is the data with which we will be working while taking examples of first 8 method.

```javascript

const studentData = [
	{ name: 'John', marks: 634, passed: true },
	{ name: 'Mark', marks: 467, passed: true },
	{ name: 'Randy', marks: 390, passed: true },
	{ name: 'Leo', marks: 149, passed: false },
	{ name: 'Chris', marks: 564, passed: true },
	{ name: 'Apu', marks: 456, passed: true },
	{ name: 'Naty', marks: 567, passed: true },
	{ name: 'James', marks: 98, passed: false },
	{ name: 'Andy', marks: 478, passed: true },
	{ name: 'Frank', marks: 180, passed: false },
	{ name: 'Don', marks: 123, passed: false }
];

```

## filter()
The `filter()` method **creates a new array** with all elements that pass the test implemented by the provided function.\
Let us  say we have to get only those students who have passed. So we will filter them as below
```js
const passedStudents = studentData.filter((student) => {
	return student.passed;
});
console.log(passedStudents);

```
Output : 
> [\
  { name: 'John', marks: 634, passed: true },\
  { name: 'Mark', marks: 467, passed: true },\
  { name: 'Randy', marks: 390, passed: true },\
  { name: 'Chris', marks: 564, passed: true },\
  { name: 'Apu', marks: 456, passed: true },\
  { name: 'Naty', marks: 567, passed: true },\
  { name: 'Andy', marks: 478, passed: true }\
]

## map()
The `map()` method **creates a new array** populated with the results of calling a provided function on every element in the calling array.
Say we want to get array of name of every student. So we can get it as follows
```js
const studentNames = studentData.map((student) => {
	return student.name;
});
console.log(studentNames);
```

Output:
>[\
  'John',  'Mark',\
  'Randy', 'Leo',\
  'Chris', 'Apu',\
  'Naty',  'James',\
  'Andy',  'Frank',\
  'Don'\
]

## find()
The `find()` method returns the value of the first element in the provided array that satisfies the provided testing function. If no values satisfy the testing function, `undefined` is returned. Say we want to get data of student whose name is 'Leo' then
```js
const dataOfLeo = studentData.find((student) => {
	return student.name === 'Leo';
});
console.log(dataOfLeo);
```
Output:
>{ name: 'Leo', marks: 149, passed: false }

## reduce()
The `reduce()` method executes a `reducer` function (that you provide) on each element of the array, resulting in single output value. It takes first parameter as `reducer` function and second parameter is `initial value`
Say we want to calculate sum of marks of all students then
```js
const totalMarksOfAll = studentData.reduce((currentTotal, student) => {
	return student.marks + currentTotal;
}, 0);
console.log(totalMarksOfAll);

```
Output:
>4106

## findIndex()
The `findIndex()` method returns the **index** of the first element in the array **that satisfies the provided testing function.** Otherwise , it returns `-1`, indicating that no element passed the test. Say we want to find the index of Leo's Data then
```js
const indexOfLeo = studentData.findIndex((student) => student.name === 'Leo');
console.log(indexOfLeo);
```
Output:
>3

## forEach()
The `forEach()` method executes a provided function once for each array element. It works similar to for loop. Say we want to print result status for each student then 
```js
studentData.forEach((student) => {
	console.log(
		`${student.name} has ${
			student.passed ? 'passed' :
			'failed'} !`
	);
});

```
Output:
>John has passed !\
Mark has passed !\
Randy has passed !\
Leo has failed !\
Chris has passed !\
Apu has passed !\
Naty has passed !\
James has failed !\
Andy has passed !\
Frank has failed !\
Don has failed !

## some()
The `some()` method tests whether at least one element in the array passes the test implemented by the provided function. It returns true if, in the array, it finds an element for which the provided function returns true; otherwise it returns false. It doesn't modify the array. Say we want to know if data have some failed students in it or not then
```js
const hasFailedStudents = studentData.some((student) => {
	return !student.passed;
});
console.log(hasFailedStudents);

```
Output:
>true

## every()
The `every()` method tests whether all elements in the array pass the test implemented by the provided function. It returns a Boolean value. It is similar to `some()` method the only difference is that the `some()` method will return true if any predicate is true while `every()` method will return true if all predicate are true. Say we want to check if all the students are passed or not then
```js
const hasAllPassed = studentData.every((student) => {
	return student.passed;
});
console.log(hasAllPassed);
```
Output:
>false

## New Data
Now , for remaining two methods lets use below data , 
```js
const languages = [
	'java',
	'cpp',
	'python',
	'javascript'
];
```
## includes()
The `includes()` method determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate.
Say we want to check if python and ruby are in above languages array or not then
```js
const includesRuby = languages.includes('ruby');
console.log(includesRuby)
const includesPython = languages.includes('python');
console.log(includesPython);

```

Output:
>false\
true

## indexOf()
The `indexOf()` method returns the first index at which a given element can be found in the array, or -1 if it is not present.
Say we want to find index of python then
```js
const indexOfPython = languages.indexOf('python');
console.log(indexOfPython);
```
Output:
>2

And that is it for this article. Thanks for reading.