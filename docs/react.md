# React - best practices
##[WIP] Rules
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


##Libraries
###[WIP] react-immutable-proptypes
https://github.com/HurricaneJames/react-immutable-proptypes
##[WIP] Naming convention

##Best Practices

###Keep your components small (Very Small) [3]
Rule of thumb is that if your render method has more than 10 lines is probably way too big. The whole idea of using React is code re-usability so if you just throw everything in one file you are losing the beauty of React.

###Use ShouldComponentUpdate for performance optimization [3]
React is a templating language that renders EVERY TIME the props or the state of the component changes. So imagine having to render the entire page every time there in an action. That takes a big load on the browser. That’s where ShouldComponentUpdate comes in, whenever React is rendering the view it checks to see if shouldComponentUpdate is returning false/true. So whenever you have a component that’s static do yourself a favor and return false. Or if is not static check to see if the props/state has changed.

###Use Smart and Dumb Components [3]
There is not much to say here other than you don’t need to have a state in every object. Ideally you will have a smart parent view and all the children are dumb components that just receive props and don’t have any logic in it. You can create a dumb component by doing something like this:
```javascript
const DumbComponent = ({props}) => {
  return (<div />);
}
```
Dumb components are also easier to debug because it enforces the top down methodology that React is all about.

###Avoid Refs [3]
Refs will only make your code harder to maintain. Plus when you use refs you are manipulating the virtual Dom directly. Which means that the component will have to re-render the whole Dom tree.

###Use Prop validation [3]
PropTypes will make your life a lot better when working with a large team. They allow you to seemly debug your components. They will also make your debugging a lot easier. In a way you are setting standard requirements for a specific component.

###Change title of application [3]
If you want to change the title of your application dynamically you can do something like this:
```javascript
componentDidMount(){ 
  document.title = "Store Profile" 
}
```

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
[3]:https://medium.com/@nesbtesh/react-best-practices-a76fd0fbef21#.nti9m9ig1
