# React 

## ADVANCED GUIDES

## Props Default to “True”

If you pass no value for a prop, it defaults to `true`. These two JSX expressions are equivalent:

```jsx
    <MyTextBox autocomplete />

    <MyTextBox autocomplete={true} />
```

In general, we don’t recommend using this because it can be confused with the ES6 object shorthand `{foo}` which is short for `{foo: foo}` rather than `{foo: true}`. This behavior is just there so that it matches the behavior of HTML.

## Spread Attributes

If you already have `props` as an object, and you want to pass it in JSX, you can use `...` as a “spread” operator to pass the whole props object. These two components are equivalent:

```jsx
    function App1() {
      return <Greeting firstName="Ben" lastName="Hector" />;
    }

    function App2() {
      const props = {firstName: 'Ben', lastName: 'Hector'};
      return <Greeting {...props} />;
    }
```

You can also pick specific props that your component will consume while passing all other props using the spread operator.

```jsx
    const Button = props => {
      const { kind, ...other } = props;
      const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
      return <button className={className} {...other} />;
    };

    const App = () => {
      return (
        <div>
          <Button kind="primary" onClick={() => console.log("clicked!")}>
            Hello World!
          </Button>
        </div>
      );
    };
```

In the example above, the `kind` prop is safely consumed and is not passed on to the `<button>` element in the DOM. All other props are passed via the `...other` object making this component really flexible. You can see that it passes an `onClick` and `children` props.

Spread attributes can be useful but they also make it easy to pass unnecessary props to components that don’t care about them or to pass invalid HTML attributes to the DOM. We recommend using this syntax sparingly.