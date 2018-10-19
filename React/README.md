# React Notes

## Communicate Child to Parent

Since there is no way to communicate between siblings (only
parent to child and vice versa), keeping the state at the root
of the hierarchy is the best strategy.

## Spread Operator

"spread" operator to pass the whole props object.

```JSX
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

## Object rest spread (Redux example)

http://redux.js.org/docs/recipes/UsingObjectSpreadOperator.html

## Required module as default

- Create a index.js module
- improt A from './folder_name'

## React Router

`withRouter` will cause rerender if enable it in `Route`, it has bo be used when export component.

## PurComponent

A PureComponent will always re-render if the state or props reference a new object. This implies that if we do not want to lose the benefits of PureComponent, we should avoid such structures:

```
<Entity values={this.props.values || []}/>
```

It is important to remember, that PureComponent skips the re-render operation not only for component itself, but also for all its children, so the best use case for PureComponent are presentational components which have no child components and no dependencies on the global state in the application.

## Fragment

A common pattern in React is for a component to return multiple elements. Fragments let you group a list of children without adding extra nodes to the DOM.

## Using the state

1. We should always keep in mind that only the minimal amount of data needed should be put into the state
1. We should add to the state only the values that we want to update when an event happens, and for which we want to make the component re-render.

## Should component update

1. Dont' duplicate data from props in state, calculate what you can in render() method
1. Don't keep something in the state if you don't use it for rendering, For example, API subscriptions are better off as custom private fields or variables in external modules.

## Container and Presentational pattern

`Container components`

- They are more concerned about the behavior
- They render their presentational components
- They make API calls and manipulate data
- They define event handlers
- They are written as classes

`Presentational components`

- They are more concerned with the visual representation
- They render the HTML markup (or other components)
- They receive data from the parents in the form of props
- They are often written as stateless functional components

## Function as Child

```React
const FunctionAsChild = ({ children }) => children()

FunctionAsChild.propTypes = {
  children: React.PropTypes.func.isRequired,
}
```

## Uncontrolled Components

where we do not set the value of the input field, but we let the component manage its internal state.

## Controlled Components

We have full control over the value of the fields

## Event

- Synthetic Event

A Synthetic Event is an object that wraps the original event object provided by the browser, and it has the same properties, no matter the browser where it is created.

- single global handler
- event bubbling: What it does instead is attach a single event handler to the root element, which listens to all the events,
- single global handler : When an event we are interested in is fired by the browser, React calls the handler on the specific components on its behalf.

## Server side rendering

- SEO :One of the main reasons we may want to render our applications on the server-side is Search Engine Optimization (SEO).
- A common code base: We do not have many options on the client: our applications have to be written in JavaScript. There are some languages that can be converted into JavaScript at build time, but the concept does not change.
- Better performance:we all love client-side applications, because they are fast and responsive, but there is a problem: the bundle has to be loaded and run before users can take any action on the application.

`SSR or not`

- If your page is non-interactive don't render it in the browser (Only render the page to HTML on the server.) (Not only is computational time saved by skipping rendering to the DOM but also load time is saved by skipping loading JavaScript code.)

- If your page is non-interactive and doesn't change on every request, then render it on the server at build-time.

- The SSR should be enabled on when strictly needed. For example, if you need SEO or if you need to customize the social sharing information, you should start thinking about it.

- If you realize that your application takes a lot of time to fully load and you have already done all the optimization (see the following chapter for more about this topic), you can consider using server-side rendering to offer a better experience to your users and improve the perceived speed.