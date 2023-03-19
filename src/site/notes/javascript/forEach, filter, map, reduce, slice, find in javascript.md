---
{"dg-publish":true,"permalink":"/javascript/for-each-filter-map-reduce-slice-find-in-javascript/","created":"","updated":""}
---


<br ><br >

# ForEach, Filter, Map, Reduce, Slice, Find In Javascript




The array method `forEach` is wonderfully useful, but I see it used in instances where other array methods are a better fit. For those who don’t know what `forEach` does, it effectively replaces a for-loop iterating over an array:

```
<pre class="iw ix iy iz ja jb jc jd">const names = ['karishna', 'sean', 'tayo'];  
const uppercaseNames = [];for (let i = 0; i < names.length; i++) {  
  uppercaseNames.push(names[i].toUppercase());  
}// is the same as  
names.forEach(name => uppercaseNames.push(name.toUppercase()));</pre>
```

It’s a great method as it allows us to bypass all the boilerplate of making a for-loop: no temporary index variable, no checking against the array length, no clunky `arrayName[index]` code to access an element. It is very similar to writing a `for..of` loop, but inline. However `forEach` is arguably the least awesome of the array methods we have available to us in JavaScript. Let’s refactor some for-loops (or `forEach` implementations) into better code with these other methods.

## [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

When to use it: you need a subset of the original array.

How to use it: pass in a _predicate function_ that will be evaluated against each element of the array. If and only if the predicate returns true is the element is included in the resulting array.

```<pre class="iw ix iy iz ja jb jc jd">const positives = [];  
[-1, -4, 3, 8].forEach((n) => {  
  if (n > 0) {  
    positives.push(n);  
  }  
});// with filter  
const positives = [-1, -4, 3, 8].filter(n => n > 0);</pre>
```

## [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

When to use it: you need an array (of the exact same size of the original) whose elements are each derived from their counterparts in the original array.

How to use it: pass in a _transformer function_ that will consume each element in turn and whatever it returns gets pushed to the resulting array.

```js
const capitals = [];  
['a', 'b', 'c'].forEach(l => capitals.push(l.toUppercase()));

// with map  
const capitals = ['a', 'b', 'c'].map(l => l.toUppercase());
```

## [slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

When to use it: you need a subset of the original array, delimited by indexes. (This is also a quick way to copy an array: `const copy = original.slice(0)`.)

How to use it: pass a beginning and (optional) ending index number. Negative indexes count backwards from the end of the array. No “out of bound” errors are ever thrown — a too-large index acts as if `array.length` was passed.

```js
const letters = ['a', 'b', 'c', 'd'];const subset = [];  
letters.forEach((el, i) => {  
  if (i > 0) {  
   copy.push(el);  
  }  
});// with slice  
const subset = letters.slice(1);
```

## [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

When to use it: you need a single value from an array… **usually not one of the elements**. This value can be derived from all or part of the array.

How to use it: pass an _accumulator function_ that accepts the accumulation (what gets returned from each iteration) and the element. Also, pass the initial value for the accumulator as the second parameter of `reduce`.

```js
const sentences = [  
  'See Jane run.',  
  'See John play.',  
  'Write better sentences.'  
];let wordCount = 0;  
sentences.forEach((s) => {  
  wordCount += s.split(' ').length;  
});

// with reduce  
const wordCount = sentences.reduce((count, s) => (  
  count + s.split(' ').length  
), 0);
```

## [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

When to use it: you need the first element in an array that meets some criterion.

How to use it: pass in a _predicate function_ that will be evaluated against each element in the array **until it returns true**. The element it returns true for will be returned from the method and the array iteration will stop.

```js
const nums = [-3, -2, 0, 4];let firstPositive;  
for (let n of nums) {  
  if (n > 0) {  
    firstPositive = n;  
    break;  
  }  
}

// with find  
const firstPositive = nums.find(n => n > 0);
```

## [every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

When to use it: you need to know if every element in the array meets some requirement.

How to use it: pass a _predicate function_ that will be evaluated against each element in the array **until it returns false**. If the predicate returns false, the iteration stops and the whole method returns false. Otherwise it will return true.

```js
>const nums = [1, 2, 3, 4, 5, -6, 7];let isAllPositive = true;  
for (let n of nums) {  
  if (n < 0) { // same as !(n >= 0)  
    isAllPositive = false;  
    break;  
  }  
}

// with every  
const isAllPositive = nums.every(n => n >= 0);
```

## [some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)

When to use it: you need to know if **an** element in the array meets some requirement.

How to use it: pass a _predicate function_ that will be evaluated against each element in the array **until it returns true**. If the predicate returns true, the iteration stops and the whole method returns true. Otherwise it will return false.

```js
const nums = [1, 2, 3, 4, 5, -6, 7];let hasNegative = false;  
for (let n of nums) {  
  if (n < 0) {  
    hasNegative = true;  
    break;  
  }  
}// with some  
const hasNegative = nums.some(n => n < 0);
```

## [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

When to use it: you need to know if a value is in the array.

How to use it: pass in the value to check. Nice ’n’ simple.

```js
let hasBlue = false;  
const colors = ['red', 'yellow', 'blue', 'green'];  
for (let color of colors) {  
  if (color === 'blue') {  
    hasBlue = true;  
    break;  
  }  
}


// with includes  
const hasBlue = colors.includes('blue');
```

## Chaining Array Methods

This is the secret power of using array methods that return arrays — `map`, `filter`, `slice`, and sometimes `reduce`: they can be chained to implement complex operations via simple steps.

```js
let firstTenUnderTenItems = [];  
items.forEach(item => {  
  if (firstTenUnderTenItems.length < 10) {  
    if (item.inStock && item.price < 10) {  
      firstTenUnderTenItems.push(item.name);  
    }  
  }  
}const firstTenUnderTenItems = items  
  .filter(item => item.inStock && item.price < 10)  
  .slice(0, 10)  
  .map(item => item.name);
```

## Bonus: [Object.keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys), [Object.values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values), [Object.entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

When to use them: you are working with objects but wish you were working with arrays!

How to use them: pass in an object to generate an array of either the object’s keys, values, or key-value pairs (entries).

```js
const stringObj = '';  
for (let key in myObj) {  
  stringObj += `${key}: ${myObj[key]},`;  
}

// with Object.entries  
const stringObj = Object.entries(myObj)  
  .map(([key, value]) => `${key}: ${value}`)  
  .join(',');
```

## Conclusion

In my practice, I only reach for `forEach` if I know I’m going to do a side-effect. In this way, it is more clear than the other methods, in that it practically screams, “**side-effect happening here!**” If I enacted some secondary code in the midst of a `map`, it might be lost to the next person to read that code:

```js
// side-effect with map  
callbacks  
  .filter(cb => typeof cb === 'function')  
  .map(cb => cb()) // <-- side effect!
  
  
// with forEach  
callbacks  
  .filter(cb => typeof cb === 'function')  
  .forEach(cb => cb());
```

Since `forEach` always returns `undefined` it will only ever be on the end of a chain of array methods and is easy to spot. (I could have added more array methods after the `map` in the first example and completely obscured that a side-effect occurred in the midst of the chain.)

For all other array manipulations, even to the point of extracting a single value from the array, I use the array methods shown above. They keep the code simple and readable, and tend to be easy to remove from a long chain of manipulations.

While there are cases for performing a side-effect within some other array method, I prefer those to be the exceptions and not the rule. Thus my mantra: **forEach is for side-effects!**



