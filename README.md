# notes

Notes on front end web development

# Accessibility

### Debugging

- Use a11y web extensions (axe for chrome or firefox)
- You can use Chrome's dev tool audit for a11y but axe's chrome extension goes into more detail. They both use axe engine at the core.
- Check color contrast (axe checks for this)
- Test with keyboard
- Test with screen readers
- Use magnification & zoom

Use this small script to see which element is currently focused

```
document.body.addEventListener('focusin', (event) => {
  console.log(document.activeElement)
})
```

### Keyboard navigation

### Focus management

- Moving the user's focus as part of an interaction to alert them to new content
- Handle focus on disabled and mutated parts of the page
- Reachable and operable elements
- Can use tab, escape and arrow keys
- Visible focus styles
- Hidden/intert content

Tab index - similar to z-index

tabIndex="0" = adds element to tab order
tabIndex="-1" = remove from tab order
tabIndex="99329" = moves element up in tab order heirarchy

tabindex + role + name

Focusable, a button widget (not a DIV) and has an accessible name

```
<div tabIndex="0"
     role="button"
     aria-label="Close">
</div>
```

Intended for custom interactive elements, not wrapper DIVs

Things that need focus management:

- Dropdowns and menus
- Layers and modals
- View changes and deletes
- Loading screens

### Announcements

Notify assistive tech users without moving focus. Below are some patterns where you want to tell the user what is happening

- Asynchronous save/update/etc.
- Combobox usage/list filtering
- Chat widgets
- Title changes

Use ARIA live regions for announcements. You can interrupt or wait
https://www.w3.org/TR/wai-aria/#live_region_roles

Wait: aria-live='polite' / role='status'
Alert: aria-live='assertive' / role='alert'

### Semantic HTML

Use it!

### Colors

Check color contrast. You can use axe for this.

### Resources

### React docs on a11y

- https://reactjs.org/docs/accessibility.html

### Screen reader cheatsheet

- [VoiceOver](https://webaim.org/articles/voiceover/)
- [NVDA](https://webaim.org/articles/nvda/)
- [JAWS](https://webaim.org/articles/jaws/)

### Tools

- https://stuartsandine.com/lighthouse-circle-ci/ (also in performance section)

- axe chrome extension

- [cypress-axe](https://github.com/avanslaars/cypress-axe)

- [jest-axe](https://github.com/nickcolley/jest-axe)

- [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y)

- Checking color contrast ratios: [colorsafe](http://colorsafe.co/) and [contrast ratio](https://contrast-ratio.com/). Chrome's devtools has a tool as well

---

# Analytics

### Google Analytics / tag manager

- Use gtag instead of analytics.js, this is the preferred way

- View -> View settings change All Web Site Data to Raw

- Create a test view

### Gatsby

- Use gatsby-ssr/react-helmet to set the gtag script in the <head>

- Use gatsby-browser onRouteUpdate hook to do page view events

### Setting up views with filters

- Mixpanel

- What to track and why

- Changes that can be made based on analytics

---

# Performance

## Metrics

Tools to get metrics:

- Lighthouse
- WebPageTest
- GTMetrix
- Pingdom Tools

## Performance budgets

- Milestone timings: Good for describing UX and monitoring.
  Some milestons:
- time to first byte
- first contentful paint (fcp)
- when any contentful thing appears in the DOM (text,img, svg, etc.)
- first meaningful paint (fmp)
- when primary content is visible
- time to interactive (tti)
- After fmp, domcontentloaded fired, is visually ready and the user feels like they can engage with the page

- Quantity based metrics: based on raw values that relate to the browser experience
- weight of JS bundle
- number of HTTP requests
- great for monitoring changes over time and raising alarms
- not great for understanding UX

- Rule based metrics: tools that score your webpage
- Lighthouse, WebPageTest, GTMetrix, Pingdom tools

Some budget examples:

- Must score 90+ on Lighthouse accessibility, performance and seo audits
- App must ship less than 170kb js on mobile and < 600kb for desktop
- Page must load in < 2s on ideal desktop situations and under < 5s on Slow 3G and low tier mobile phone
- SpeedIndex must be under 4 seconds

Use bundlesize or size-limit in your project to keep your bundle size in check. Webpack can also set performance budgets. If you are over budget and using React, you can use `React.lazy` for code-splitting.

A helpful tool is [http://www.performancebudget.io/](performancebudget) if you want to create a performance budget for your project.

### First Meaningful Paint (FMP)

Provides the timing when primary content appears on the page, providing an insight into how quickly the server outputs any data. Long FMP usually indicates JavaScript blocking the main thread, but could be related to back-end/server issues as well.

### Time to Interactive (TTI)

The point at which layout has stabilized, key webfonts are visible, and the main thread is available enough to handle user input — basically the time mark when a user can interact with the UI. The key metrics for understanding how much wait a user has to experience to use the site without a lag.

### First Input Delay (FID)

The time from when a user first interacts with your site to the time when the browser is actually able to respond to that interaction. Complements TTI very well as it describes the missing part of the picture: what happens when a user actually interacts with the site. Intended as a RUM metric only.

### Speed Index

Measures how quickly the page contents are visually populated; the lower the score, the better. The Speed Index score is computed based on the speed of visual progress, but it’s merely a computed value. It’s also sensitive to the viewport size, so you need to define a range of testing configurations that match your target audience

### CPU time spent

A metric that indicates how busy is the main thread with the processing of the payload. It shows how often and how long the main thread is blocked, working on painting, rendering, scripting and loading. High CPU time is a clear indicator of a janky experience, i.e. when the user experiences a noticeable lag between their action and a response. With WebPageTest, you can select "Capture Dev Tools Timeline" on the "Chrome" tab to expose the breakdown of the main thread as it runs on any device using WebPageTest.

### Custom metrics

Custom metrics are defined by your business needs and customer experience. It requires you to identify important pixels, critical scripts, necessary CSS and relevant assets and measure how quickly they get delivered to the user. Use Performance API, marking particular timestaps for events that are important for your business. Also, you can collect custom metrics with WebPagetest by executing arbitrary JavaScript at the end of a test.

You can use WebPageTest in your CI to see how a new feature will affect your app

- Real time user metrics (RUM)

- Prometheus + grafana

- What to track and why

- React profiling

- Chrome dev tools profiling

- Build optimization

- Have CI test for lighthouse performance (https://stuartsandine.com/lighthouse-circle-ci/)

Resources:

- https://developers.google.com/analytics/devguides/collection/analyticsjs/user-timings

- https://frontendmasters.com/courses/web-performance/

- https://www.youtube.com/watch?v=UButxfgBljA - The Awesome Web Performance APIs - Dan Shappir

- https://docs.google.com/document/d/1ZKW9N0cteHgK91SyYQONFuy2ZW6J4Oak398niTo232E/edit

- http://siusin.github.io/perf-timing-primer/

- https://css-tricks.com/breaking-performance-api/

- https://developers.google.com/web/fundamentals/performance/why-performance-matters/

- https://ca.godaddy.com/engineering/2018/08/21/real-user-performance-measuring-for-next-js/

- https://www.keycdn.com/blog/user-timing

- https://speedcurve.com/blog/user-timing-and-custom-metrics/

- https://medium.com/the-andela-way/timing-performance-with-performance-hooks-in-node-js-45e666a046a1

- Types:

- NetworkInformation API

- Frame Timing API

- User Timing API

- Navigation Timing API

- Paint Timing API

- Resource Timing API

---

# Testing

- Writing docs on how to easily create a test

- Jest + react testing library
- Create tests that represent how a user uses the app -> integration tests

- Custom helpers to for writing integration tests (mocks for async calls such as graphql or rest, context providers, libraries etc...)

- Cypress testing
- Visual regression testing
- Accessibility
- e2e flows

---

# Visual + Usability -> UI/UX/CSS

Read Refactoring UI.

Writing custom CSS is not great. Adds bloat to an app over time. Use atomic classes such as tachyons or tailwindcss. If using css-in-jss, styled components and styled system are a great combo.

Create design tokens for your app. Having an abstraction over your styles will help you create different themes. As an example for body text: instead of #444 or 'black', you call your color 'text'. When you create a new theme you can reuse 'text' for your new body text color

styled-system + styled-components + theme = 💯

---

# Patterns

## General

- Write wrappers over libraries that are consistently used throughout the app. This could be a network library such as axios or sending events to analytics.

- Use a component library that makes writing UI easy, scalable, accessible, consistent and themeable.

## React

- https://reactpatterns.com/

- https://github.com/vasanthk/react-bits

---

# TypeScript

## Do not do

- Functional changes at the same time

- Be perfect

- Forget to add tests for types

## Converting to TS

### 1

- Rename .js to .ts or .tsx

- Allow implicit any

- Fix things

### 2

- add noImplicitAny: true

- use explicit any if needed

- add types from @types

### 3

- Slowly remove explicit anys and enable strict mode

- strictNullChecks

- strict

- strictFunctionTypes

- strictBindCallApply

- Do this in small chunks

- Try to avoid unsafe casts

## Generics

- When to use

- Type parameters

- Constraints

---

# Testing

You should always have tests. These add a couple of things:

1. Prevents regressions
2. Increases quality of product
3. Tests act as documentation for your feature

## Types of tests

- Unit tests
- Integration tests
- e2e tests

I like to favour integration and e2e tests. Jest tests should be run before every commit. CI should always run jest and cypress tests.

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

## Feature testing

## Performance testing

## Visual testing

## Security testing
