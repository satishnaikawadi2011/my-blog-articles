- ![custom-modal.jpg](https://res.cloudinary.com/dh1srz69c/image/upload/v1615580227/custom_modal_5c6ff2a4f1.jpg)

In this post , we will build custom modal component with react js. We will build this Modal component from scratch without using any css framework. This is the second part of my series **Build Custom UI Components With React**. Below is the demo 😍 of what we will build going towards the end of this tutorial - very beautiful and fully customizable Modal Component.

![modal-demo.gif](https://res.cloudinary.com/dh1srz69c/image/upload/v1615614965/modal_demo_17b918a948.gif)


We will proceed as below:
1. Creating a fresh react app.
2. Making and designing our Modal component.
3. A button to trigger an event to show Modal.

# Creating a Fresh React App
Firstly , we will create a fresh react project with the help of `create-react-app` cli tool by using following command.
```
npx create-react-app modal
```

Let’s start the created app using `npm start` and open up your browser and go to `http://localhost:3000`. You’ll see react’s default app.
Now let's move on to the next step which is to designing and making of actual Modal component.

# Making and designing our Modal component
Now , inside src folder of our app , we will create components folder. Inside this component folder , we will create a modal folder which will have `Modal.js` file for having modal  component and `modal.module.css` file having css styling for our Modal component. 

Getting back to designing part, below is the code snippet for it.
```css
/* modal.module.css */

.modal__wrap {
	position: fixed;
	display: block;
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
	margin: 0 auto;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	z-index: 100;
	overflow-x: hidden;
	background-color: rgba(31, 32, 41, .75);
	pointer-events: none;
	opacity: 0;
	transition: opacity 250ms 700ms ease;
}

.visible {
	pointer-events: auto;
	opacity: 1;
	transition: all 300ms ease-in-out;
}

.modal {
	overflow-y: scroll;
	overflow-x: hidden;
	position: relative;
	display: block;
	width: 60vw;
	height: 60%;
	min-height: 400px;
	min-width: 400px;
	margin: 0 auto;
	margin-top: 20px;
	margin-bottom: 20px;
	border-radius: 4px;
	padding-bottom: 20px;
	background-color: #fff;
	align-self: center;
	box-shadow: 0 12px 25px 0 rgba(199, 175, 189, .25);
	opacity: 0;
	transform: scale(0.6);
	transition: opacity 250ms 250ms ease, transform 300ms 250ms ease;
	transform: scale(0);
}

.visible .modal {
	opacity: 1;
	transform: scale(1);
	transition: opacity 250ms 500ms ease, transform 350ms 500ms ease;
}

```
- `.modal__wrap` is the class which will have the styling for wrapper and backdrop of the modal.
-  `.modal` is the class which will have the styling of actual Modal component which will be hidden initially.
-  `.visible`  class makes the Modal visible with fade in and fade out effect.

Now let’s create Modal component.
Below is the code snippet for it.

```jsx
//Modal.js

import React, { useEffect, useRef } from 'react';
import Button from '../button/Button';
import CloseIcon from '../CloseIcon';
import styles from './modal.module.css';

const Modal = ({ modalStyle, children, show, onClose, backdropStyle }) => {
	const modalRef = useRef(null);
	useEffect(
		() => {
			if (show) {
				modalRef.current.classList.add(styles.visible);
			}
			else {
				modalRef.current.classList.remove(styles.visible);
			}
		},
		[
			show
		]
	);
	return (
		<React.Fragment>
			<div ref={modalRef} style={backdropStyle} className={`${styles.modal__wrap}`}>
				<Button
					onClick={onClose}
					style={{ width: 60, height: 40, position: 'absolute', top: 0, right: 0, margin: '1rem' }}
					className={styles.close__btn}
				>
					<CloseIcon height="20px" width="20px" className={styles.close__icon} />
				</Button>
				<div style={modalStyle} className={styles.modal}>
					{children}
				</div>
			</div>
		</React.Fragment>
	);
};

export default Modal;

```
This component will take four props:
1.`modalStyle` - With which one can customize the styling of visible modal window.\
2. `backdropStyle` - With which one can customize the styling of the backdrop of modal window.\
3. `onClose` -  Event handler with which one can write logic to close the modal.\
4. `show` - Boolean property which will decide wheather the modal is open or not.\

Here , inside this component we have used two more component [Button](https://satishnaikawadi.me/posts/build-custom-button-component-with-react-js) and CloseIcon. Now Button component is a reusable UI component which we have build in first part of this series tutorial  for which is [here](https://satishnaikawadi.me/posts/build-custom-button-component-with-react-js). CloseIcon is just simply a `svg` icon to close the modal.

This component has two main functional parts
1. Firstly , inside `useEffect()` hook we will check if the show prop is true or not. If show is true , then we will add the `.visible` class to the component  or else we will remove the `.visible` class from the Modal component with the help of `useRef()` react hook.
2. We will add `onClose()` handler passed by props to the `onClick` event handler of CloseIcon , so that modal will close on clicking it.

# A button to trigger an event to show Modal

To make it simple, I added the Button in App.js file as below,
```jsx

//App.js

import React, { useState } from 'react';
import './App.css';
import Button from './components/button/Button';
import Modal from './components/modal/Modal';

function App() {
	const [
		show,
		setShow
	] = useState(false);
	return (
		<React.Fragment>
			<div style={{ display: 'flex', justifyContent: 'center', alignItems: 'center', height: '100vh' }}>
				<Button onClick={() => setShow(true)}>Open Modal</Button>
			</div>
			<Modal show={show} onClose={() => setShow(false)}>
				<div className="content">
					<img src="https://cdn.pixabay.com/photo/2015/01/09/11/11/office-594132__340.jpg" alt="Developer" />
					<div className="text">
						<h2>John Doe</h2>
						<p>
							Lorem ipsum dolor sit amet consectetur adipisicing elit. Saepe aliquid placeat omnis
							adipisci dolores quae amet mollitia sint, temporibus eum magnam facilis odio ex incidunt?
							Deleniti quam et rem obcaecati. Laborum atque odit expedita nulla.
						</p>
						<p>
							Lorem ipsum dolor sit amet consectetur adipisicing elit. Expedita labore laborum, assumenda
							dolorum provident quod itaque earum, officia in placeat dignissimos nostrum? Totam corrupti
							nihil repudiandae ducimus atque quod eos!
						</p>
					</div>
				</div>
			</Modal>
		</React.Fragment>
	);
}

export default App;


```

That’s it you did it. It’s as simple as that. Now you can use this component anywhere in your project.
This is link to [CodeSandbox](https://codesandbox.io/s/gallant-albattani-d29r4?file=/src/components/modal/modal.module.css)  of Modal component.
Let me know if this tutorial was helpful for you guys and for which case you used it.