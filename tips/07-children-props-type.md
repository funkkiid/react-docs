# Type of the Children props

Usually, a component's children (`this.props.children`) is an array of components:

```javascript
var GenericWrapper = React.createClass({
  componentDidMount: function() {
    console.log(Array.isArray(this.props.children)); // => true
  },

  render: function() {
    return <div />;
  }
});

ReactDOM.render(
  <GenericWrapper><span/><span/><span/></GenericWrapper>,
  mountNode
);
```

However, when there is only a single child, `this.props.children` will be the single child component itself _without the array wrapper_. This saves an array allocation.

```javascript
var GenericWrapper = React.createClass({
  componentDidMount: function() {
    console.log(Array.isArray(this.props.children)); // => false

    // warning: yields 5 for length of the string 'hello', not 1 for the
    // length of the non-existent array wrapper!
    console.log(this.props.children.length);
  },

  render: function() {
    return <div />;
  }
});

ReactDOM.render(<GenericWrapper>hello</GenericWrapper>, mountNode);
```

To make `this.props.children` easy to deal with, we've provided the [React.Children utilities](../docs/ref-01-top-level-api.md#react.children).
