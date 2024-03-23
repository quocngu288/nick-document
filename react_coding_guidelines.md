# Coding Guidelines - ReactJS

## Table of Contents

1. [Folder Structure](#folder-structure)
2. [Basic Rules](#basic-rules)
3. [Naming](#naming)
4. [Declaration](#declaration)
5. [Alignment](#alignment)
6. [Quotes](#quotes)
7. [Spacing](#spacing)
8. [Props](#props)
9. [Parentheses](#parentheses)
10. [Tags](#tags)
11. [Refs](#refs)
12. [Methods](#methods)
13. [Ordering](#ordering)

## Cấu trúc thư mục (Folder Structure)

    src/
    ├── assests/
    │   ├── css                             # Storing css files
    │   ├── images                          # Storing image files
    │   ├── fonts                           # Storing fon files
    │   ├── scss                            # Storing scss files
    │   └── ...
    ├── data/                               # Static Data or Dummy data
    │   ├── products.js
    │   ├── about-us.js
    │   └── ...
    ├── features/                           #
    │   ├── flashsale/                      #
    │   │   ├── components/
    │   │   ├── constants/
    │   │   ├── enums/
    │   │   ├── context/
    │   │   ├── hooks/
    │   │   ├── hocs/
    │   │   └── ...
    │   ├── li-xi/                          #
    │   │   ├── components/
    │   │   └── ...
    │   └── ...
    ├── pages/                              #
    │   ├── _app.js                         #
    │   ├── 404.js                          #
    │   ├── error.js                        #
    │   ├── global-error.js                 #
    │   └── ...
    ├── shared/                             # Shared elements used across the site
    │   ├── components/                     # Reusable components
    │   │   ├── layout                      #
    │   │   │   ├── Header.js               #
    │   │   │   ├── Footer.js               #
    │   │   │   ├── Sidebar.js              #
    │   │   │   ├── NoAuthLayout.js         #
    │   │   │   ├── AuthLayout.js           #
    │   │   │   └── ...
    │   │   ├── form                        # Storing form controls
    │   │   │   ├── Input.js
    │   │   │   ├── Textarea.js
    │   │   │   ├── Select.js
    │   │   │   └── ...
    │   │   ├── modals                      #
    │   │   │   ├── CheckoutModal.js
    │   │   │   ├── NotificationModal.js
    │   │   │   └── ...
    │   │   └── ...
    │   ├── constants/                      #
    │   │   ├──                             #
    │   │   └── ...
    │   ├── enums/                          #
    │   │   ├── order-status.enum.js
    │   │   └── ...
    │   ├── context/                        # Storing context files
    │   │   ├── AuthContext.js
    │   │   └── ...
    │   ├── hooks/                          # Custom hooks
    │   │   ├── useFormValidation.js
    │   │   ├── useOnClickOutSide.js
    │   │   ├── useCountries.js
    │   │   └── ...
    │   ├── hocs/                           # Higher-order components
    │   │   ├──                   #
    │   │   └── ...
    │   ├── libs/                           # Config Third-party library
    │   │   ├── ant-design.js
    │   │   ├── prismadb.js
    │   │   └── ...
    │   ├── services or api/                # Shared services or API calls
    │   │   ├── base.service.js
    │   │   ├── auth.service.js
    │   │   ├── order-tracking.service.js
    │   │   └── ...                         # Other services
    │   ├── utils/                          # Utility functions
    │   │   ├── index.js
    │   │   └── ...                         ## Other utils
    │   └── ...
    ├── styles/                             # Global styles
    │   └── ...
    └── ...                                 # Other necessary files and folders

## Những quy tắc cơ bản (Basic Rules)

### Quy tắc đặt tên

Có 4 quy tắc đặt tên thường dùng là PascalCase, camelCase, kebab-case và SCREAMING_SNAKE_CASE

1. PascalCase
   - Viết hoa tất cả các chữ cái đầu. Ví dụ: ProductList, OrderStatusEnum
   - Chúng ta thường dùng PascalCase cho React Component, Enumerations, Reference Naming
2. camelCase

   - Từ đầu tiên viết thường, các từ tiếp theo viết hoa chữ cái đầu. Ví dụ: lastName, getProducts, useCustomHook, withHOC
   - Chúng ta thường dùng camelCase cho Variable Names, Function Names, Object Properties, Custom Hooks, Higher Order Component, utility functions or helper functions

3. kebab-case

   - Sử dụng dấu gạch - giữa các từ, tất cả các từ đều viết thường. Ví dụ: header-container, product-list
   - Chúng ta thường dùng kebab-case cho CSS Class Names, Folder Names

4. SCREAMING_SNAKE_CASE
   - Sử dụng dấu gạch \_ giữa các từ, tất cả các từ đều viết hoa. Ví dụ: BASE_PATH
   - Chúng ta thường dùng SCREAMING_SNAKE_CASE cho Constants, Enumeration Properties, Global Variables

## Naming Convention

### Folder Names

- Sử dụng quy tắc kebab-case đặt tên cho folder name

```javascript
// ✅ Good
-product -
  product -
  list -
  product -
  list -
  item -
  // ❌ Avoid
  Product -
  productList -
  ProductList -
  product_list;
// ....
```

### Reference Naming

- Sử dụng quy tắc PascalCase cho React components và camelCase cho instance

```javascript
// ❌ Avoid
import reservationCard from "./ReservationCard";

// ✅ Good
import ReservationCard from "./ReservationCard";

// ❌ Avoid
const ReservationItem = <ReservationCard />;

// ✅ Good
const reservationItem = <ReservationCard />;
```

### Components

- Sử dụng quy tắc PascalCase đặt tên cho filename cũng như component name

```javascript
// ✅ Good
// Filename: Products.js
// Filename: ProductList.js
// Filename: ProductItem.js

class Products extends React.Component {}

export default Products;

class ProductItem extends React.Component {}

export default ProductItem;


// ❌ Avoid
// Filename: products.js
// Filename: productList.js
// Filename: product-list.js
// Filename: product_list.js
// ....

class products extends React.Component {}

export default products;

class productItem extends React.Component {}

export default productItem;
```

### CSS Class Names

- Sử dụng quy tắc kebab-case đặt tên cho class name

```javascript
// ✅ Good
// Use ** lowercase letters** and **hyphens** for CSS class names
// className="product"
// className="product-container"

// ❌ Avoid
// className="BUTTON"
// className="Product-container"
// className="Product-Container"
// ....
```

### Enumerations

- Sử dụng quy tắc kebab-case đặt tên cho filename và thêm .enum phía sau filename, ví dụ: order-status.enum.js
- Sử dụng quy tắc PascalCase đặt tên cho Enum name và thêm Enum phía sau Enum name.

```javascript
// ✅ Good
// Filename: order-status.enum.js
// Filename: product-status.enum.js

const OrderStatusEnum = {};

const ProductStatusEnum = {};

// ❌ Avoid
// Filename: productstatus.js
// Filename: productStatus.js
// Filename: ProductStatus.js
// Filename: product_status.js
// ....

const orderStatus = {};
const productstatus = {};
const order_status = {};
```

### Enumeration Properties

- Sử dụng quy tắc SCREAMING_SNAKE_CASE đặt tên cho properties của enum

```javascript
// ✅ Good
// Enumeration Properties
const RequestTypeEnum = {
  // Name in Pascal Case
  // Properties in Screaming Snake Case
  GET: "GET",
  POST: "POST",
  PUT: "PUT",
  DELETE: "DELETE",
};
```

### Variable Names

- Sử dụng quy tắc camelCase đặt tên cho variable name

```javascript
// ✅ Good
const userName = "Example";
const userLastName = "Example";
const userFirstName = "Example";

// ❌ Avoid
const UserName = "Example";
const userlastname = "Example";
const user_first_name = "Example";
// ....
```

### Function Names

- Sử dụng quy tắc đặt tên cho

```javascript
// ✅ Good
const getFullName = (firstName, lastName) => {
  return `${firstName} ${lastName}`;
};
```

### Object Properties

- Sử dụng quy tắc đặt tên cho

```javascript
// ✅ Good
const user = {
  userName: "sathishskdev",
  firstName: "Sathish",
  lastName: "Kumar",
};
```

### Custom Hooks

- Sử dụng quy tắc đặt tên cho

```javascript
// ✅ Good
// Custom Hook: useTimer
// name have "use" as Prefix
// "Timer" is add as Suffix which is behaviour of hook
const useTimer = (initialTime) => {
  // ... hook implementation
};

// Usage of the custom hook
const { time, start, stop, reset } = useTimer(60);
```

### Higher Order Component

- Sử dụng quy tắc đặt tên cho

```javascript
// ✅ Good
// HOC: name have "with" as Prefix
// "Filter" is add as Suffix which is original component
const withFilter = () => {
  //...
};

// Usage of the HOC
const Filter = withFilter(/*Component Name*/);
```

### Utility Functions or Helper Functions

- Sử dụng quy tắc đặt tên cho

  ```javascript

  ```

### Constants

- Sử dụng quy tắc SCREAMING_SNAKE_CASE đặt tên cho constants

```javascript
// ✅ Good
const BASE_PATH = "PRODUCTION";
```

### Global Variables

- Sử dụng quy tắc SCREAMING_SNAKE_CASE đặt tên cho global variables

```javascript
// ✅ Good
// Global Variables
const PI = 3.14159;
```

## Declaration

- Do not use displayName for naming components. Instead, name the component by reference.
- ```javascript
  // bad
  export default React.createClass({
    displayName: "ReservationCard",
    // stuff goes here
  });
  ```

// good
export default class ReservationCard extends React.Component {
}

````

## Alignment
- Follow these alignment styles for JSX syntax

```javascript
// bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>

// if props fit in one line then keep it on the same line
<Foo bar="bar" />

// children get indented normally
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
>
    <Spazz />
</Foo>

// bad
{showButton &&
<Button />
}

// bad
{
  showButton &&
  <Button />
}

// good
{showButton && (
  <Button />
)}

// good
{showButton && <Button />}

// good
{someReallyLongConditional
&& anotherLongConditional
&& (
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  />
)
}

// good
{someConditional ? (
  <Foo />
) : (
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  />
)}
````

## Quotes

- Always use double quotes (") for JSX attributes, but single quotes (') for all other JS.

```javascript
// bad
<Foo bar='bar' />

// good
<Foo bar="bar" />

// bad
<Foo style={{ left: "20px" }} />

// good
<Foo style={{ left: '20px' }} />
```

## Spacing

- Always include a single space in your self-closing tag

```javascript
// bad
<Foo/>

// very bad
<Foo                 />

// bad
<Foo
 />

// good
<Foo />
```

- Do not pad JSX curly braces with spaces

```javascript
// bad
<Foo bar={ baz } />

// good
<Foo bar={baz} />
```

## Props

- Always use camelCase for prop names.

```javascript
// bad
<Foo
    UserName="hello"
    phone_number={12345678}
/>

// good
<Foo
    userName="hello"
    phoneNumber={12345678}
/>
```

## Refs

- Always use ref callbacks

```javascript
  // bad
<Foo
  ref="myRef"
/>

// good
<Foo
  ref={(ref) => { this.myRef = ref; }}
/>
```

## Tags

- Always self-close tags that have no children.

```javascript
// bad
<Foo className="stuff"></Foo>

// good
<Foo className="stuff" />
```

- If your component has multi-line properties, close its tag on a new line.

```javascript
// bad
<Foo
    bar="bar"
    baz="baz" />

// good
<Foo
    bar="bar"
    baz="baz"
/>
```

## Hocs

When using Higher-Order Components (HOCs) in React, it’s a common convention to prefix the name of the HOC with the word “with”. This helps make it clear that the component is a HOC and makes the code more readable and maintainable.

```javascript
// Example of an HOC named withAuth
const withAuth = (Component) => {
  // ...
};

// Example of an HOC named withToggle
const withToggle = (Component) => {
  // ...
};
```

## Avoid Abbreviations, use full words

When naming a component it is important to avoid abbreviations and instead use the full words that accurately describe the component's purpose.

```javascript
// Good
const UserInformation = () => {
  // ...
};

// Good
const ShoppingCart = () => {
  // ...
};

// Bad
const User = (Component) => {
  // ...
};
```
