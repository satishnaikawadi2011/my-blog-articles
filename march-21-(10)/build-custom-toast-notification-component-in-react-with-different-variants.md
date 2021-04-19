![custom-toast.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1615579665/custom_toast_5229291ab7.jpg)

In this post , we will create a Custom Toast/Snackbar  Notification Component in  React JS which will have different styling ❤️ depending upon variant. This is the third part of my **Custom UI Components With React series** 🥳. You can see the demo of what we are going to build in this tutorial [here](https://codesandbox.io/s/confident-https-xl9k3?file=/src/App.js). 

Here , in this tutorial , we are going take a different approach than other tutorials. In other tutorial we have created a React Functional components. But here we have to trigger the method to show toast notification which is part of this component from outside it . So instead of creating a component directly , we will create `useToast()` custom hook which will return two things
1. `openToast` -  a method to trigger opening of toast notification.
2. `ToastComponent` - the actual Toast Notification component.

Now going forward we will proceed as below:
1. Creating a fresh react app.
2. Making and designing our `useToast` custom hook.
3. A button to trigger an event to show Toast Notification.

# Creating a Fresh React App
Firstly , we will create a fresh react project with the help of `create-react-app` cli tool by using following command.
```
npx create-react-app modal
```

Let’s start the created app using `npm start` and open up your browser and go to `http://localhost:3000`. You’ll see react’s default app.
Now let's move on to the next step which is to designing and making of actual Modal component.

# Making and designing our useToast custom hook
Now , inside `src` folder of our app , we will create components folder. Inside this component folder , we will create a `toast.js` file for having our `useToast` hook and `toast.module.css` file having `css` styling for our Toast Notification component. 

Getting back to designing part, below is the code snippet for it.
```css
/* toast.module.css */

.snackbar {
  visibility: hidden;
  min-width: 250px;
  margin-left: -125px;
  color: #111;
  text-align: center;
  border-radius: 2px;
  padding: 16px;
  position: fixed;
  z-index: 1;
  left: 50%;
  bottom: 30px;
}

.content {
  display: flex;
  font-size: 1.2rem;
  font-weight: bold;
}

.icon {
  height: 25px;
  width: 25px;
  margin-right: 10px;
}

/* Show the snackbar when clicking on a button (class added with JavaScript) */
.snackbar.show {
  visibility: visible;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

@keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}

@keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 0;
    opacity: 0;
  }
}


```
- `.snackbar` is the class which will have the styling for Toast component whic will be hidden initially.
-  `.content` and `.icon` are the classes which will have the styling for message text of Toast Notification and icon present in  it respectively.
-  `.snackbar.show`  class makes the Toast Notification visible with fade in effect which after 3s disappears with fade out effect.

Now let’s create `useToast` hook.
Below is the code snippet for it.

```jsx

//toast.js

import React, { useRef } from "react";
import ErrorIcon from "./icons/error";
import InfoIcon from "./icons/info";
import SuccessIcon from "./icons/success";
import WarningIcon from "./icons/warning";
import styles from "./toast.module.css";

const useToast = (message, variant = "success", style = {}) => {
  const toastRef = useRef(null);
  const openToast = () => {
    toastRef.current.classList.add(styles.show);
    setTimeout(function () {
      toastRef.current.classList.remove(styles.show);
    }, 3000);
  };
  let toastStyle, icon;
  switch (variant) {
    case "success":
      toastStyle = {
        backgroundColor: "#adebad",
        borderTop: "5px solid #2db92d"
      };
      icon = <SuccessIcon className={styles.icon} fill="#2db92d" />;
      break;
    case "error":
      toastStyle = {
        backgroundColor: "#ffcccc",
        borderTop: "5px solid #ff0000"
      };
      icon = <ErrorIcon className={styles.icon} fill="#ff0000" />;
      break;
    case "info":
      toastStyle = {
        backgroundColor: "#ccf2ff",
        borderTop: "5px solid #33ccff"
      };
      icon = <InfoIcon className={styles.icon} fill="#33ccff" />;
      break;
    case "warning":
      toastStyle = {
        backgroundColor: "#fff0b3",
        borderTop: "5px solid #ffcc00"
      };
      icon = <WarningIcon className={styles.icon} fill="#ffcc00" />;
      break;
    default:
      break;
  }
  const ToastComponent = () => (
    <React.Fragment>
      <div
        ref={toastRef}
        className={styles.snackbar}
        style={{ ...toastStyle, ...style }}
      >
        <div className={styles.content}>
          {icon}
          {message}
        </div>
      </div>
    </React.Fragment>
  );
  return { openToast, ToastComponent };
};

export default useToast;


```
This custom hook will take three parameters:
1.message - Which is a required parameter , which indicates message to show inside this toast notification.\
2. variant - Which will have value one of `'success | warning | error | info`.Depending upon this the styling of notification will be different.This is optional parameter with default value of `success`.\
3. style -  It will have any custom styles that user want to apply to Notification.This is optional parameter with default value of empty object.\

Here , inside this hook we have used four more component InfoIcon,SuccessIcon,WarningIcon and Errorcon , all of which are just simply  `svg` icons.

This component has two main functional parts
1. Correct Styling - Firstly , we will use javascript `swicth` statement to check what is the variant of the toast notification and according to that we will decide the which styling to apply and which icon to render inside this toast notification.\
2. `openToast()` - After that we will implement the method inside this hook to open a toast notification. Inside this method , we will add the `.show` class to toast with the help of `useRef()` to make it visible and after 3 seconds we will remove that class from toast with help of `setTimeout()` so that notification will disappear after 3 seconds.\ 

Now , we will create a ToastComponent inside this hook as shown in above code snippet. After that lastly , we will return the `ToastComponent` and `openToast` from this hook.\
Now , we will see how we can trigger this toast notification with the help of button.

# A button to trigger an event to show Modal

To make it simple, I added the Button in App.js file as below,
```jsx

//App.js

import React from "react";
import useToast from "./components/toast";
import "./styles.css";

export default function App() {
  const { openToast, ToastComponent } = useToast(
    "This is my notification.",
    "success"
  );
  return (
    <div
      style={{
        display: "flex",
        justifyContent: "center",
        alignItems: "center",
        height: "100vh"
      }}
    >
      <button onClick={() => openToast()}>Show Snackbar </button>
      <ToastComponent />
    </div>
  );
}


```

That’s it you did it. It’s as simple as that. Now you can use this component anywhere in your project.We have made a simple , customizable ,beautiful and most important reusable Toast Notification Component.
This is link to [CodeSandbox](https://codesandbox.io/s/confident-https-xl9k3?file=/src/App.js:0-499)  of Toast component.
Let me know if this tutorial was helpful for you guys and for which case you used it.If you have any queries you can contact me through my email or other social media platforms.