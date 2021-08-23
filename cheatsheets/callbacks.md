# Callbacks

## What is a callback?

A callback is a function that you pass in as a parameter to another function.

Examples:

```js
setTimeout(
    ()=>{
        console.log('hi');
    },
    2000
);
```

```js
setInterval(
    ()=>{
        console.log('hi');
    },
    2000
)
```

```js
const iceCreams = ['Vanilla','Chocolate','Strawberry','Rocky Road'];
iceCreams.forEach(
    (currentElement)=>{
        console.log(currentElement);
    }
)
```


