---
layout: default
title: JavaScript Style Guide
---

# EY JavaScript Code Style Guide {

*A mostly reasonable approach to JavaScript*

> **Note**: this guide is based on the Airbnb guide [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/blob/master/README.md),
it reinforces the most important rules and revises some of them.

## Table of Contents

1. [Naming](#naming)
2. [Brace](#brace)
3. [Concise Block](#concise-block)
4. [Type Function](#type-function)
5. [ES7](#es7)
6. [Template String](#template-string)

## Naming

<a name="naming"></a>
- **Methods and Functions**: Both should be named with a verb in infinitive + noun.

```js
// bad
const validating = () => {
    //...
};

// bad
const calculatedAge = () => {
    //...
};

// good
const validate = () => {
    // ...
};
```

**[⬆ back to top](#table-of-contents)**

## Brace

<a name="brace"></a>
- Use braces with all single-line blocks.

```js
// bad
if (test) return false;

// good
if (test) {
    return false;
}
```

**[⬆ back to top](#table-of-contents)**

## Concise block

> Consider side-effects when using concise body syntax.

<a name="concise-block"></a>
- Use **concise body** syntax instead of using a body block for single-expression functions.

```js
// bad
const bar = (a, b) => {
    const result = a + b;
    return result;
}

// good
const foo = (a, b) => a + b;
```

**[⬆ back to top](#table-of-contents)**

## Type function

<a name="type-function"></a>
- Use arrow functions for callbacks and function expressions (when you don't need to bind `this`).

```js
// bad
const foo = function(a, b) {
    const result = a + b;
    return result;
}

// good
const bar = (a, b) => a + b;
```

**[⬆ back to top](#table-of-contents)**

## ES7
<a name="es7"></a>
- **Async/Await**: use `async/await` instead of `then` (promises)

```js
// bad
const fetchUser = url => getAuthHeader().then(
    authorization => fetch(url, { headers: { authorization } })
).then(
    response => response.json()
).then(
    data => new User(data.user)
).catch(
    err => console.log(err)
);

// good
const fetchUser = async url => {
    try {
        const response = await fetch(url, {
            credentials: 'same-origin',
            headers: {
                authorization: await getAuthHeader()
            }
        });
        const data = await response.json();
        return new User(data.user);
    } catch (err) {
        console.log(err);
        throw err;
    }
}
```

**[⬆ back to top](#table-of-contents)**

## Template String
<a name="template-string"></a>
- Use template strings instead of string concatenation.

```js
// bad
const greeting = 'Hello ' + name + ', how are you?';

// good
const greeting = `Hello ${name}, how are you?`;
```

**[⬆ back to top](#table-of-contents)**

# }
