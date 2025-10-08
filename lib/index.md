---
layout: default
title: Library Usage Guide
---

# EY Library Usage Guide

*Libraries to use in EY projects and how to use them.*

## Table of Contents

1. [Icons](#icons)
2. [Styles](#styles)

## Icons

<a name="icons"></a>
- **Icons**: use [Fluent UI System Icons](https://react.fluentui.dev/?path=/docs/icons-catalog--docs).
> Not use other icon libraries like FontAwesome or Material Icons or @fluentui/react-icons-mdl2.

```jsx
import { Icon } from "@fluentui/react-icons";

const ExampleIcon = () => <Icon />
```

**[⬆ back to top](#table-of-contents)**

## Styles

<a name="styles"></a>
- **Styles**: use [Fluent UI System](https://react.fluentui.dev/) for styling components.
> - Not use other libraries like ant-design.
> - Consider creating another file for styles if the component is big.

```jsx
import { makeStyles, mergeClasses } from "@fluentui/react-components";

const useClasses = makeStyles({
    root: {
        width: "100%",
    },
});

const ExampleComponent = () => {
    const classes = useClasses();
    return (
        <div className={mergeClasses(classes.root, "generic-class")}>
            Example
        </div>
    );
};
```

**[⬆ back to top](#table-of-contents)**
