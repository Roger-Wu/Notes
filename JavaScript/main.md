iterate through array (es6)
```js
let arr = ['a', 2];
for (let element of arr) {
  // do anything
  console.log(element);
}
```

iterate through keys or values of object (es6)
```js
let obj = {'a': 1, 'b': 2};

let keys = Object.keys(obj);
for (let key of Object.keys(obj)) {
  // do anything
  console.log(key);
}

let values = Object.values(obj);
for (let value of Object.values(obj)) {
  // do anything
  console.log(value);
}
```

iterate through object
```js
let obj = {'a': 1, 'b': 2};
for (let key in obj) {
  if (!obj.hasOwnProperty(key)) {
    continue;
  }
  let value = obj.key;
  // do anything
  console.log(value);
}
```
