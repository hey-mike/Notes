# React Notes
## Communicate Child to Parent
Since there is no way to communicate between siblings (only
parent to child and vice versa), keeping the state at the root
of the hierarchy is the best strategy.


# Spread Operator
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