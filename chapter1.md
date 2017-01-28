# Design Patterns

This part of the book will _**not**_ be library/framework specific.

Just some ol' skool ES6/ES2015.

## Builder Pattern

### Introduction

It is an **object creation** pattern.

### Problem

Imagine creating a simple Product class.

```js
class Product {
    constructor(type) {
        this.type = type;
    }
}

const productWithType = new Product('life');
```

So far so good.

Now imagine the real world. You now have to butcher this class because you have _n_ attributes that you need to represent in this class.

```js
class Product {
    constructor(type, price, id) {
        this.type = type;
        this.price = price;
        this.id = id;
    }
}

const productWithEverything = new Product('life', '15', 'sad');
```

Oh God. Creating a product now is _complex_ and _error-prone_. Not only do you need to worry about _what_ this object _**represents**_, you also need worry about its _**construction**_.

The above problem is what the builder pattern attempts to solve.

### How is this pattern useful?

_**Builders separate the construction of a complex object from its representation.**_

As you supply more arguments to your constructor, it becomes harder to reason about what the factory function does.

The following is an example of using the builder pattern to simplify object creation.

```js
class Product {
    constructor(type, price, id) {
        this.type = 'defaultType';
        this.price = 'defaultPrice';
        this.id = 'defaultID';
    }
    withType(type) {
        return new Product(type, this.price, this.id);
    }
    withPrice(price) {
        return new Product(this.type, price, this.id);
    }
    withID(id) {
        return new Product(this.type, this.price, id);
    }
}

const product = new Product()
                    .withType('life')
                    .withPrice('15')
                    .withID('good');
```

Way more readable right?

## Decorator Pattern

### Introduction

A decorator:

* wraps an existing object
* implements the interface of the wrapped object
* extends the functionality of the wrapped object

### Problem

### How is this pattern useful?

## Strategy Pattern

My understanding of the strategy pattern is to have different implementations of the **same behavior **that can be used interchangeably during run-time.

Imagine having a set of configurations defined in the UI of your website.

## Composite Pattern

## Visitor Pattern



