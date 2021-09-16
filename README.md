# NOTES
<!-- 
- [🏀 Promises](#-promises)
<!-- - [🌋 Week Three](#-week-three)
- [🛰️ Week Four](#-week-four)
- [🔮 Week Five](#-week-six)
- [🥌 Week Six](#-week-six)
- [💣 Week Seven](#-week-seven)
- [🛸 Week Eight](#-week-eight)
- [🌵 Week Nine](#-week-nine)
- [🔗 Week Ten](#-week-teb)
- [🧫 Week Eleven](#-week-eleven) -->

### 👀 Functions

Arrow functions can be defined and then called immediately.

`arrowFn = (n => n + 1)(5) //returns 6`

```js
let value = 5;
value = (n => n * 3)(value);
value = (n => n + 1)(value);
value;
```

```js
// Functions that return `objects` can return a `callback` that can be called using `.` notation. 

function chain(value) {
  return {
    value: value,
    then: callback => {
      return       callback(value);
    }
  };
}

chain(5).then(n => n * 3);

// The then in this example could be named anything
```

### 🏀 Promises 

- Promises don't involve assignments like value = ..., so we need to get rid of those. The first step toward that is to introduce a chain function that wraps the value in an object. (The extra whitespace in this example will be filled in with code as we go.)

- Promises use `then` which can see the previous value. 

```js
Promose.resolve(5).then(n => n + 1) // 6
```

- Promises' `then` callbacks are the same. Callbacks attached with `then` don't run immediately; they're only scheduled to run later.

- Using promises feels very different from using `setTimeout`. But in terms of their underlying execution and scheduling, they're quite similar.

- `Promises` are called `promises` because when we create one, we're promising to provide a value at some point in the future.

- `Promises` without an arguement `Promise.resolve()` return `{fulfilled: undefined}` the same as a function without an explicit return statement