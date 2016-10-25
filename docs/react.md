# React - best practices

###Use Classes[1]

React works well with ES2015 classes.

```javascript
class HelloMessage extends React.Component {  
  render() {
    return <div>Hello {this.props.name}</div>
  }
}
```
We prefer higher order components over mixins so for us leaving createClass was more like a syntactical question rather than a technical one. We believe there is nothing wrong with using createClass over React.Component and vice-versa.

###PropType[1]

If you still don't check your properties, you should start 2016 with fixing this. It can save hours for you, believe me.

```javascript
MyComponent.propTypes = {  
  isLoading: PropTypes.bool.isRequired,
  items: ImmutablePropTypes.listOf(
    ImmutablePropTypes.contains({
      name: PropTypes.string.isRequired,
    })
  ).isRequired
}
```
Yes, it's possible to validate Immutable.js properties as well with react-immutable-proptypes.

###Higher order components[1]

Now that mixins are dead and not supported in ES6 Class components we should look for a different approach.

#####What is a higher order component?

`PassData({ foo: 'bar' })(MyComponent)`
  
Basically, you compose a new component from your original one and extend its behaviour. You can use it in various situations like authentication: 

`requireAuth({ role: 'admin' })(MyComponent)` 

(check for a user in higher component and redirect if the user is not logged in) or connecting your component with Flux/Redux store.

###Use SmartComponents to do as much pre-processing as possible, so your DumbComponents can be really Dumb [2]
   For instance, when you pass a handler to your DumbComponent, curry it with the id, so the DumbComponent doesn’t need to know it:
```javascript
   renderComponents () {
     return <DumbComponent 
       onSelect={this.itemSelected.bind(this, this.props.item.id)}
     >;
   }
```
###Use SmartComponents to ensure that your DumbComponents are ready to render
   Your SmartComponents should be the components in your Route. In your SmartComponent’s render function have a method that makes sure it has the data it needs:
   ```javascript
   render () {
     if (this.hasData()) {
       return this.renderComponents();
     } else {
       return this.renderLoadingScreen();
     }
   }   
 ```

###Use DumbComponents to render *everything* [2]
   Don’t even put a `<div>` in a SmartComponent. It should only ever be composing DumbComponents for you. Separate your concerns — and don’t start just doing “one little thing here”!
   
   Use SmartComponents to generate actions creators.
   When a DumbComponent has an interaction from a user, **it shouldn’t handle any logic itself** — **it should blindly call a function which is passed to it by a SmartContainer and let it do the work**.
   The SmartContainer should then marshal the necessary data and pass it to an action creator.

[1]:https://blog.risingstack.com/react-js-best-practices-for-2016/
[2]:https://medium.com/@tkssharma/react-redux-best-practices-write-production-apps-7c3639e3c447#.ytgt7dszs
