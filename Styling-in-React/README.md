## Styling in React can be accomplished in a number of ways. 

### Inline Styling: 
you can define styles inline using the style attribute, which accepts an object containing key-value pairs of CSS properties and values
> ```javascript
> const styles = {
>   color: 'red',
>   fontSize: '20px'
> };
>
> function MyComponent() {
>   return (
>     <div style={styles}>Hello, world!</div>
>   );
> }
> ```

### CSS Modules:
allow you to import CSS files directly into your component and use them as local scoped styles
> ```javascript
> import styles from './MyComponent.module.css';
> 
> function MyComponent() {
>   return (
>     <div className={styles.container}>Hello, world!</div>
>   );
> }
> ```

### Styled Components: 
it is a library that allows you to write CSS in your JavaScript code using a special syntax.\
This creates components that are styled using CSS-in-JS.
> ```javascript
> import styled from 'styled-components';
> 
> const Button = styled.button`
>   background-color: ${props => props.primary ? 'blue' : 'white'};
>   color: ${props => props.primary ? 'white' : 'black'};
>   font-size: 1em;
>   margin: 1em; padding: 0.25em 1em;
>   border: 2px solid blue; border-radius: 3px;
> `;
> 
> function MyComponent() {
>   return (
>     <Button primary>Hello, world!</Button>
>   );
> }
> 
> ```

