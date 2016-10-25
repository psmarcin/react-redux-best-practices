#Redux - best practices


##Naming convetion
###How to name your XXX [1]
Naming things is hard. But so is managing state, and Redux takes the pain out of that so can we name things simply as well?

Actions: 
>Name them \<noun>-\<verb>, eg project-create, user-login. The rationale behind this is that you want them grouped together by the object type, rather than the action type.

Reducers: 
>Name them \<noun>.


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

