Questions to answer:

- How can I maintain complex state in apps and when I come back to that piece of code in 6 months, will it be easy to extend functionality?

- Current problem is lacking a method for handling complex state. So far I've used redux and react's context. No documentation was created. Going back to this after a couple of months is hard to understand. Especially when you don't know what properties objects have. Typescript should help with this

Styled-system gave us an easy to understand component styling API. Deleting a component removed that style, unlike creating style components via `styled-components`. We should have a template/rules/methodology of how to deal with any complex state in our app. When we change/delete some functionality, we shouldn't have any code that we might forget to delete. Make state easily deletable!

State checklist:

[] - Define all possible states
[] - Define transition states. How do I go from one state to the next?
[] - Easily deletable so that no extra code is left behind
[] - Can easily be modified/extended (how can I prove this?)
[] - Has documentation
[] - Has tests

Look into x-state. We can define a state machine that we can use to generate state charts for documentation as well as tests. Typescript would help defining the shape of our objects. In a couple of months going back to a part of the app with complex should be easy to understand with documentation + typed objects.
