# Testing

Why test?

You should always have tests. These add a couple of things:

1. Prevents regressions
2. Increases quality of product
3. Tests act as documentation for your feature

## Types of tests

- Unit tests
- Integration tests
- e2e tests

I like to favour integration and e2e tests. Jest tests should be run before every commit. CI should always run jest and cypress tests.

## Feature testing

## Performance testing

## Visual regression testing

## Security testing

## A11y testing

Tests can catch 30-50% of a11y issues, depending on the rule set

Automated:
Unit tests are good for component-specific behaviour, interaction/focus APIs,
ARIA states

Integration/e2e tests are good for real world browser testing, document/page-level rules, color contrast

- HTML/ARIA validation
- Form labels
- Color contrast
- Accessible names
- Focus management
- Specifying a language

Manual:

- Focus order
- Text alternative quality
- Screen reader
- Keyboard support
- Contrast over images/gradients
- Error identification

## Which tests should we automate?

Automation requires maintenance. As the application changes, we must update the tests. Dependencies change. Lots of automation requires lots of time. Redundant automation is noisy.

Things to ask yourself:

1. What is your gut feeling?
2. What is the risk

- Frequency of use by customers (1-5) x Impact (1-5, if broken what's the impact to customers?)

3. What is the value

- Distinctness: does this test provide new info? x Induction to action: how quickly would this failure be fixed?

4. Cost-efficiency

- Quickness: how quickly can this be scripted x Ease: how easy will it be to script this

5. History

- Similar to weak areas: volume of historical failures in related areas x Frequency of breaks: volume of historical failures for this test

Add up the scores
67-100 Automate
34-66 Possibly automate
0-33 Don't automate

- Accessibility
- Authentication
- Buying a product
- Account functionality

## Actions

1. Use Jest + react testing library
2. Write docs on how to easily create a test for different scenarios

- How and when to mock deps (mocks for async calls such as graphql or rest, libraries etc...)
- How does the end user use the app?
- Test helper functions to use and when

3. Use different tests for different reasons

- Cypress testing
  - e2e is slow, prefer to use this tool for happy paths
- Visual regression testing
  - Check different browsers and different viewports
- Accessibility
  - People with disabilities want to use your app
- Integration
  - Cover edge cases
- Unit
  - Not really needed. Prefer integration because components are rarely used in isolation
