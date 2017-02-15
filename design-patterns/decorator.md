# Decorator Pattern

## Introduction

A decorator:

* wraps an existing object
* implements the interface of the wrapped object
* extends the functionality of the wrapped object

## Problem

Let's take a look at an actual real world problem. Recently, we had to implement a [network interface](http://dev.apollodata.com/core/network.html#NetworkInterface) for [Apollo](http://dev.apollodata.com/).

The _interface_ of the NetworkInterface looks like below:

```js
query: (request: GraphQLRequest) => Promise<GraphQLResult> 
```

For those familiar with [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming), you would know that an _**interface**_ is a collection of abstract methods. If something conforms or implements the interface, you would know you can access the methods provided in the interface.

So, without looking at the Apollo's implementation, I can reasonably expect that somewhere out in the wild someone will do something along the lines of:

```js
instanceOfNetworkInterface
.query(someGraphQLRequest)
.then(someGraphQLResult => doSomeThings)
.catch(error => doSomeOtherThings)                                
```

Kewl right? It's like a contract, only without having to sign your life away.

Back to reality now though.

### Challenge: Logging

You are doing _**production**_ things in a _**production** **world**_, so you need to put your _**production**_ hat on to brace for some _**production errors**_. Did I mention you are running on production?

You now managed to get this awesome library working, but you need to _**log network errors**_ for monitoring so you can sleep at night.

_**But where do I log it?**_

You _could_ probably do a high level catch-all in your app, a.k.a the catch 'em all

```js
try {
    runMyApp();
} catch (error) {
    doSomeLogging(error);
}
```

However, it feels like logging network errors is a concern of _**Network Interface**_ rather than your entire App.

We don't really want to modify _**Network Interface**_ because we don't have access to it and more importantly, even if we did, we want to ensure it doesn't do more than one thing. I'm looking at you, [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single_responsibility_principle "Single Responsibility Principle").

Let me cut to the chase. What we wish for is to **extend the functionality** of the original interface while conforming to the Single Responsibility Principle.

The decorator pattern is a neat way of achieving this. We can _wrap_ the original object and implement the same interface of the original object.

```js
const original = {
    doSomething: () => null
};

const decorator = obj => {
    doSomeOtherThings();
    return {
        doSomething: () => obj.doSomething()
    };   
}
```

Here's how we can _decorate_ our _**Network Interface**_ nicely!

```js
const logNetworkErrors = networkInterface => ({
    query: request => networkInterface
                        .query(request)
                        .catch(error => {
                            console.error(error);
                            throw error;                    
                        })
});

// Usage
const decoratedNetworkInterface = logNetworkErrors(originalNetworkInterface);
```

Because we implement the same interface, any consumers of _decoratedNetworkInterface_ do not need to:

* Change
* Know the internals of the logNetworkErrors. In fact, they don't need to know that we are not using the original _**NetworkInterface**_ directly!



