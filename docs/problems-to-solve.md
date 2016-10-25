#Problems to solve
List of problems that we had during development of advertiser dashboard:

1) Too much data in state of components - lack of data flow trough redux, much operations take place in smart component which causes difficulties in components state synchronization. (Igor: maybe it would be better to not use states, just functional components)

2) Some problems were caused by Material UI (it's pretty heavy, a lot of HTML is generated when we use UI components from there). We should consider using another UI framework ( Igor: maybe bootstrap?).

3) There were problems in data mutations, it's too easy to make mutation function which leads to many application bugs. We think that Immutable.js would be best tool to ensure immutability of function args.

4) it would be better to start development of application from dumb components (Daniel: we should consider creating more smart components with smaller responsibility. When we will do that, React would not to have to check should ComponentUpdate on all children. For example root smart component will provide just accessToken and advertiserId props to a couple smart components that will take another props from state. If we make change in one of child of those smart components, React don't have to check it on rest of them).

5) Components interface - how should look interface of components ( hooks ). For example we have low level components like FileUploader which gives you hooks like onSuccess, onFail, ... From those components we create wrappers that looks like VideoVastTag component. VideoVastTag should take care of validation and data integrity for parent component providing nice hook ( onChange props function that is called when someone changed something in those fields. Signature of this function is onChange(isValid,{vastTag,videos}) ) that gives you information if videoVastTag is valid, and all changes made to it. But not every one loved that interface. We should agree on some pattern on this.

6) What tool should we use to do form validation? We used `formsy` but everyone  migrates to https://github.com/erikras/redux-form

7) Console logs. We think that we should use https://github.com/pimterry/loglevel to log stuff in console. We can easily change what type of logs should be display depending on level ( it's easy to disable all logs in prod )

8) Data structure - A lot of problems were caused by difference on assets data format depending on source. This caused a lot of code and added unnecessary complexity to application. We should consider using tools that will help us keep clear object schema ( for example if we get assets data, application itself don't care what is source of data, it cares about required fields in that object). As I saw, Marcin is using Joi.js but it's too big for our requires.

9) Should we use this lib? https://github.com/markdalgleish/redial

10) Will we use some sort of css/scss framework? http://gridle.org/
