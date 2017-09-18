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
