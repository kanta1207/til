## Spring animations

### What is Spring Animation and when it comes into play

We want to design motion that feels natural and familiar. While using the right type of easing already helps, these easings are made based on a curve and a duration. That means that we can’t create a perfectly natural motion, because the movement in the world around us doesn't have a fixed duration.

Spring animations can help here as they are based on the behavior of an object attached to a spring in a physical world, so it feels more natural by definition.

Spring animations are heavily used in iOS; they're also the default animation in SwiftUI.

Spring animations are also interruptible. Sometimes, when an animations hasn't yet finished, we need to start a new one. When that happens, a spring animation uses the velocity it had when it was re-targeted making the movement feel smooth and natural.

CSS animations are not interruptible. That affects case like when we need to show sooner, if we quickly fire two toasts, the first one will unnaturally jump up to the next position.

**So it comes into play when we need to start a new one even if an animations hasn't yet finished.**

### Should we use spring animations everywhere?

You might be thinking, why use easing if spring animations feel more natural, are interruptible, and so on? Unfortunately, creating actual spring animations in CSS is currently impossible. You can only mimic spring animations using the linear() function, but this remains just an approximation.

Libraries such as Framer Motion or React Spring can help, though their file sizes are quite large. You don't necessarily need spring animations for simple transitions like color or opacity changes; however, they can enhance animations that involve motion, even a simple Toggle. It's a trade-off that requires consideration. However, I strongly believe that this doesn't go unnoticed, even if it's just subconscious. It adds up to the overall feeling of the product in the end.

### Vaul as an example

[Vaul](https://github.com/emilkowalski/vaul) is a library made by Emil Kowalski, it's implemented without using framer motion to keep the package size small. so there's no spring animations.
