# Design Patterns

This part of the book will _**not**_ be library/framework specific.

Just some ol' skool ES6/ES2015.

## Builder Pattern

It is an **object creation** pattern.

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

There you go! The above problem is what the builder pattern attempts to solve.

> Builders separate the construction of a complex object from its representation.

As you supply more arguments to your constructor, it becomes harder to reason about what the factory function does.

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
        return new Price(this.type, price, this.id);
    }
    withID(id) {
        return new Price(this.type, this.price, id);
    }
}

const product = new Product()
                    .withType('life')
                    .withPrice('15')
                    .withID('good');
```



