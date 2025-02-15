## Duration

The average human reaction time to a visual change is 215ms. Thus, we can say that a duration between 200 and 300ms should be the sweet spot for most animations.

The Modal Human Processor indicates that it takes anywhere between 70ms and 700ms for our eyes to move. This means that the location of the element that is being animated should affect the duration.

Hover transitions should be faster than other animations, as we are focused on the element already. Additionally, our eyes are quite sensitive to color changes, so we can use even shorter duration for color and opacity transitions.

### Effects of Higher vs. Lower Duration:

- Higher duration (slower animation)
  - The animation takes longer to complete.
  - Feels smoother and more elegant.
  - Can make UI feel sluggish if too slow.
  - Useful for emphasizing key transitions (e.g., modals, page transitions).
- Lower duration (faster animation)
  - The animation completes quickly.
  - Feels snappy and responsive.
  - Can feel abrupt or jarring if too fast.
  - Best for small UI interactions (e.g., button clicks, hover effects).

### Guidelines

- Use 150ms for hover effects
- For Modals or popovers, use 200ms for the enter transition and 150ms for the exit, combined with the right easing
- Generally large animation requires more duration
- Typically, animations consist of simple enter and exit transitions, for which an ease-out animation with a duration of 200ms is suitable. This should be the default.
- Don't forget that duration influences the perceived performance of your app. When thinking about the right duration, think about how it will be perceived as well. You should generally keep your animations fast. Animations longer than 700ms should be an exception.

## Purpose

### When should we animate things?

t's easy to start adding animations everywhere. The user then becomes overwhelmed and animations lose their impact. We need to pace them through the experience and add them in places where they enrich the information on the page.

The purpose of most animations should be to add context.

To check whether an animation adds context you can try to describe what benefit it provides to the whole experience. The easier this task is, the more context your animation provides.

- animations that explicitly explain something are useful
- animations to indicate a change in state

### When to avoid animations

- When user would see it soooo many times.
- On key board interactions or something needs instant response.
