Project: Food Delivery App

We'll create 3 Contexts:

FoodContext → Food Items
CartContext → Add/Remove Cart Items
ThemeContext → Dark/Light Modetext → Food Items
CartContext → Add/Remove Cart Items
ThemeContext → Dark/Light Mode

```
src
│
├── context
│   ├── FoodContext.jsx
│   ├── CartContext.jsx
│   └── ThemeContext.jsx
│
├── components
│   ├── FoodList.jsx
│   ├── Cart.jsx
│   └── ThemeButton.jsx
│
├── App.jsx
└── main.jsx

```

1. FoodContext
   
FoodContext.jsx

```Javascript
import { createContext } from "react";

export const FoodContext = createContext();

const foodItems = [
  { id: 1, name: "Pizza", price: 200 },
  { id: 2, name: "Burger", price: 100 },
  { id: 3, name: "Pasta", price: 150 }
];

const FoodContextProvider = ({ children }) => {
  return (
    <FoodContext.Provider value={{ foodItems }}>
      {children}
    </FoodContext.Provider>
  );
};

export default FoodContextProvider;
```

2. CartContext
   
CartContext.jsx

```javascript

import { createContext, useState } from "react";

export const CartContext = createContext();

const CartContextProvider = ({ children }) => {

  const [cartItems, setCartItems] = useState([]);

  const addToCart = (item) => {
    setCartItems([...cartItems, item]);
  };

  const removeFromCart = (id) => {
    setCartItems(
      cartItems.filter((item) => item.id !== id)
    );
  };

  return (
    <CartContext.Provider
      value={{
        cartItems,
        addToCart,
        removeFromCart,
      }}
    >
      {children}
    </CartContext.Provider>
  );
};

export default CartContextProvider;
```

3. ThemeContext

   ThemeContext.jsx

```javascript
import { createContext, useState } from "react";

export const ThemeContext = createContext();

const ThemeContextProvider = ({ children }) => {

  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme(theme === "light" ? "dark" : "light");
  };

  return (
    <ThemeContext.Provider
      value={{
        theme,
        toggleTheme,
      }}
    >
      {children}
    </ThemeContext.Provider>
  );
};

export default ThemeContextProvider;
```

4. Wrap All Contexts

main.jsx

```javascript

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

import FoodContextProvider from "./context/FoodContext";
import CartContextProvider from "./context/CartContext";
import ThemeContextProvider from "./context/ThemeContext";

ReactDOM.createRoot(document.getElementById("root")).render(

  <ThemeContextProvider>
    <FoodContextProvider>
      <CartContextProvider>
        <App />
      </CartContextProvider>
    </FoodContextProvider>
  </ThemeContextProvider>

);
```

5. FoodList Component

Gets data from FoodContext and adds items to CartContext

FoodList.jsx

```javascript

import { useContext } from "react";
import { FoodContext } from "../context/FoodContext";
import { CartContext } from "../context/CartContext";

const FoodList = () => {

  const { foodItems } = useContext(FoodContext);
  const { addToCart } = useContext(CartContext);

  return (
    <>
      <h2>Food Menu</h2>

      {foodItems.map((item) => (
        <div key={item.id}>
          <h3>{item.name}</h3>
          <p>₹{item.price}</p>

          <button
            onClick={() => addToCart(item)}
          >
            Add To Cart
          </button>
        </div>
      ))}
    </>
  );
};

export default FoodList;
```

6. Cart Component

Cart.jsx

```javascript
import { useContext } from "react";
import { CartContext } from "../context/CartContext";

const Cart = () => {

  const {
    cartItems,
    removeFromCart,
  } = useContext(CartContext);

  return (
    <>
      <h2>Cart</h2>

      {cartItems.map((item) => (
        <div key={item.id}>
          {item.name}

          <button
            onClick={() =>
              removeFromCart(item.id)
            }
          >
            Remove
          </button>
        </div>
      ))}
    </>
  );
};

export default Cart;
```

7. Theme Button

ThemeButton.jsx

```javascript
import { useContext } from "react";
import { ThemeContext } from "../context/ThemeContext";

const ThemeButton = () => {

  const {
    theme,
    toggleTheme,
  } = useContext(ThemeContext);

  return (
    <>
      <h2>Current Theme : {theme}</h2>

      <button onClick={toggleTheme}>
        Change Theme
      </button>
    </>
  );
};

export default ThemeButton;
```

8. App.jsx

```javascript
import FoodList from "./components/FoodList";
import Cart from "./components/Cart";
import ThemeButton from "./components/ThemeButton";

const App = () => {
  return (
    <>
      <ThemeButton />
      <FoodList />
      <Cart />
    </>
  );
};

export default App;

```


Real Industry Usage

Context API is commonly used for:

✅ Authentication (User Login)
 ✅ Shopping Cart
 ✅ Theme (Dark/Light)
 ✅ Language Translation
 ✅ User Profile
 ✅ Product Data


```
createContext()
      ↓
Provider
      ↓
value={}
      ↓
useContext()
      ↓
Access Data Anywhere
```
