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

### 🧱 Objects 

```js
// Object.assign will combine two objects

Object.assign({name: 'Betty'}, {city: 'Nassau'});
```

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

### REGEX

LITERALS

Regular expressions (regexes) are patterns that describe strings. We might write a regex for filenames ending in ".jpg". Or we might write one that recognizes phone numbers.

- `/a/.test('cat')` returns `true`

- `/b/.test('cat')` returns `false`

- `spaces` are characters

WILDCARD

Regexes like `/a/` are literal: they specify exact characters to match. The real power in regexes is in the various operators. The most basic is `.`, the wildcard operator. It matches any character. But the character must be present; `.` won't match the empty string.

- `.` does not match new lines `/n`

- Putting `.` next to another character means that they occur consecutively. For example, `/a./` matches an `"a"` followed by any character. And `/.a/` matches any character followed by an `"a"`.

```
/x..z/.test('xaaz') //true
/x.z/.test('xyz) //true
/x.z/.test('xyyz') //false
```

BOUNDARIES

Often, we want to match text at the beginning and end of strings. We'll use boundaries for that. 

- The first is `^`, which means beginning of string.

- The second boundary is `$`, which means end of string.

- Usually, we want to match an entire string. Most regexes should include these boundaries, `^` and `$`.

- To match only the empty string, we can smash the `^` and `$` together

- If we use the wrong boundaries, there's no error. The regex always returns false.

- 