---
layout: default
title: Functional Programming Guide
---

# EY Functional Programming Guide() {

*A mostly reasonable approach to functional programing*

## Table of Contents

1. [Map](#map)
2. [Filtering](#filtering)
3. [Immutability](#immutability)
4. [Functional IF](#functional-if)
5. [Functional FOR](#functional-for)
6. [No Set/Map](#no-set-map)
7. [No Mutation](#no-mutation)
8. [Pure Functions](#pure-functions)

## Map

<a name="map"></a>
- **Map Usage**: Map should only be used when a transformation of the data is intended.

```js
// bad
users.map((user, index) => {
    user.order = index + 1;
});

// good
users.forEach((user, index) => {
    user.order = index + 1;
});

// best
const newUsers = map(users, (user, index) => ({...user, order: index + 1}));
```

**[⬆ back to top](#table-of-contents)**

## Filtering

<a name="filtering"></a>
- **Filtering**: Do not use `Array#splice` instead `filter` o `reject` should be used.

 > Why? Splice mutates the original array.

```js
// bad
let arr1 = ['a', 'b', 'c', 'd', 'e'];
const result = array.splice(0, 2);
// array mutates into ['c', 'd', 'e']
// result = ['a', 'b']
```

```js
// good
const arr1 = ['a', 'b', 'c', 'd', 'e'];
const result = arr1.filter(a => a !== 'e');
// result = ['a', 'b', 'c', 'd']
```

**[⬆ back to top](#table-of-contents)**

## Immutability

<a name="immutability--methods"></a>
- **Immutable Methods**: Methods that do not mutate the arguments are preferred.

```js
// bad (mutates original array)
arr.splice(arr.indexOf(value), 1);
```

```js
// good (does not mutate original array)
const newArr = arr.filter(item => item !== value);
```

**[⬆ back to top](#table-of-contents)**

## Functional IF

<a name="functional-if"></a>
- **Functional `if`**: Functional replacement for `IF` statement.

```js
// imperative
const formatUserName = (user) => {
    if (user.disabled) {
        return user.name + ' [disabled]';
    } else {
        return user.name;
    }
};
```

```js
// functional
const formatUserName = user => user.disabled ? `${user.name} + [disabled]` : user.name;
```

**[⬆ back to top](#table-of-contents)**

## Functional FOR

<a name="functional-for"></a>
- **Functional `for`**: Functional replacement for `FOR` statement

```js
const users = [
    { name: 'John', age: 84 },
    { name: 'Mark', age: 34 },
    { name: 'Michael', age: 4 },
    { name: 'James', age: 6 }
]
```

```js
// imperative
const underAge = [];
for (let i = 0; i < users.length; i++) {
    if (users[i].age < 18) {
        underAge.push(users[i].name)
    }
}
```

```js
// functional
const isUnderAge = user => user.age < 7;
const getName = user => user.name;
const getUnderAge = users.filter(isUnderAge).map(getName);
const underAge = getUnderAge(users);
```

**[⬆ back to top](#table-of-contents)**

## No Set/Map

<a name="no-set-map"></a>
- **No Use of `Set` or `Map`**: Avoid using `new Set` or `new Map` for basic array/object operations.

> Why? Using native array and object methods (`filter`, `map`, `reduce`, etc.) keeps code simple, readable, and consistent. `Set` and `Map` introduce additional complexity and are not always necessary for typical data manipulation tasks.

```js
// bad
const unique = new Set(arr);

// good
const unique = arr.filter((item, idx) => arr.indexOf(item) === idx);
```

**[⬆ back to top](#table-of-contents)**

## No Mutation

<a name="no-mutation"></a>
> Why? Mutation breaks referential transparency and makes code harder to reason about.

- **No Mutation**: Avoid mutating arguments or external state inside functions.

```js
// bad
const addItem = (arr, item) => {
    arr.push(item);
    return arr;
}

// good
const addItem = (arr, item) => [...arr, item]
```

**[⬆ back to top](#table-of-contents)**

## Pure Functions

<a name="pure-functions"></a>
> Why? Mutation breaks referential transparency and makes code harder to reason about.

- **Pure Functions**: Prefer pure functions that always return the same output for the same input and have no side effects.


```js
// bad
let counter = 0;
function increment() {
    counter++;
    return counter;
}

// good
const increment = (n) => n + 1
```

**[⬆ back to top](#table-of-contents)**

# }
