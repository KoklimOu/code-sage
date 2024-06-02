### When a Regular Variable Isn’t Enough

Here's a component that should show different sculptures when a button is clicked, but it doesn't work as expected:

```javascript
import { sculptureList } from './data.js';

export default function Gallery() {
  let index = 0;

  function handleClick() {
    index = index + 1;
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>
        Next
      </button>
      <h2>
        <i>{sculpture.name}</i> 
        by {sculpture.artist}
      </h2>
      <h3>  
        ({index + 1} of {sculptureList.length})
      </h3>
      <img 
        src={sculpture.url} 
        alt={sculpture.alt}
      />
      <p>
        {sculpture.description}
      </p>
    </>
  );
}
```

### Why This Doesn’t Work

1. **Local Variables Don’t Persist Between Renders**:
   - The variable `index` is a local variable.
   - Each time the component re-renders, it initializes `index` to `0` again.
   
2. **Changes to Local Variables Don’t Trigger Renders**:
   - Changing `index` inside `handleClick` does not tell React to re-render the component.
   - React re-renders components in response to state or prop changes, not local variable changes.

### Solution: Using `useState`

To fix this, you need to:
1. **Retain the data between renders**.
2. **Trigger React to render the component with new data (re-rendering)**.

The `useState` Hook provides these two capabilities:

- **State Variable**: Retains data between renders.
- **State Setter Function**: Updates the variable and triggers a re-render.

Here’s how to update the component using `useState`:

```javascript
import { useState } from 'react';
import { sculptureList } from './data.js';

export default function Gallery() {
  // Declare a state variable named 'index' and a setter function 'setIndex'
  const [index, setIndex] = useState(0);

  function handleClick() {
    // Update the state variable using the setter function
    setIndex(index + 1);
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>
        Next
      </button>
      <h2>
        <i>{sculpture.name}</i> 
        by {sculpture.artist}
      </h2>
      <h3>  
        ({index + 1} of {sculptureList.length})
      </h3>
      <img 
        src={sculpture.url} 
        alt={sculpture.alt}
      />
      <p>
        {sculpture.description}
      </p>
    </>
  );
}
```

### How `useState` Solves the Problem

1. **Retains Data Between Renders**:
   - `useState` declares a state variable `index` that persists between renders.
   
2. **Triggers Re-renders**:
   - `setIndex(index + 1)` updates the state and tells React to re-render the component with the new `index` value.

Now, when you click the "Next" button:
- `handleClick` calls `setIndex(index + 1)`.
- `setIndex` updates the state.
- React re-renders the `Gallery` component with the updated `index`.
- The new sculpture is displayed based on the updated `index`. 
This makes the component dynamic and interactive, correctly updating the displayed sculpture with each button click.
----

### What is `useEffect`?

`useEffect` is a hook in React used to handle side effects in functional components. Side effects include actions like data fetching, setting up subscriptions, and manually manipulating the DOM.

### How Does `useEffect` Work?

1. **Effect Callback Function**: This function contains the side effect logic. It runs after the render is committed to the screen.
2. **Dependency Array**: An optional array that determines when the effect should re-run. It includes variables that the effect depends on.
3. **Cleanup Function**: An optional function returned by the effect callback, which cleans up side effects before the effect re-runs or when the component unmounts.

### When is `useEffect` Triggered?

1. **Initial Render**: The effect always runs after the first render. This is similar to the `componentDidMount` lifecycle method in class components.
2. **Dependency Changes**: The effect re-runs whenever any value in the dependency array changes between renders. This is akin to the `componentDidUpdate` lifecycle method in class components.
3. **Cleanup**: If the effect returns a cleanup function, this cleanup function is run before the effect re-runs due to dependency changes and when the component unmounts. This is akin to the `componentWillUnmount` lifecycle method in class components.

### Examples of `useEffect` Usage

#### 1. Run on Every Render (No Dependency Array)

```javascript
useEffect(() => {
  console.log('Effect runs after every render');
});
```
- **Trigger**: Runs after every render.

#### 2. Run Once on Mount (Empty Dependency Array)

```javascript
useEffect(() => {
  console.log('Effect runs once on mount');
}, []);
```
- **Trigger**: Runs once when the component mounts.

#### 3. Run on Specific Dependency Changes

```javascript
useEffect(() => {
  console.log('Effect runs when count or name changes');
}, [count, name]);
```
- **Trigger**: Runs when `count` or `name` changes.

#### 4. Cleanup Example

```javascript
useEffect(() => {
  const subscription = someAPI.subscribe();
  return () => {
    subscription.unsubscribe();
    console.log('Cleanup on unmount or dependency change');
  };
}, [count]);
```
- **Trigger**: Runs the effect when `count` changes.
- **Cleanup**: Runs the cleanup function before re-running the effect due to `count` change or when the component unmounts.

### Summary

- **Initial Render**: Effect runs after the first render.
- **Dependencies Change**: Effect re-runs if values in the dependency array change.
- **Cleanup Function**: Runs before the effect re-runs due to dependency changes and when the component unmounts.

Using `useEffect` ensures that side effects are managed correctly and efficiently, preventing unnecessary operations and potential issues like infinite loops.
