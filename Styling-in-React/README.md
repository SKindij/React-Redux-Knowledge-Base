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





