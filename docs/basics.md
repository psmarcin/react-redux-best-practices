# Basics about javascript standard code style
I prefer to use es2015 syntax and then compile it to old one. Completely dropped `var` instead of `let` and `const`. It's much more meaningful then `var`s.

##Naming convection
###File name
* action `name-spearated-by-dash.action.js`
* components `UpperCamelCase.js` - each component in separate directory with styles and tests files
* config `config.<env>.js`
* constants `name-spearated-by-dash.constants-actions.js`
* container `name-spearated-by-dash.container.js`
* logic `<noun>-<verb>.js`
* reducers 
    * initial state `name-spearated-by-dash.initial-state.js`
    * reducer `name-spearated-by-dash.reducer.js`
* store `store-config.<env>.js`


##Libraries
###Normalizr
It's god for store model and to be sure that we have right data with right structure.
>Normalizes deeply nested JSON API responses according to a schema for Flux and Redux apps.
 Kudos to Jing Chen for suggesting this approach.

We will use it for **every** single response from server. 

https://github.com/paularmstrong/normalizr
 
###Immutable.js
>Immutable data cannot be changed once created, leading to much simpler application development, no defensive copying, and enabling advanced memoization and change detection techniques with simple logic. Persistent data presents a mutative API which does not update the data in-place, but instead always yields new updated data.

We will use it for all states. 

https://github.com/facebook/immutable-js

###Pure functions*
All of our functions will be pure. It means that function can not change context and it does not modify arguments or context. It should not depends on context. So for good example:
```javascript
function sum(a,b){
  return a + b
}
sum(2,3) // 5
sum(2,3) // 5
sum(2,3) // 5
```
And now bad example: 
```javascript
let x = 2
function sum(b){
  x += b
  return x
}
sum(3) // 5
sum(3) // 8
sum(3) // 11

```
> * - I know it's not a library :) 

##Tools
###Code style 
I prefer [standardjs](http://standardjs.com/) for linting our code. It's very simple and has strict rules. 
Quick sumup:
> - **2 spaces** – for indentation
> - **Single quotes for strings** – except to avoid escaping
> - **No unused variables** – this one catches *tons* of bugs!
> - **No semicolons** – [It's][1] [fine.][2] [Really!][3]
> - **Never start a line with `(`, `[`, or `` ` ``**
>   - This is the **only** gotcha with omitting semicolons – *automatically checked for you!*
>   - [More details][4]
> - **Space after keywords** `if (condition) { ... }`
> - **Space after function name** `function name (arg) { ... }`
> - Always use `===` instead of `==` – but `obj == null` is allowed to check `null || undefined`.
> - Always handle the node.js `err` function parameter
> - Always prefix browser globals with `window` – except `document` and `navigator` are okay
>   - Prevents accidental use of poorly-named browser globals like `open`, `length`,
>     `event`, and `name`.

> [1]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
> [2]: http://inimino.org/~inimino/blog/javascript_semicolons
> [3]: https://www.youtube.com/watch?v=gsfbh17Ax9I
> [4]: RULES.md#semicolons


###React Dev Tools
Very useful tool for debugging. Git it a try:
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
###Redux Dev Tools
https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd
