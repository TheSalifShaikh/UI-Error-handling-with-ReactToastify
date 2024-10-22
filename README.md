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

---

#### **DirectToast.jsx**

```
import React, { useEffect } from 'react';
import axios from 'axios';
import { toast } from 'react-toastify';

function DirectToast() {
  useEffect(() => {
    // Make API call and directly call toast in the promise chain
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then((response) => {
        // Show success toast directly
        toast.success('Data fetched successfully!');
        console.log(response.data);
      })
      .catch((error) => {
        // Show error toast directly
        toast.error('Error fetching data.');
      });
  }, []);

  return (
    <div>
      <h1>Data Fetching on Component Mount</h1>
    </div>
  );
}

export default AppDirectToast;
```

### Explanation
- We use the `useEffect` hook to make an API call when the component is first loaded (mounted).
- In the `.then()` block (after the successful request), we call `toast.success()` directly.
- In the `.catch()` block (when the request fails), we call `toast.error()` directly.
- This approach is simpler but less flexible if you need to reuse the logic.

---

## 4. Why Are We Using `toast` in Axios API Calls?

Let’s explain the reasoning step-by-step, assuming a user is new to development:

### a. Why Use a Toast for Success?
- **Purpose:** When the API request is successful, you want to notify the user that everything went well. This is where we use a **success toast** to give positive feedback.
- **Example:** When a user submits a form and the data is saved successfully, a toast saying, "Data saved!" reassures the user that the action was completed.

### b. Why Use a Toast for Errors?
- **Purpose:** If something goes wrong during the API request (like a server issue or bad internet connection), it’s important to alert the user. This is done with an **error toast**.
- **Example:** If the API call fails to fetch data, an error toast like "Error fetching data" informs the user that something went wrong, and they may need to retry or check their connection.

---

## 5. Key Options in Toast Customization

When showing toasts in React-Toastify, you can customize their appearance and behavior to suit your needs:

- **`position`**: Controls where the toast appears on the screen (e.g., `top-right`, `bottom-left`).
- **`autoClose`**: Determines how long the toast stays visible (in milliseconds).
- **`hideProgressBar`**: Hides or shows the progress bar.
- **`pauseOnHover`**: Pauses the auto-close timer when the user hovers over the toast.

You can pass these options either inside the `ToastContainer` for global control or directly when calling the `toast` function.
