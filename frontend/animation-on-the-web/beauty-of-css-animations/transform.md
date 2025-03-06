## What is transform?

- The CSS transform property allows us to change how a given element looks.
- It's very powerful, because it's not only about moving the element on the y or x axis. We can move it, rotate it, scale it, and translate it. This unlocks a lot of possibilities when it comes to animations.

- Translate
- Scale
- Rotate
-

### Translate

- The translate function allows us to move an element around
- Using translate doesn't change its position in the document flow, meaning that other elements position will not be affected by the element's movement.
- Unlike margin or padding, when using percentages, the element will be moved relative to its own size. Setting translateY(100%) for example, will move the element down by its own height.

### Scale

- The scale function allows us to resize an element.
- It works as a multiplier, scale(2) will make the element twice as big, scale(0.5) will make it half as big.
- We can also use scaleX and scaleY to only scale the element on one axis, or just use scale with two values to scale on both axes (scale(x, y)). This is less common as it'll usually look bad.
- Unlike width and height, scaling an element scales its children as well, which is a good thing. When scaling a button on click we want its font size, icons, etc. to scale as well.
- Usecases:
  - Entering object
  - Clicking button
  - Zooming up the image
- Tip for using scale() is to (almost) never animate from scale(0). Instead, you can combine an initial scale like 0.5 with opacity animation like I did for Clerk's toast.

### Rotate

- Just rotate the element.

### 3D Transform

- We can also use rotateX and rotateY in combination with `transform-style: preserve-3d` to rotate an element around a specific axis. This is useful for creating 3D effects
- You can implement kinda rich 3d animations with this. (https://animations.dev/learn/css-animations/transforms#3d-transforms)
