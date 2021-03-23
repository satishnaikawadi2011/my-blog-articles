![1.Buttons.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1615438576/1_Buttons_6f58501ecb.jpg)

This is the first part of many 🛎️ from the series Custom UI Components With React. In this post we will see how we can create custom Button component with different props and styles in React JS.

Below is the demo of what we are going to build in this tutorial.

![btn-demo.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1615440700/btn_demo_50096e523e.jpg)

##  ✔️ Button Component Props
We are going to have several props for this component so that we can have control on it from outside to how we can customize or modify it.The props will be as follows  - 

- btnColor - This props will decide the color of the button. 
- labelColor - This props will decide the color of text inside the button. By default it will be `white`, but depending on your `btnColor` you can change it to have right contrast.
- onClick - This  will be a `onClick` handler present on button. 
- type - This prop will decide the styling of the button. It will have the value either one of `outline | block | rounded`. If this prop is not passed button will have default styling.
- style - This prop will have any custom styling you want to give Button component from outside.
- disabled - This prop will decide if the button is in active state or not.


## 🃏Basic Styling Of Button
We will give button some basic styling. Here we will create `button.module.css` file and then we will add `btn` class to it for giving some basic styles to our button as follows.

```css

/* button.module.css */

.btn {
	font-family: 'Ubuntu', sans-serif;
	position: relative;
	font-weight: 400;
	font-size: 1.3rem;
	line-height: 2;
	height: 50px;
	transition: all 200ms linear;
	border-radius: 4px;
	width: 240px;
	letter-spacing: 1px;
	display: inline-flex;
	align-items: center;
	justify-content: center;
	text-align: center;
	align-self: center;
	border: none;
	cursor: pointer;
	box-shadow: 0 12px 35px 0 rgba(16, 39, 112, .25);
	outline: 0;
	text-transform: capitalize;
}
```

## 💠 Creating Button Functional Component

Now we will create a `Button.js` files in which we will create out custom Button Component. In this file we will import `styles` from our `button.module.css` file . Here we will return a basic HTML `button` element and we will add `btn` class to it from `styles`.We will destructure the all props.

```jsx
//Button.js

import React from 'react';
import styles from './button.module.css';

const Button = ({ children, onClick, btnColor = 'teal', labelColor, disabled, type, style, ...props }) => {
	return (
		<button
			className={styles.btn}
		>
			{children || 'label'}
		</button>
	);
};

export default Button;

```
Now in this  `Button.js` file we will create some styles objects for different types of buttons.
```js

//Button.js

	const commonStyles = {
		backgroundColor : btnColor,
		color           : labelColor || 'white'
	};
	const outlineStyles = {
		border          : `1px solid ${btnColor}`,
		color           : btnColor,
		backgroundColor : 'white'
	};
	const outlineHoverStyle = {
		color           : labelColor || 'white',
		backgroundColor : btnColor
	};

	const roundedStyle = {
		backgroundColor : btnColor,
		color           : labelColor || 'white',
		borderRadius    : '25px'
	};
	const disabledStyle = {
		cursor          : 'default',
		backgroundColor : btnColor,
		color           : labelColor || 'white',
		opacity         : 0.4
	};
	const blockStyles = {
		width  : '95%',
		margin : '0 auto'
	};
```
Here we have common styles depending on `btnColor` which will be added to every type of  button . On the other hand all the other styles will be added conditionally depending on the `type` of button. Here note that for `outline` type we have two cases - first is default outlineStyles which will be added when type of button is outline and the other case is when we hover over the button.

So to track the hover state we will create `state` hover with `useState()` [react hook](https://reactjs.org/docs/hooks-intro.html) with which we will add hover style conditionally. With Javascript Event Handlers `onMouseEnter` and `onMouseLeave` we will toggle our `hover` state.

Now we will add a simple `switch` statement in javascript to conditionally render the styles depending on the type of button.
```javascript

//Button.js
	let btnStyle;
	switch (type) {
		case 'rounded':
			btnStyle = roundedStyle;
			break;
		case 'block':
			btnStyle = blockStyles;
			break;
		case 'outline':
			if (hover) {
				btnStyle = outlineHoverStyle;
			}
			else {
				btnStyle = outlineStyles;
			}
			break;
		default:
			btnStyle = {
				backgroundColor : btnColor,
				color           : labelColor || 'white'
			};
			break;
	}


```

And that's it , Now we will just add this `btnStyle` along with any `style` passed from props onto button and we will also add disabled style if button has `disabled` prop. So our final code will look like follows - 

```jsx

//Button.js

import React, { useState } from 'react';
import styles from './button.module.css';

const Button = ({ children, onClick, btnColor = 'teal', labelColor, disabled, type, style, ...props }) => {
	const [
		hover,
		setHover
	] = useState(false);
	const toggleHover = () => {
		setHover(!hover);
	};
	const commonStyles = {
		backgroundColor : btnColor,
		color           : labelColor || 'white'
	};
	const outlineStyles = {
		border          : `1px solid ${btnColor}`,
		color           : btnColor,
		backgroundColor : 'white'
	};
	const outlineHoverStyle = {
		color           : labelColor || 'white',
		backgroundColor : btnColor
	};

	const roundedStyle = {
		backgroundColor : btnColor,
		color           : labelColor || 'white',
		borderRadius    : '25px'
	};
	const disabledStyle = {
		cursor          : 'default',
		backgroundColor : btnColor,
		color           : labelColor || 'white',
		opacity         : 0.4
	};
	const blockStyles = {
		width  : '95%',
		margin : '0 auto'
	};
	let btnStyle;
	switch (type) {
		case 'rounded':
			btnStyle = roundedStyle;
			break;
		case 'block':
			btnStyle = blockStyles;
			break;
		case 'outline':
			if (hover) {
				btnStyle = outlineHoverStyle;
			}
			else {
				btnStyle = outlineStyles;
			}
			break;
		default:
			btnStyle = {
				backgroundColor : btnColor,
				color           : labelColor || 'white'
			};
			break;
	}
	return (
		<button
			style={

					disabled ? { ...commonStyles, ...btnStyle, ...disabledStyle, ...style } :
					{ ...commonStyles, ...btnStyle, ...style }
			}
			onMouseEnter={toggleHover}
			onMouseLeave={toggleHover}
			{...props}
			type="button"
			onClick={

					!disabled ? onClick :
					() => {}
			}
			className={styles.btn}
		>
			{children || 'button'}
		</button>
	);
};

export default Button;

```
[Here](https://codesandbox.io/s/zealous-chaum-3jmi5?file=/src/components/Button.js) you can see live demo and interact with this component.
Hope you inderstand this tutorial . Thank You for reading 😇.