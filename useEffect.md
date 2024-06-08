# Side Effect

- Any operations or behaviors that occur in a component after rendering, and that don’t directly impact the current component render cycle.
- These side effects can include tasks like `data fetching`, `DOM Manipulation`, `HTTP Call`, `Intervals`, `Browser Storage`
- One common use case for handling side effect making an asynchronous data request, such as fetching data from an API.

# `useEffect` Hook

- This hook lets us perform side effects in functional components.
- Effects let you specify side effects that are caused by rendering itself, rather than by a particular event.
- Sending a message in the chat is an event because it is directly caused by the user clicking a specific button. However, setting up a server connection is an Effect because it should happen no matter which interaction caused the component to appear.
- When you begin writing code in React to fetch data from an API, you may encounter an issue where your application enters into an infinite rendering loop. This occurs because **updating the state triggers a re-render**, leading to the execution of the same code again.

* `useEffect()` hooks takes 2 arguments
> useEffect(Effect function,[dependency Array])

**Effect function** is an callback function that contains the side-effect logic and is executed after the component renders first time and after every subsequent render.
**dependency Array** is an optional array of dependencies. Effect function is executed only if the dependencies have changed between rendering.

## Dependency Array items

- All the values from the component scope that change their values between re-renders should be included in the dependency array.
- So we should include the **state variables**, **props**, **context variables** inside the dependency array. Change in these values triggers re-render.

## Dependency Array importance

Dependency Array determines when the effect runs

- **No Dependency Array**: Runs after every render.

```
useEffect(() => {
  console.log('Effect runs after every render');
});
```

- **Empty Dependency Array**: Runs once after the initial render.

```
useEffect(() => {
  console.log('Effect runs only once after the initial render');
}, []);
```

- **Specific Dependencies**: Runs when any of the specified dependencies change.

```
const [count, setCount] = useState(0);
useEffect(() => {
  console.log('Effect runs when count changes');
}, [count]);
```

- **Multiple Dependencies**: Runs when any of the listed dependencies change.

```
const [count, setCount] = useState(0);
const [text, setText] = useState('');
useEffect(() => {
  console.log('Effect runs when count or text changes');
}, [count, text]);
```

- **Changing Dependencies**: Reacts to changes in dynamic dependencies.

```
const [count, setCount] = useState(0);
const [anotherValue, setAnotherValue] = useState(0);
useEffect(() => {
  console.log('Effect runs when count or anotherValue changes');
}, [count, anotherValue]);
```

- **Function/Object Dependencies**: Use memoized values to avoid unnecessary executions.

```
const [count, setCount] = useState(0);
const handleClick = useCallback(() => {
  console.log('Button clicked');
}, []);
useEffect(() => {
  console.log('Effect runs when handleClick changes');
}, [handleClick]);
```

> `useEffect` without dependencies can lead to unintentional side effects and reduced performance, so it's generally a good practice to specify dependencies when possible. Also, always clean up resources in the cleanup function to prevent memory leaks.

## Cleanup in `useEffect`

The cleanup function in `useEffect` is crucial for handling side effects that need to be cleaned up to prevent memory leaks, remove event listeners, cancel network requests, and generally tidy up resources. The cleanup function is returned from the `useEffect` callback and is executed under two main circumstances:

- Before the component unmounts.
- Before the effect re-runs due to changes in dependencies.

```
import React, { useState, useEffect } from 'react';
const TimerComponent = () => {
  const [count, setCount] = useState(0);
  useEffect(() => {
    const interval = setInterval(() => {
      setCount((prevCount) => prevCount + 1);
    }, 1000);
    // Cleanup function to clear interval
    return () => {
      clearInterval(interval);
    };
  }, []); // Empty dependency array, runs only once
  return <div>Count: {count}</div>;
};
export default TimerComponent;
```

## Why we cannot use async in the callback of `useEffect`

The reason is that using callback as async code returns a promise, which React doesnot handle it the way it handles cleanup functions or synchronous values.An effect can only return void or a cleanup function. So using callback as async will give an error

## Using async functions inside of `useEffect`

```
useEffect(() => {
  const fetchData = async () => {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      // Process the data...
    } catch (error) {
      // Handle errors...
    }
  };
  fetchData();
}, []);
```
