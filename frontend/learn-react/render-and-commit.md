# React Rendering and Commit

Reference: https://react.dev/learn/render-and-commit

## Steps until we see React components on the screen

## Step 1: Trigger a render

There are two reasons for a component to render:

1. Initial render

   - When your app starts, you need to trigger the initial render
   - Done by calling `createRoot` with the target DOM node and calling its `render` method with your component

   ```jsx
   const root = createRoot(document.getElementById('root'));
   root.render(<App />);
   ```

2. State updates
   - When a component's state is updated using the set function (e.g., `setState`)
   - React automatically queues a render when state updates
   - Like a restaurant guest ordering additional items after their first order

## Step 2: Render

During this phase, React calls your components to determine what should be on the screen:

- For initial render: React calls the root component
- For re-renders: React calls the function component whose state update triggered the render
- Process is recursive - React will continue rendering nested components until there are no more to render
- Rendering must be pure:
  - Same inputs should give same outputs (like a predictable food order)
  - Components should not change existing objects/variables (no affecting other orders)
- React calculates what has changed since the previous render

## Step 3: Commit(Update DOM)

After rendering your components, React modifies the DOM:

- For initial render: React uses the DOM API to put all DOM nodes on the screen
- For re-renders: React only applies the minimal necessary changes to make the DOM match the latest rendering output
- React only changes the DOM nodes if there's a difference between renders
- After React commits changes, the browser will repaint the screen

## Step 4: Browser paint (Browser Rendering)

The final step where the browser repaints the screen:

- Browser takes the DOM changes React committed and paints the final pixels to the screen
- Known as "browser rendering" (different from React rendering)
- Browser handles this step automatically - React's job is done after committing DOM changes
