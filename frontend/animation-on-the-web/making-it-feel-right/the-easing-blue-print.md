Reference: https://animations.dev/

Easing has significant impact on the feel of an animation.

## Different types of easing and when to choose

### Ease-out

- Fast start, slow end.
- Good for user-initiated actions(ex. opening a modal), because fast start gives user a sense of instant response.
- Slow end makes it natural?

### Ease-in-out

- Slow start and end.
- Good for anything that is already on the screen and needs to move to a new position, or morph into a new form.
- Don't give user a surprise when something start to move or transform, and don't take too long in the transition, and slow end adds more natural feel at the end.

### Ease-in

- Slow start, fast end.
- Generally can be avoided
- If you need something appears to screen reacting to user's action, use ease-out.
- If you need something already on the screen to move to a new position, use ease-in-out.

### Linear

- Constant speed.
- Tends to be robotic and unnatural.
- Only good use case it where there is no user interaction at all.

### Ease

- start faster and ends slower than ease-in-out.
- Good for hover effects that transition color, background-color, opacity, etc.

### Custom easing

- When built in easing is not strong enough, or you need to create a unique effect.

```css
:root {
  --ease-in-quad: cubic-bezier(0.55, 0.085, 0.68, 0.53);
  --ease-in-cubic: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  --ease-in-quart: cubic-bezier(0.895, 0.03, 0.685, 0.22);
  --ease-in-quint: cubic-bezier(0.755, 0.05, 0.855, 0.06);
  --ease-in-expo: cubic-bezier(0.95, 0.05, 0.795, 0.035);
  --ease-in-circ: cubic-bezier(0.6, 0.04, 0.98, 0.335);

  --ease-out-quad: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  --ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1);
  --ease-out-quart: cubic-bezier(0.165, 0.84, 0.44, 1);
  --ease-out-quint: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-out-expo: cubic-bezier(0.19, 1, 0.22, 1);
  --ease-out-circ: cubic-bezier(0.075, 0.82, 0.165, 1);

  --ease-in-out-quad: cubic-bezier(0.455, 0.03, 0.515, 0.955);
  --ease-in-out-cubic: cubic-bezier(0.645, 0.045, 0.355, 1);
  --ease-in-out-quart: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-in-out-quint: cubic-bezier(0.86, 0, 0.07, 1);
  --ease-in-out-expo: cubic-bezier(1, 0, 0, 1);
  --ease-in-out-circ: cubic-bezier(0.785, 0.135, 0.15, 0.86);
}
```

## Other resources

- https://www.youtube.com/watch?v=fZpTvZuysIo
