# notes

Notes on front end web development

# Accessibility

### Keyboard navigation

### Tab trapping

### Screen readers

### Semantic HTML

### Focus control

### ARIA

### Colors

### Resources

### Tools
- https://stuartsandine.com/lighthouse-circle-ci/ (also in performance section)

- [cypress-axe](https://github.com/avanslaars/cypress-axe)

- [jest-axe](https://github.com/nickcolley/jest-axe)

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

### Metrics

#### Performance budgets

- Milestone timings: what is the user experience when loading a page?
 - time-to-interactive (tti) or first contentful paint (fcp)

- Quantity based metrics: based on raw values that relate to the browser experience
 - weight of JS bundle
 - number of HTTP requests

- Rule based metrics: tools that score your webpage
 - Lighthouse, WebPageTest, GTMetrix, Pingdom tools

Some budget examples:
- Must score 90+ on Lighthouse accessibility, performance and seo audits
- App must ship less than 170kb js on mobile and < 600kb for desktop
- Page must load in < 2s on ideal desktop situations and under < 5s on Slow 3G and low tier mobile phone
- SpeedIndex must be under 4 seconds

Use bundlesize or size-limit in your project to keep your bundle size in check.  Webpack can also set performance budgets.  If you are over budget and using React, you can use `React.lazy` for code-splitting.

A helpful tool is [http://www.performancebudget.io/](performancebudget) if you want to create a performance budget for your project.

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

- Jest + react testing library
- Writing docs
- Custom helpers: make testing easy
- Context Providers / Async calls (Graphql, REST endpoints)
- Cypress testing
- Visual regression testing
- Accessibility
- e2e flows

---

# UI/UX

- Refactoring UI

- Design tokens

- Theme + styled system + css-in-js

---

# Patterns

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