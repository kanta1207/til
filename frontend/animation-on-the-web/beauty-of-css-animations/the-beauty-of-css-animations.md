## Pure CSS is enough or not

- For simple animations like hover effects, pure CSS is enough.
- Animations have to be feeling right, and the beautiful animations like the ones in iOS are not achievable with pure CSS.
- At the end user don't care if the animation is done with CSS or JavaScript, but they want it to feel right.
- JavaScript animations come with trade-offs:
  - **Performance impact**: JS animations run on the main thread, potentially causing jank if the thread is busy with other tasks
  - **Battery consumption**: More CPU-intensive than CSS animations, which can be hardware-accelerated
  - **Bundle size**: Animation libraries add to your JavaScript payload
  - **Complexity**: Requires more code and maintenance than CSS-only solutions
  - **Accessibility concerns**: Custom JS animations may interfere with user preferences for reduced motion
- While increased bundle size is unavoidable, this is usually not a cause for concern. Frame drops will not be an issue if you animate things in the right way. And you are here to learn this right way.

## Exiting animation in pure CS

```css
/* This just works */
.dialog-content[data-state='closed'] {
  animation: fadeOut 300ms ease-in;
}
```

## When to use CSS animations

Use CSS animations when:

- You need a simple hover effect.
- You need to animate an element in or out.
- You have an infinite, linear animation like a marquee.
- You have a bundle-size sensitive project.

Use Framer Motion/other animation library when:

- You need to create complex animations.
- You want to make your animations feel more sophisticated.
- You want your animations to be interruptible and feel natural.
