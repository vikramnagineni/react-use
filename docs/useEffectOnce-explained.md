The provided code showcases a React functional component named `Demo` that utilizes the `useEffectOnce` hook from the `react-use` library. Here's a breakdown:

1. **Import**:
   - `useEffectOnce`: Imported from the `react-use` library, this hook is a utility that ensures a side effect is run only once when the component mounts.

2. **Demo Component**:
   - Inside the component, the `useEffectOnce` hook is invoked with a callback function.
     - When the `Demo` component mounts, the line `console.log('Running effect once on mount')` will execute, logging the provided message to the console.
     - The callback function also returns a clean-up function. This clean-up function runs when the `Demo` component is unmounted from the React DOM. When this happens, the line `console.log('Running clean-up of effect on unmount')` will execute, logging its message to the console.
   - The component renders `null`, meaning it doesn't visually render anything in the DOM.

### Usage:

When the `Demo` component is used in an application and is mounted, you'll see the message "Running effect once on mount" in the console. If the component is subsequently unmounted from the DOM (e.g., due to a route change or conditional rendering), you'll see the message "Running clean-up of effect on unmount".

The primary purpose of this code is to demonstrate the behavior of the `useEffectOnce` hook and how it can be used to run side effects upon mounting and cleanup upon unmounting, without re-running the effect on component updates.


how the cleanup code runs?

In React, the cleanup code inside the `useEffect` hook runs when the component is unmounted, but it's not limited to just that scenario. Here's how it works:

1. **Component Mounts**:
   When the component first mounts, the function passed to `useEffect` (or `useEffectOnce` in your provided example) is executed.

2. **Component Updates**:
   If you're using the standard `useEffect` hook with dependencies (specified in the dependency array), the cleanup function will run before re-invoking the effect function on subsequent renders when the dependencies have changed. This ensures any side effects from the previous render are cleaned up before applying new ones.

3. **Component Unmounts**:
   When the component is unmounted from the DOM, the cleanup function runs to perform any necessary cleanup tasks, like clearing timers, canceling network requests, or cleaning up subscriptions.

In your provided example with `useEffectOnce`:

```javascript
useEffectOnce(() => {
  console.log('Running effect once on mount')

  return () => {
    console.log('Running clean-up of effect on unmount')
  }
});
```

The effect function logs "Running effect once on mount" when the component mounts. The cleanup function, which logs "Running clean-up of effect on unmount", is returned from the effect function but is held onto by React. It will be executed when the component is unmounted from the DOM.

In essence, the cleanup function is a way for you to specify how to "undo" or "clean up" any side effects that were introduced when the component mounted or updated. It's a mechanism provided by React to ensure that components don't leave unwanted artifacts behind, especially when dealing with external resources or subscriptions.