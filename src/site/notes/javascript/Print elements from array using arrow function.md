---
{"dg-publish":true,"permalink":"/javascript/print-elements-from-array-using-arrow-function/","tags":["javascript"],"created":"","updated":""}
---


<br ><br >

# Print Elements From Array Using Arrow Function

## Method 1

```js
var a = ["a", "b", "c"];
a.forEach(function(entry) {
  console.log(entry);
});

```


## Method 2

```js
var a = ["a", "b", "c"];
a.forEach((element) => {
        console.log(element)
    }
);

```

<br ><br >


