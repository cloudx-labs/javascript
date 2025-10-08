# EY React Style Guide() {

*A mostly reasonable approach to React*

> **Note**: this guide is based on Airbnb guide [Airbnb React Style Guide](https://github.com/airbnb/javascript/tree/master/react),
it reinforces the most important rules and revises some of them.

## Table of Contents

1. [Methods](#methods)
2. [Hooks](#hooks)
    - useMemo
    - useCallback
    - useEffect
3. [Naming Conventions](#naming-conventions)
   - Component naming
   - File naming
   - Const and variable naming
4. [Components](#components)
   - Component structure
   - Props
   - Imports

## Methods

<a name="method--placement"></a>
- **Method placement**: if the method doesn't use `this`, it can be a global function at the compilation unit.

<a name="method--purefunction"></a>
- **Method declaration in pure functions**: method declarations should be outside pure functions.

> Why? Methods are created in every execution of the render.

```jsx
// bad
const UserDetails = ({states, user}) => {
    const findState = (states, user) => find(states, state => state._id == user.state);
    return (
        <div>
            {findState(states, user).name}
        </div>
    );
};

// good
const findState = (states, user) => find(states, state => state._id == user.state);

// bad
const UserDetails = ({states, user}) => (
    <div>
        {findState(states, user).name}
    </div>
);

// good
const findState = (states, user) => states.find(state => state._id == user.state);
```

<a name="method--props"></a>
- **Methods and props naming**: handlers of a component should be called `handler`+`event`.

```jsx
// good
const handleSubmit = () => {
    // ...
}

const handleChange = (e) => {
    // ...
}
```

<a name="method--child"></a>
- **Child methods naming**: handlers got from props should be named `on`+`event`.

```jsx
// bad
const UserDetails = ({submit, setChange}) => {
    //...
}

// good
const UserDetails = ({onChange, onSubmit}) => {
    //...
}
```

**[⬆ back to top](#table-of-contents)**

## Hooks

<a name="use--memo"></a>
- **useMemo**: use useMemo always when the result is used in the render.

```jsx
// bad
const UserDetails = ({states, user}) => {
    const state = states.find(state => state._id == user.state);
    return (
        <div>
            {state.name}
        </div>
    );
};
// good
const UserDetails = ({states, user}) => {
    const state = useMemo(() => states.find(state => state._id == user.state), [states, user]);
    return (
        <div>
            {state.name}
        </div>
    );
};
```

**[⬆ back to top](#table-of-contents)**

<a name="use--callback"></a>
- **useCallback**: use useCallback always when the function is passed to a child component

```jsx
// bad
const UserDetails = ({onChange}) => {
    const handleChange = (e) => {
        onChange(e.target.value);
    };
    return (
        <input onChange={handleChange} />
    );
};
// good
const UserDetails = ({onChange}) => {
    const handleChange = useCallback((e) => onChange(e.target.value), [onChange]);
    return (
        <input onChange={handleChange} />
    );
};
```

**[⬆ back to top](#table-of-contents)**

<a name="use--effect"></a>
- **useEffect**: if the effect is used to fetch data, it should be in a custom hook if not put just before the return.

```jsx
// bad
const UserDetails = ({userId}) => {
    const [user, setUser] = useState(null);
    useEffect(() => {
        fetchUser(userId).then(user => setUser(user));
    }, [userId]);
    return (
        <div>{user.name}</div>
    );
};
// good
const UserDetails = ({userId}) => {
    const user = useUser(userId);
    return (
        <div>{user.name}</div>
    );
};
// good
const Foo = () => {
    const location = useLocation();
    useEffect(() => {
        //...
    }, [location]);
    return (
        <div>
            {location.pathname}
        </div>
    );
};
```

**[⬆ back to top](#table-of-contents)**

## Naming Conventions

<a name="naming--conventions"></a>
- **Component naming**: component files should be named with PascalCase and the component inside the file should be named the same.
```jsx
// bad
// userdetails.jsx
const userdetails = () => {
    // ...
};
// good
// UserDetails.jsx
const UserDetails = () => {
    // ...
};
```

- **File naming**: files should be named with camelCase. Only the component files should be named with PascalCase.
```js
// bad
// user_details.tsx
// user-details.ts
// userDetails.tsx
// UserDetails.ts

// good
// UserDetails.tsx
// userDetails.ts
```

```js
// bad
// user_list.jsx
const UserList = () => {
   const users = [];
   //...    
}

// good
// UserList.jsx
const UserList = () => {
    const users = [];
    //...    
}
```

- **Const and variable naming**: use camelCase for variables and UPPER_SNAKE_CASE for constants.
```js
// bad
const maxSize = 10;
const pi_value = 3.14;

// good
const MAX_SIZE = 10;
const PI_VALUE = 3.14;
```

**[⬆ back to top](#table-of-contents)**

## Naming Conventions

<a name="components--structure"></a>
- **Component structure**: component structure should be as follows:

```jsx
// bad
const UserDetails = ({user}) => {
    const [state, setState] = useState(null);
    useEffect(() => {
        //...
    }, []);
   const handleChange = (e) => {
      //...
   };
    const renderUser = () => (
        <div>{user.name}</div>
    );
    return (
        <div>
            {renderUser()}
            <input onChange={handleChange} />
        </div>
    );
};

// good
const UserDetails = ({user}) => {
    const [state, setState] = useState(null);
    const handleChange = (e) => setState(e.target.value);

    useEffect(() => {
        //...
    }, []);

    return (
        <div>
            <div>{user.name}</div>
            <input onChange={handleChange} />
        </div>
    );
};
```

- **Props**: props should be destructured in the function signature.
```jsx
// bad
const UserDetails = (props) => {
    const {user, onChange} = props;
    return (
        <div>
            <div>{user.name}</div>
            <input onChange={onChange} />
        </div>
    );
};
```

```jsx
// good
const UserDetails = ({user, onChange}) => (
    <div>
        <div>{user.name}</div>
        <input onChange={onChange} />
    </div>
);
```

**[⬆ back to top](#table-of-contents)**

- **Imports**: Import organization and best practices for React components.

<a name="imports--specific"></a>
- **Specific imports**: avoid importing everything to reduce bundle size. Import only what you need.

```js
// bad
import * as React from 'react';
import * as utils from '../utils';
```

```js
// good
import { FC, useState, useEffect, useMemo } from 'react';
import { formatDate, validateEmail } from '../utils';
```

<a name="imports--order"></a>
- **Import order**: organize imports in the following order with blank lines between groups:

1. External libraries (React, third-party packages)
2. Internal modules (components, hooks, utils)
3. Relative imports (same directory, parent directories)
4. Type imports (if using TypeScript)

```js
// good
import { useState, useEffect, useCallback } from 'react';
import { Router } from 'react-router-dom';
import { styled } from '@mui/material/styles';

import { Button } from '../components/Button';
import { useAuth } from '../hooks/useAuth';
import { api } from '../services/api';

import './Component.css';
import { validateForm } from './utils';

import type { User, UserProps } from '../types';
```

<a name="imports--default"></a>
- **Default vs named imports**: prefer named imports for better tree-shaking and explicit dependencies.

```js
// bad
import React from 'react';
import utils from '../utils';

// good
import { FC, ReactNode } from 'react';
import { formatDate, validateEmail } from '../utils';
```

<a name="imports--dynamic"></a>
- **Dynamic imports**: use dynamic imports for code splitting when appropriate.

```js
// good - for large components or libraries
const LazyChart = lazy(() => import('../components/Chart'));
const LazyModal = lazy(() => import('../components/Modal'));

// good - for conditional imports
const loadAnalytics = async () => {
  if (process.env.NODE_ENV === 'production') {
    const { analytics } = await import('../services/analytics');
    return analytics;
  }
};
```

<a name="imports--aliases"></a>
- **Import aliases**: use clear and consistent aliases when needed.

```js
// bad
import { Button as B } from '../components/Button';
import { Utils as U } from '../utils';

// good
import { Button as PrimaryButton } from '../components/Button';
import { DateUtils } from '../utils';
```

<a name="imports--types"></a>
- **Type imports**: separate type imports from value imports (TypeScript).

```tsx
// bad
import { FC, useState, User, UserProps } from 'react';

// good
import { FC, useState } from 'react';
import type { User, UserProps } from '../types';
```

**[⬆ back to top](#table-of-contents)**
