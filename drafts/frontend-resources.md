# Frontend Resources

Here you will find a list of useful resources that I have come across over time.

# Must Read

I consider these resources a must read for any developer using the following technologies

## React

React is a modern library for rendering dynamic content in on a single webpage, it can also be used for native applications.
There are other libraries in the ecosystem that work very well with it, for example Redux for state management. One unique selling point of React is that it uses a 'virtual DOM' to reduce DOM repaints

- [React JS](https://reactjs.org/docs/getting-started.html) - Component based frontend framework for rendering complex applications
- [Learn Tech React](https://learn.madetech.com/core-skills/react/)
- [freeCodeCamp React Tutorial](https://www.freecodecamp.org/news/best-react-javascript-tutorial/)

## Next.JS

Next.js is a neat frontend and backend application framework that is powered using React. Next will serve pages via an inbuilt (or externally configurable) web server, and provides the ability to maintain serverside code within the same file as client render functions.

- [Next.js](https://nextjs.org/docs) - A frontend and backend application framework for React Applications 
- [lukemorton.co.uk source](https://github.com/lukemorton/lukemorton.co.uk/tree/b8eb88f23cfdb0c9afb141be33b3992186156f63) - Luke's implementation of Next.js on his personal website provides some interesting takes on good practises using the library

## Redux

- [Redux](https://redux.js.org/introduction/getting-started) - A centralised predictable state container for JavaScript apps.
- [Redux (React)](https://react-redux.js.org/introduction/quick-start) - React bindings for Redux using context

## TypeScript 

- [TypeScript](https://www.typescriptlang.org/docs/home.html) - Superset of JavaScript used to guarantee types during development
- ~[TSLint](https://palantir.github.io/tslint/rules/) - A linter we use for ensuring code standards~ TSLint is now deprecated and replaced by ESLint

## Browser Technology

- [Webpack](https://webpack.js.org/concepts/) - The tool that bundles our TypeScript, Less, and HTML into a browser ready package
- [Mozilla Development Network](https://developer.mozilla.org/en-US/) - A great repository of knowledge, all things web

## Testing

The following tools are all very useful, depending on the aim of your tests.

- [Jest](https://jestjs.io/docs/en/getting-started) - A testing tool for JavaScript applications, similar to mocha.
- [Testing Library](https://testing-library.com/docs/intro) - A general testing tool for DOM rendered applications. It has bindings for React, Vue, Angular etc. This library has a different approach to testing which encourages tests to be independent of implementation concerns. Instead, you assert that specific behaviours can be observed.
- [Kent C. Dodds react-testing-library introduction](https://kentcdodds.com/blog/introducing-the-react-testing-library) - Kent C. Dodds is the brains behind the Testing Library, here he gives some examples
- [Enzyme](https://airbnb.io/enzyme/) - A React Component testing utility - this was one of the first libraries to be developed that enables easy testing of React components. It uses a more simplistic approach, encouraging unit tests to be written against prop inputs/outputs and requires a lot of knowledge of the components that you're testing (read: tests become reliant on implementation)
- [jsdom](https://github.com/jsdom/jsdom) - A &#39;fake&#39; DOM designed for testing JavaScript applications. It has some limitations


# Should Read

Depending on the context, there are some other links that are important

- [Ant Design](https://ant.design/docs/react/introduce) - A pre-designed component library akin to bootstrap or material
- [Storybook.js](https://storybook.js.org/docs/guides/guide-react/) - A tool that allows you to render a component in isolation – makes development and styling faster. The tool can also be used to create a reusable component library - ideal for large teams working with the same user interface.

# Other Content

A collection of interesting blog posts that don't necessary belong in the above categories

- [Execute Program](https://www.executeprogram.com/) - &quot;Spaced Repetition System&quot; for learning TypeScript, JS Arrays, regex etc.
- [Modern Javascript Explain For Dinosaurs](https://medium.com/the-node-js-collection/modern-javascript-explained-for-dinosaurs-f695e9747b70) - Evolution of the frontend and all it&#39;s glorious tooling
- [Freecodecamp]
