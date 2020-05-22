# Designing React Components with Redux

_Note: This was written ~2019 and may be out of date_

When starting to create react components, there are several things we must keep at the forefront of our minds.

## Composition

One of the trickiest problems of building a scalable web application (React, Angular, Vue, etc) is designing reusable components from the start.

Most of the time we'll be starting with a design spec to adhere to, this is your chance to think about how the new page, or widget is going to fit in with the entire application.

Just like you would start by thinking about what functionality you should be testing to prove a certain service is behaving as expected, you should take some time to plan out the various components on the screen and define some boundaries.

![](https://static.slab.com/prod/uploads/posts/images/UBnF991GsNM6bbsdpNh1App7.png)

By slicing a design into individual components, you can identify what components you already have in the common library and start bringing them together – composing them.

If an exact match for a common component don't exist for your required design, then you have several options ahead of you:

- Implement your own custom non-reusable feature specific component – this is usually not the best solution as it leads to a higher cost of maintenance of the application
- Look for other common components that are similar but perhaps not exactly the same – ask the designer if it's possible to change the design. The design team may in fact want the old component to be updated to the new styling.
- Look for other components that are not currently reusable and refactor them into the common library.
- Implement your own reusable component and place it into the common library for future reuse

Common components enable consistency through design and ensure that any design changes in the future can be easily made. Think of components similar to utility functions – you'd strive to keep your code DRY by refactoring logic into a single function if possible – components should be no different.

### Dan Abramov's Container vs Presentational Components

A pattern that can be useful for designing composible components [back in 2015](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0) – which is still popular today – described two distinct component types:

1. Container – those that have state, and perform some kind of business function. These potentially complex components often have state, or rely on component lifecycle methods. They would typically be connected to Redux, and would only contain Presentation components. For example a page view (`CollectionDetailsView`), or an action dispatching Button (`BookmarkCollectionButton`)
1. Presentation – those that are purely responsible for rendering some information which they receive through `props`. In most cases they are a PureComponent and have no requirement for state. For example a skeleton, `LessonPlan`, etc.

I agree with Dan's latest update in that these two component styles do not need to be so explicitly differentiated, but keeping this in mind when thinking about composibility certainly does help.

There are certainly some scenarios where a component is only used in one place and needs access to the store, and its parent has access. In this case it wouldn't make sense to make a fully fledged common presentational component to pass the props down just for something that is only used in one place, and only takes properties from the Redux store – in this case I'd argue that you may be prematurely refactoring.

## Testing

Below are some points that are specific to React Components

### Unit testing - needs work

- Test drive the structure of your component
- Write your component "unconnected"
- Test various props being passed in, if using redux for dispatching, test a spy is called under the right circumstances etc.
- Almost always shallow mount your component

### Integration testing - needs work

- Set up the router
- Set up the redux store
- Mount a page view
- Check that you can interact with it

## Styling

Ideally, most of the components that we create are atomic and can be rendered in isolation. They should not rely on other components, or expect to be rendered within a given context.

In this way, the components should contain their own specific styling, a `less` file that lives next to the component, and is `import`ed inside the component will guarantee there is no pollution, or leakage of styling.

A common component, designed to be used throughout the application should contain its own styling and nothing else. It may extend styling from a common source, such as an `antd` button.

A page component, or component that brings together common components into a single view may have a requirement to modify the style of a child component for the purposes of making it look perfect in position.

Of course, when bringing together components into a shared view, there may be situations where there is styling pollution by one or more components. To mitigate this risk, it is important to follow the BEM naming standard.

## Accessibility

_tbc - I don't have a replacment resource to point to_

## Props

Where will your component get its information from? This is a big question and varies depending on the context, depth within the application/page component, and the type of component you're building.

A simple case of a `Button` takes its props from the parent component. More advanced cases may take a video Id from the parent, and expect to be connected to the Redux store to look up the full video.

## Redux

The global application state is managed via Redux, this immutable state system requires actions to be dispatched, and reducers to mutate the state off the back of actions. Middleware can also be deployed to have a side effect on the state of the store, based on actions that are dispatched.

