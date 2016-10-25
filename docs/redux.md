#Redux - best practices
##Rules [2]
1. Your reducers must be **pure** (deterministic).
2. Any logic with side effects (non-deterministic) (external services, async code) belong in an action (via something like redux-thunk)
4. Containers read a store’s data through selectors. Selectors are your “reading API” and should be co-located with their reducers.
6. Use selectors everywhere. Even for the most trivial ones.
7. Redux should store the minimal possible state, allowing Selectors to compute derived data.
8. Use Reselect for selectors that need to be memoized (like derived data).
9. Selectors can be composed of other selectors
10. Normalize your data for better reducer composition
    1. See the output of normalizr for an example
11. Totally OK to have many, many reducers.
12. We will use 
https://github.com/erikras/ducks-modular-redux with https://github.com/acdlite/redux-actions
for structuring redux actions

## Libraries
###[WIP] redux-action [?]
> Wraps an action creator so that its return value is the payload of a Flux Standard Action. If no payload creator is passed, or if it's not a function, the identity function is used.
https://github.com/acdlite/redux-actions



##Naming convetion
###Actions [2]

**DO** name each action (constant) as `<NOUN>-<VERB>` with the present tense

**Why?** For namespacing and sorting your reducers

```
TODO_ADD
```

**DO** build your action creators using redux-actions’s `createAction()`

**Why?** To reduce boilerplate and enforce FSA-compliant actions

```
createAction( ‘TODO_ADD’ )
```

**DO** name each action creator as `<verb><Noun>`

**Why?** As a convention to clearly identify what type of function it is

```
const addTodo = createAction( ‘TODO_ADD’ )
```

###Selectors [2]
**DO** name each selector as get<Noun>

**Why?** As a convention to clearly identify what type of function it is

```const getTodo = (state) => state```

###Reducers [2]
**DO** build your reducers using redux-actions’ `handleActions()`
```javascript
export default handleActions({

  TODO_ADD: (state, action) => ([
    ...state,
    action.payload,
  ]),

  // Other reducers
  // ...
  //

}, initialState )
```
**Why** this instead of the documented switch statement? Primarily because it keeps a clean switch-like syntax, while adding block scoping to the cases. This means you can reuse variable of the names in each “case”. With switch, your cases are scoped to the switch, so you are forced to use var or unique names.

##Best Practices

###Use reducers to keep your state in sync[1]
The interesting thing here is that a reducer can handle any action at all. One neat thing to do is when a user logs out, clear all your stores.
switch (action.type) {
   ...
   case USER_LOGOUT: 
     return {}
}

###Use ActionCreators to translate application data structures to API data structures.[1]
Your ActionCreators are responsible for converting the data in your application’s format to the format of the API to which you are communicating. This is in both directions — when making the request or handling the response.
Because the output of an action is handled by a reducer that has no knowledge of how it was called, you might find that sometimes you can’t merely return the result of an API call — you need to enrich it extra data, eg: if your action is PROJECT_UPDATE, and you pass a new project name and the project id, and the API just returns {savedAt: “<some date>”}, then you will need to pass the data from the arguments into the response:
```javascript
function updateProject(projectId, projectName) {
  request.put(`/project/${projectId}`, {projectName}).then(
    response => Object.assign(
      {projectId, projectName}, 
      response.data
    )
  );
}
```



[1]: https://medium.com/@tkssharma/react-redux-best-practices-write-production-apps-7c3639e3c447#.ytgt7dszs
[2]: https://medium.com/@kylpo/redux-best-practices-eef55a20cc72#.1isrqgmze
