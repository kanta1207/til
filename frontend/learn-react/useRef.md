# UseRef (Referencing values with refs & Manipulating the DOM with Refs)

References

- https://react.dev/learn/referencing-values-with-refs
- https://react.dev/learn/manipulating-the-dom-with-refs

## When refs come into play

When you want a component to “remember” some information, but you don’t want that information to trigger new renders, you can use a ref.

## Difference between state and ref

- State:
  - State is retained by React between re-renders.
  - Setting state re-renders a component.
- Ref:
  - Ref is retained by React between re-renders.
  - Changing a ref does not re-render a component.

## When to use refs

- Refs are useful when you need to directly manipulate the DOM or when you need to store a value that doesn’t need to trigger re-renders.
- For example, if you need to focus an input field or scroll to a specific element, you can use a ref.

## Best practices

- Treat refs as an escape hatch:
  - You should only use them when you have to “step outside React”. Common examples of this include managing focus, scroll position, or calling browser APIs that React does not expose.
  - Avoid using refs for state management or data fetching.
  - Prefer state for data that needs to trigger re-renders.
- Use refs for DOM manipulation:
  - If you need to focus an input field or scroll to a specific element, use a ref.
- Use refs for storing values that don’t need to trigger re-renders:
  - If you need to store a value that doesn’t need to trigger re-renders, use a ref.
