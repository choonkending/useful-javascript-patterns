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
{
    query(request: GraphQLRequest): Promise<GraphQLResult> 
}
```

For those familiar with o[bject-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming), you would know that an _**interface**_ is a collection of abstract methods. If something conforms or implements the interface, you would know you can access the methods provided in the interface.

So, without looking at the Apollo's implementation, I can reasonably expect that _somewhere_ something is doing this:

```js
instanceOfNetworkInterface
.query(someGraphQLRequest)
.then(someGraphQLResult => doSomeThings)
.catch(err => doSomeOtherThings)                                
```

Kewl right? It's like a contract, only without having to sign your life away.

Back to reality now though.

You are doing _**production**_ things in a _**production** _world, so you need to put your _**production**_ hat on to brace for some _**production**_ _**errors**_. Did I mention you are running on production?

You now managed to get this awesome library working, but you need to log errors for monitoring so you can sleep at night.

_**But where do I log it?**_

You _could_ probably do a high level catch-all in your app, a.k.a the catch 'em all

```js
try {
    runMyApp();
} catch (error) {
    doSomeLogging(error);
}
```

Doesn't feel right does it?

You have absolutely no idea _where_ and you resort to some powerful function that will miraculously catches everything.

Hmm...

## How is this pattern useful?



