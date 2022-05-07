## react-recipes

A collection of most useful hooks (includes many of hooks below)

https://www.npmjs.com/package/react-recipes

Note: not working on React v18 for now

## React Hook Form

```js
import React from "react";
import useForm from "react-hook-form";

const fontstyle = {
  fontSize: "15px"
};
export default function Order() {
  const { signup, handleSubmit, errors } = useForm();
  const onSubmit = data => {  // upload the data retreived from the form to a database, return value to a user, etc
    console.log(data);
  };

  return (
    <div>
      <form onSubmit={handleSubmit(onSubmit)}>
        <label>Full Name</label>
        <input name="fullname" ref={signup} />
        <label>Product Name</label>
        <input
          name="productName"
          ref={signup({ required: true, maxLength: 20 })}
        />

        <select style={fontstyle} name="Title" ref={signup({ required: true })}>
          <option value="">Select...</option>
          <option value="One bundle">One bundle</option>
          <option value="Two bundle">Two bundle</option>
        </select>
        <label>
          <input type="checkbox" placeholder="Age 18+" name="Age 18+" ref={signup} /> 
          Age Above 18 Years Only
        </label>
        {errors.productType && <p>Required Field</p>}
        <input type="submit" value="Make the Payment" />
      </form>
    </div>
  );
}
```

## HookRouter

alternative to react-router

```js
// index.js or where you choose to render your entire app from
import { useRoutes } from "hookrouter";
import Routes from "./router";

function App() {
  const routes = useRoutes(Routes);
  return <div>{routes}</div>;
}
```

## Use-http

```js
import useFetch from "use-http"

const OrderExample = () => {
  const [orders, setOrders] = useState([])
  const { get, post, response, loading, error } = useFetch("https://ordering.com")
  
  useEffect(() => { get("/orders") }, [])

  const addOrder = async () => {
      await post("/orders", { title: "example order" });
      if (response.ok) setOrders([...orders, newOrder])
  }

  return (
    <>
      <button onClick={addOrder}>Add Order</button>
      {error && 'Error!'}
      {loading && 'Loading...'}
      {orders.map(order => (
        <span key={order.id}>{order.title}</span>
      )}
    </>
  );
};
```

## Use Local Storage

```js
import React from "react";
import { useLocalStorage } from '@rehooks/local-storage';

export default function App() {
  const [value, setValue, remove] = useLocalStorage("key", "product");

  return (
    <div>
      <div>Value: {value}</div>
      <button onClick={() => setValue("Shampoo")}>Shampoo</button>
      <button onClick={() => setValue("Conditioner")}>Conditioner</button>
      <button onClick={() => remove()}>Remove</button>
    </div>
  );
}
```

## React-Use-Hover

```js
import useHover from "react-use-hover";

const Example = () => {
  const [isHovering, hoverProps] = useHover();
  return (
    <>
      <span {...hoverProps} aria-describedby="overlay">Hover pls</span>
      {isHovering ? <div> Hey.. I am hovered! </div> : null}
    </>
  );
}
```

## Use Media

```js
import useMedia from 'use-media';

const Example = () => {
  const isWidth = useMedia({minWidth: '500px'});

  return (
    <span>
      Page width is: {isWidth ? "WideScreen" : "NarrowScreen"}
    </span>
  );
};
```

## UseDebounce

You can use this hook to debounce any rapidly changing value. It is frequently used in inputs and forms that fetch data, and it is used to delay function execution.

```js
mport React, { useState } from "react";
import { useDebounce } from "use-debounce";

export default function Input() {
  const [text, setText] = useState("Hi");
  const [value] = useDebounce(text, 1000);

  return (
    <div>
      <input
        defaultValue={"Hey There!"}
        onChange={(e) => {
          setText(e.target.value);
        }}
      />
      <p>Value: {text}</p>
      <p>Debounced text: {value}</p>
    </div>
  );
```

