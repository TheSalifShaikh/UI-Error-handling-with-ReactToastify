# React-Toastify Documentation with API Call

**React-Toastify** is a powerful and easy-to-use library that allows us to display notifications (called toasts) in our React applications. It’s especially helpful for informing users of actions such as API request successes or errors.

## Why Use Toast Notifications in API Calls?

When we interact with a server (such as fetching or submitting data), users want to know the outcome. For example, they need to know if:
1. The data was fetched or saved successfully (a **success toast**).
2. There was a problem (like a network issue or server error) and the request failed (an **error toast**).

React-Toastify gives us an easy way to provide this feedback, making the user experience smoother by immediately informing users of what happened.

---
## 1. Installation

First, we need to install the required libraries:

```
npm install react-toastify
```
or
```
yarn add react-toastify
```
---
## 2. Setting Up ToastContainer

The `ToastContainer` is what actually renders the toast notifications on the screen. It can be added to any part of your React app but is often placed in a higher-level component like `App.jsx` or `main.jsx`. Let’s create a separate component for the `ToastContainer` to keep things organized. Or you can directly use it in higher-level component.

### **Direct Call in App.jsx**
```
import { ToastContainer} from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

const App = () => {
  return(
    <>
      <ToastContainer
        position="top-right"
        autoClose={5000}
        hideProgressBar={false}
        newestOnTop={false}
        closeOnClick
        rtl={false}
        pauseOnFocusLoss
        draggable
        pauseOnHover
        theme="light"
        transition: Bounce,
      />
      {/* your rest of the compoent}
    </>
);
};
```
Or 
### **ToastContainerComponent.jsx**

```jsx
import React from 'react';
import { ToastContainer } from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

function ToastContainerComponent() {
  return (
    <ToastContainer
      position="top-right"
      autoClose={5000}
      hideProgressBar={false}
      newestOnTop={false}
      closeOnClick
      rtl={false}
      pauseOnFocusLoss
      draggable
      pauseOnHover
    />
  );
}

export default ToastContainerComponent;
```

Explanation:
    ToastContainer handles where the toasts appear on the screen.
    The options allow us to control behavior like autoClose (how long the toast stays), the position, and whether the toast is draggable.
    The  <ToastConatiner /> works too. But it will get the default properties.

---

## 3. Using `toast` in an Axios API Call

Now, let’s look at two ways of showing toast notifications when an API call is made using Axios.

### A. Using a Function to Show toast

Here, we’ll use a function to make the API call and show a success or error toast based on the result.

#### **App.jsx**

```
import React from 'react';
import axios from 'axios';
import { toast } from 'react-toastify';
import ToastContainerComponent from './ToastContainerComponent';

function App() {
  const fetchData = async () => {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/posts/1');
      
      // Show success toast if the API call is successful
      toast.success('Data fetched successfully!');
      console.log(response.data);
    } catch (error) {
      // Show error toast if the API call fails
      toast.error('Error fetching data. Please try again later.');
    }
  };

  return (
    <div>
      <button onClick={fetchData}>Fetch Data</button>
      <ToastContainerComponent />
    </div>
  );
}

export default App;
```

### Explanation
- **In the `fetchData` function**:
  - We use `axios.get()` to make an API request.
  - If the request is successful (inside the `try` block), we call `toast.success()` to show a success message.
  - If there’s an error (inside the `catch` block), we call `toast.error()` to show an error message.
