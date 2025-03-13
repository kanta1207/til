This chapter covers

- The reason code quality matters
- The four goals that high-quality code aims to achieve
- The six high-level strategies we can use to ensure code is of a high-quality
- How writing high-quality code actually saves time and effort in the medium to long term

#### Why code quality matters in short

> Higher quality code tends to produce more reliable, maintainable, and scalable software.

#### 4 fundamental definitions of good code quality

Defining code as being high quality or low quality is an inherently subjective and somewhat judgmental thing. To try to be a bit more objective about it; I personally find it useful to step back and think about what I’m really trying to achieve when I write code. Code that helps me achieve these things is high quality in my mind, and code that hinders these things is low quality.

There are four high-level goals that I aim to achieve when writing code:

- It should work.
- It should keep working.
- It should be adaptable to changing requirements.
- It should not reinvent the wheel.

## Six pillars of good code quality

### Make code readable

Code is hard to read when things below are unclear:

- What it does
- How it does it
- What ingredients it needs (inputs or state)
- What we’ll get after running that piece of code

### Avoid surprises

Even with the best of intentions, writing code that does something helpful or clever can run the risk of causing surprises. If code does something surprising, then the engineer using that code will not know or think to handle that scenario. Often this will cause a system to limp on until some weird behavior manifests far away from the code in question. This might cause a mildly annoying bug, but it might also cause a catastrophic problem that corrupts some important data. We should be wary of causing surprises in our code and try to avoid them if we can.

### Make code hard to misuse

Code is often used by other code, and can be misused. We can maximize the chance that code works and stays working by making things hard or impossible to misuse.

### Make code modular

Modularity means that an object or system is composed of smaller components that can be independently exchanged or replaced.
It’s often beneficial to break a piece of code down into self-contained modules, where interactions between two adjacent modules happen in a single place and use a well-defined interface. This helps ensure that the code will be easier to adapt to changing requirements, because changes to one piece of functionality don’t require lots of changes all over the place.

### Make code reusable and generizable

Reusability and generalizability are two similar but slightly different concepts:

Reusability means that something can be used to solve the same problem but in multiple scenarios. A hand drill is reusable because it can be used to drill holes in walls, in floor boards, and in ceilings. The problem is the same (a hole needs drilling), but the scenario is different (drilling into a wall versus into the floor versus into the ceiling).

Generalizability means something can be used to solve multiple conceptually similar problems that are subtly different. A hand drill is also generalizable, because as well as being used to drill holes, it can also be used to drive screws into things. The drill manufacturer recognized that rotating something is a general problem that applies to both drilling holes and driving screws, so they created a tool that generalizes to solve both problems.

Making code reusable and generalizable allows us (and others) to use it in multiple places throughout a codebase, in more than one scenario, and to solve more than one problem. It saves time and effort and makes our code more reliable because we’ll often be reusing logic that has already been tried and tested in the wild, meaning any bugs have likely already been discovered and fixed.

### Make code testable and test it properly

- Testablity often highly related to modularity

## Writing good quality code slow down us?

Coding the first thing that comes into our heads, without considering the quality of the code, will likely save us some time initially. But we will quickly end up with a fragile, complicated codebase, which becomes increasingly hard to understand or reason about.
