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

- Arrow functions can be defined and then called immediately.

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

#### REJECTING PROMISES

- To create a rejected promise, we can call `Promise.reject(someReason)`. The "reason" argument tells us why the promise was rejected. Most reasons are `Error` objects, but other JavaScript values are allowed as well.

- We turn the error into a string because JavaScript has no way to represent literal error objects, just as it has no way to represent literal promises. Fortunately, this is more straightforward with errors: the string `Error: oh no` is what we get by calling `.toString()` on the error.

- If we `throw` an exception inside a `then` callback, the exception is automatically converted into a promise rejection. The thrown error becomes the rejection reason.

#### PROMISE CONSTRUCTOR

So far, we've only seen how to create promises with `Promise.resolve` and `Promise.reject`. Those methods are simple and work in many simple situations, so it's a good idea to use them.

However, those methods can't solve all of our problems. For example, how can we delay Promise fulfillment while waiting for a network, a disk, or a timer? Using what we've seen so far, we might try to call `Promise.resolve` inside of a setTimeout.

Thankfully, the new Promise constructor provides a better solution to this problem. We'll start with a simple code example, which is easier than explaining new Promise in words.

```js
> 

new Promise(resolve => resolve(5));

//`resolve` is a function which gets passed as an arguement
// we can call `resolve()` straight away

Async Result:

{fulfilled: 5}
```

We pass a callback function to the `new Promise` constructor. Our callback gets a `resolve` function as an argument. When we call `resolve`, the promise fulfills.

We can call `resolve()` immediately, as in the example above. However, the real power is in calling it later.

We can also use the `new Promise` constructor to create a `rejected` promise. To do that, we accept a second argument in our callback, `reject`.

```js
> 

new Promise((resolve, reject) => reject(new Error('it failed')));

Async Result:

{rejected: 'Error: it failed'}
```

This allows us to accept or reject a promise depending on what happens at runtime.

```js
const users = [
  {id: 1, name: 'Amir'},
  {id: 2, name: 'Betty'},
];

function getUser(id) {
  return new Promise((resolve, reject) => {
    const user = users.find(user => user.id === id);
    if (user) {
      resolve(user);
    } else {
      reject(new Error('no such user'));
    }
  });
}
```

One important thing to keep in mind: the `resolve` function that we get from the constructor is separate from the `Promise.resolve` method. And the `reject` function here is separate from the `Promise.reject` method.

You can think of `Promise.resolve` and `Promise.reject` as the simple versions: when we call `Promise.resolve(5)`, we're creating a new promise that's fulfilled with the value 5. No callback functions are involved, so there's no way for us to delay resolution with `Promise.resolve`.

#### CATCHING EXCEPTIONS

In regular JavaScript, we recover from exceptions with `catch`.

```js
function tryAndCatch() {
  try {
    throw new Error();
  } catch (e) {
    return 'we caught it';
  }
}
tryAndCatch();

// Result:

'we caught it'
```

We can catch promise rejection as well, but not with the usual `try { ... } catch { ... }` syntax. Instead, promises have a `catch` method. When a promise rejects, its `catch` callback (if any) is called.

In some ways, `catch` behaves like `then`. Both take callback functions, and both return promises containing the callback's return value. The main difference is that `then` is called under normal conditions, but `catch` is called only when a promise rejects. With `catch`, we can recover from a rejection, returning a fulfilled rather than rejected promise.

```js
Promise.resolve()
  .then(() => {
    throw new Error('this will reject!');
  })
  .catch(() => 'we caught it');

Async Result:

{fulfilled: 'we caught it'}
```

The `catch` method is the most common error-handling mechanism in promises. But there's another, less common method as well.

So far, our `then` callbacks have always looked like `.then (someValue => ...)`. But `then` actually takes two callback functions as arguments: `.then(onFulfilled, onRejected)`. The `onRejected` callback is called when the parent promise rejects.

```js
Promise.reject(new Error('user does not exist'))
  .then(
    value => 'it fulfilled',
    reason => 'it rejected'
  );

Async Result:

{fulfilled: 'it rejected'}
```

A promise can fulfill or reject, but it can't do both. Only one of the two then callbacks is called: either `onFulfilled` or `onRejected`.

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