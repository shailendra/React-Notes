# React-Notes



## JSX
### Simple JSX Element
```javascript
const JSX = <div>Hello</div>;
```

<br>

### Complex JSX Element and Add Comments
```javascript
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    {/* comment */}
    <p>Here's a subtitle</p>
  </div>
);
```

<br>

### Render JSX to the DOM
```javascript
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);

ReactDOM.render(JSX, document.getElementById('root'));
```

<br>


### Define an HTML Class in JSX and other attributes
To define class in JSX uses **className** attribute.<br>
The naming convention for all HTML attributes and event references in JSX become camelCase. For example, a click event in JSX is **onClick**, instead of onclick. Likewise, onchange becomes **onChange**. While this is a subtle difference.
```javascript
const JSX = (
  <div className='myDiv'>
    <h1>Add a class to this div</h1>
    <button onClick={this.handleClick}>Click Me</button>
  </div>
);
```

<br>


### Stateless Functional Component
```javascript
const MyComponent = function () {
  return (
    <div> Hello React</div>
  );
}

// using Arrow Function
const MyComponent = () => {
  return (
    <div> Hello React</div>
  );
};
```

<br>


### React Component
To define a React component is with the ES6 class syntax. In the following example, Kitten extends React.Component
```javascript
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

<br>


### Nested Components
TypesOfFruit components is nested in Fruits.
Fruits component is nested in TypesOfFood.
```javascript
const TypesOfFruit = () => {
  return (
    <div>
      <h2>Fruits:</h2>
      <ul>
        <li>Apples</li>
        <li>Blueberries</li>
      </ul>
    </div>
  );
};

const Fruits = () => {
  return (
    <div>
      <TypesOfFruit/>
    </div>
  );
};

class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits/>
      </div>
    );
  }
};
```

<br>

### Render a Class Component to the DOM
```javascript
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
      </div>
    );
  }
};

ReactDOM.render(<TypesOfFood/>, document.getElementById('root'));
```

<br>

### Pass Props to a Stateless Functional Component
```javascript
// Stateless Functional Component
const CurrentDate = (props) => {
  return (
    <div>
      <p>The current user is: {props.user}</p>
      <p>The current date is: {props.date}</p>
      <p>The current date is: {props.colors.join(', ')}</p>
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>

        {/* passing props to Stateless Functional Component */}
        <CurrentDate
          user='Shailendra'
          date={Date()}
          colors={['red', 'blue', 'green']}
        />


      </div>
    );
  }
};
```

<br>

### Default Props and Override Default Props
```javascript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}
//-----------------------
// Assigning default props
Items.defaultProps = {
  quantity: 0
}
//------------------------

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>

         {/* automatically default props value 0 will set */}
        <Items />


         {/* below will override default props value with 10 */}
        <Items quantity={10} />
      </div>
    )
  }
};
```

<br>

### PropTypes to Define the Props You Expect, Typechecking With PropTypes
React provides useful type-checking features to verify that components receive props of the correct type. For example, your application makes an API call to retrieve data that you expect to be in an array, which is then passed to a component as a prop. You can set propTypes on your component to require the data to be of type array. This will throw a useful warning when the data is of any other type<br><br>
 Check below link <br>
 [Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)

 ```javascript
 import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
 
 ```

<br>

### Access Props Using this.props
To access props within a class component use **this.props**

 ```javascript
 class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Welcome name='Shailendra' />
      </div>
    );
  }
};
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>

         { /* Accessing name property using this.props */ }
        <p>Hello, <strong>{this.props.name}</strong>!</p>

      </div>
    );
  }
};
 
 ```

<br>

### Stateful Component
 ```javascript
 class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);

    //--------
    this.state = {
      name:'Shailendra'
    }
    //--------

  }
  render() {
    return (
      <div>

        <h1>{this.state.name}</h1>

      </div>
    );
  }
};
 
 ```

<br>

### Set State with this.setState and Bind 'this' to a Class Method
React provides a method for updating component state called setState. You call the setState method within your component class like so: this.setState(), passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data.<br>
 React expects you to never modify state directly, instead always use this.setState() when state changes occur
 ```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };

    /*  
    Note: 
    A class method typically needs to use the this keyword so it can access
    properties on the class (such as state and props) inside the scope 
    of the method. bind this to handleClick in the constructor so this becomes 
    bound to the handleClick methods when the component is initialized 
    */
    this.handleClick = this.handleClick.bind(this);

  }
  handleClick() {

     /* when click trigger below code update state */
    this.setState({
      name:'React Rocks!'
    })
    
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
 
 ```


<br>

### Using State Correctly
Do Not Modify State Directly
For example, this will not re-render a component:
```javascript
// Wrong
this.state.comment = 'Hello';
// The only place where you can assign this.state is the constructor.

// Instead, use setState():
// Correct
this.setState({comment: 'Hello'});

```
React may batch multiple setState() calls into a single update for performance.<br>
Sometimes you might need to know the previous state when updating the state. However, state updates may be asynchronous - this means React may batch multiple setState() calls into a single update. This means you can't rely on the previous value of this.state or this.props when calculating the next value
```javascript
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));

// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```
Replace, update state independently with separate setState() 
```javascript
// Completely replaces this.state.posts.
// and will not effect other state property
fetchPosts().then(response => {
  this.setState({
    posts: response.posts
  });
});

// Completely replaces this.state.comments.
// and will not effect other state property
fetchComments().then(response => {
  this.setState({
    comments: response.comments
  });
});
```











