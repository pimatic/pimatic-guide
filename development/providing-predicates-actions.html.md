---
title: Providing Rule Predicates and Actions
layout: guide
tags: ['guide', page']
guideOrder: 2070
---

###Actions and Predicates

Actions and Predicates for the rule system are implemented as ActionProvider and PredicateProvider.
There are some common build in Provider in the framework. So in most cases these must not be implemented
by plugins. But if you need a special provider for a plugin specific action you can implement your own.

<div class="alert alert-warning">
	Please note, that these API's aren't fix yet and may change in the future, without a notice.
</div>

###ActionProvider

Let's create a simple action provider that awnsers the question of life the universe and everything.

Each concrete ActionProvider must be a subclass of ActionProvider. The ActionProvider must implement a `parseAction`-function
that is called for every part of the action string of a rule by the framework. If the ActionHandler can handle
the input then it should return a info object with a ActionHandler (see below) that can execute the corresponding
action. 

<script src="https://gist.github.com/sweetpi/492d63290260823cef6c.js?file=action-handler.provider"></script>

The returned ActionHandler must be a subclass of ActionHandler and must implement a 
`executeAction`-function that can be called by the framework.

<script src="https://gist.github.com/sweetpi/492d63290260823cef6c.js?file=action-handler.coffee"></script>

The `executeAction`-function should execute the action if `simulate` is `false`. It should allways return a promise
that gets fulfilled with a description string, after the action was exectured.

Finally you have to register your ActionProvider in the framework.

<script src="https://gist.github.com/sweetpi/492d63290260823cef6c.js?file=action-register.coffee"></script>

For a more complex example, you can take a look at the [shell-execute Plugin](https://github.com/pimatic/pimatic-shell-execute/blob/master/shell-execute.coffee).

###PredicateProvider

PredicateProvider follow the same pattern as ActionProvider, but the function of a PredicateHandler are different.
It follows an Example PredicateProvider that is true if the value of a numeric expression is 42.

<script src="https://gist.github.com/sweetpi/11f7ce564b5ab842ba05.js?file=predicate-provider.coffee"></script>

The corresponding PredicateHandler:

<script src="https://gist.github.com/sweetpi/11f7ce564b5ab842ba05.js?file=predicate-handler.coffee"></script>

and finally the registration:

<script src="https://gist.github.com/sweetpi/11f7ce564b5ab842ba05.js?file=predicate-register.coffee"></script>