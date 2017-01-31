# Higher Order Components

I like calling them HOCs for short. Pronounced HOK because spelling out three letters is excruciating.

Higher Order Components are useful when you wish to implement common functionality among components, or when you see certain implementation details as a _**necessary abstraction**_.

I remember being slightly confused when I first read about _**Higher Order Components**_, because they sounded eerily similar to _**Higher Order Functions**._

| Higher Order Components | Higher Order Functions |
| :--- | :--- |
| Functions that accept a component as an argument and return another component which wraps the given component. | Functions that accept functions as arguments or return a function as a result. |

In my mind, HOCs could be HOFs \(you heard it first from me\).

Here is a simple example of a HOC that adds an additional prop to the given component.

```js
const addHam = ComposedComponent => class extends React.Component {
    render() {
        return <ComposedComponent {...this.props} ham={true} />;
    }
};
```

Remember that you can also declare a stateless function as a component in React. 

```js
// ES6 Class
class Burger extends React.Component {
    render() {
        return <div {...this.props} />
    }
}

// Stateless Function
const Burger = props => <div {...props } />;
```

You could extend functionality to the above component by wrapping it in a HOC.

```js
const addHam = ComposedComponent => props => <ComposedComponent {...props} ham={true} />;
```

Tada! HOCs can be HOFs, but I do think you should always question whether the **HOC you are designing is a necessary abstraction**.

## Real World HOC

In the real world, you might be tasked to implement tracking on page load or some horrendous acts that only happen on _componentDidMount_.

Rather than violating the sanctity that is your beautiful App, you choose to hide the implementation with this abstraction.

```js
const doHorribleThings = ComposedComponent => class extends React.Component {
    componentDidMount() {
        clubBabySeal();
    }
    render() {
        return <ComposedComponent {...this.props} />;
    }
};
```

## Variations to your HOC



If you would like a deeper dive into HOCs, read this excellent post [http://rea.tech/reactjs-real-world-examples-of-higher-order-components/](http://rea.tech/reactjs-real-world-examples-of-higher-order-components/ "Real World Examples of Higher Order Components") by my mate @mehdimollaverdi.


