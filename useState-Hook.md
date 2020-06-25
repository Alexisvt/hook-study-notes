# useState Hook

## Highlights of this Hook

This Hook returns a stateful value and a function to update it.

```js
const [state, setState] = useState(initialState);
```

If the new state is computed using the previous state, you can pass a function to `setState`. The function will receive the last value and return an updated value.

```js
setCount(prevState => prevState - 1)
```

If your update function returns the same value as the current state, the subsequent *rerender will be skipped entirely*.

Note: Unlike the `setState` method found in class components, useState does not automatically merge update objects. You can replicate this behavior by combining the function updater form with object spread syntax:

```js
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
```

Another option is `useReducer`, which is more suitable for managing state objects containing multiple sub-values.

## Lazy initial state

It is possible to initialize the state in a lazy mode; this is useful when the state is the result of a costly calculation:

```js
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

This function will be executed only on the initial render.

## Bailing out of a state update

If you update a State Hook to the same value as the current state, React **will bail out without rendering the children or firing effects**.

If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.