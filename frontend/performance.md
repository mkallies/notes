# Performance

Performance needs to be a 1st class citizen. Try and ship 200-300 kb of uncompressed JS on first load. Use CI to break builds if they go over this budget.
Vendor bundles are an anti-pattern. Vendor caching is only good after someone visits your site since it's cached. First time to visit will download a large vendor bundle.

## Metrics

Tools to get metrics:

- Lighthouse
- WebPageTest
- GTMetrix
- Pingdom Tools
- Chrome Code Coverage

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
