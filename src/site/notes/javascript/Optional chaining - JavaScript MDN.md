---
{"dg-publish":true,"permalink":"/javascript/optional-chaining-java-script-mdn/"}
---


<br ><br >

# Optional Chaining (?.) - JavaScript  MDN


[Optional chaining (?.) - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining#optional_chaining_with_function_calls)


## Example 1

```JavaScript
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined

```


## Example 2


This returns: Cannot read includes property of undefined if array has item without frontmatter[keyChoice]

```JavaScript
queryFiles = files.filter(file => app.metadataCache.getFileCache(file).frontmatter[keyChoice].includes(queryValue));
```


This 


```JavaScript
queryFiles = files.filter(file => app.metadataCache.getFileCache(file).frontmatter[keyChoice]?.includes(queryValue));
```
