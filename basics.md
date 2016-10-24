# Basics about javascript standard code style
I prefer to use es2015 syntax and then compile it to old one. Completly dropped `var` instead of `let` and `const`. It's much more meaningful then `var`'s.

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
