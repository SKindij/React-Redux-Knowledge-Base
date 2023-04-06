# Almost everything in React consists of components!

&emsp;**A React component** is a piece of code that represents a reusable part of a user interface. **Components** are the building blocks of React applications. 
They are reusable, modular, and encapsulate the functionality and behavior of a specific part of the user interface.

&emsp;Most React apps have many small components, and everything loads into the main **App component**.

## JSX syntax

+ it is not separate language, but rather syntax extension that gets transformed into regular JavaScript by compiler (such as Babel) before being executed in browser;
+ it allows you to write HTML-like code directly in your JavaScript code, which can make it easier to understand and reason about your React components;
+ **tags** can be either HTML tags or custom React component tags;
+ tags can also have **attributes** just like HTML tags, and these attributes can be set to either static or dynamic values;
+ **expressions** can be nested just like HTML elements can be nested;
+ **expressions** should be wrapped in curly braces `{}`. This allows you to inject dynamic values into your JSX code;

#### Some examples of code:

> 1. Creating simple button component using JSX
> + we're defining custom component `Button`;
> + component accepts two props: `label` and `onClick`; 
> + inside component, we're using **JSX** to create **button element**:
>    - with `onClick` attribute set to the onClick prop
>    - with `label` of the button set to the label prop
> > ```javascript
> >  import React from 'react';
> >    function Button(props) {
> >      const { label, onClick } = props;
> >      return (
> >        <button onClick={ onClick }>{ label }</button>
> >      );
> >    }
> >  export default Button;
> > ```

> 2. Using conditional rendering with JSX
> + we're defining custom component `Message`;
> + component accepts two props: message and isLoggedIn;
> + inside component, we're using **JSX** to conditionally render:
>    - either message prop inside a `<p>` element 
>    - or a "Please log in" message inside a different `<p>` element\
> _based on the value of the `isLoggedIn` prop_
> > ```javascript
> >  import React from 'react';
> >  function Message(props) {
> >    const { message, isLoggedIn } = props;
> >    return (
> >      <div>
> >        { isLoggedIn ? <p>{message}</p> : <p>Please log in.</p> }
> >      </div>
> >    );
> >  }
> >  export default Message;
> > ```

> 3. Using JSX with arrays
> + we're defining custom component `List`;
> + component accepts single prop `items` (array of strings);
> + inside component, we're using `map` function to generate list of `<li>` elements\
> _each containing one item from the array_
> > ```javascript
> >  import React from 'react';
> >  function List(props) {
> >    const { items } = props;
> >    return (
> >      <ul>>{ items.map((item, index) => <li key={index}>{item}</li>) }</ul>
> >    );
> >  }
> >  export default List;
> > ```







