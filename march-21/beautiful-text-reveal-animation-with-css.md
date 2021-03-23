In this post , we will build beautiful and very smooth text reveal animation with CSS which can be used for headings and subheadings of our webpages.

![text-reveal-gif.gif](https://res.cloudinary.com/dh1srz69c/image/upload/v1616047104/text_reveal_gif_8f5fea3796.gif)

For building this text reveal animation/effect , we will proceed as below - 
1. Writing Required HTML Code
2. Adding Some Styling To All Elements
3. Creating and Adding Animations Through CSS Keyframes

So lets firstly write some HTML code required for this tutorial.

## Writing Required HTML Code
```html
<div class="container">
        <div class="box">

            <div class="title">
                <span class="block"></span>
                <h1>Satish Naikawadi</h1>
            </div>

            <div class="role">
                <div class="block"></div>
                <p>CS Student,Web Developer,Mobile Developer and UI/UX Designer</p>
            </div>

        </div>
    </div>

```
Here , 'box' `div` is the parent of the both 'title' and 'role' `div`. Inside both these divs ,  we have 'block' `div` which will cover all the text inside it before revealing it. And that is it , this is the tiny amount of HTML code required for this tutorial.

## Adding Some Styling To All Elements
```css
* {
	margin: 0;
	padding: 0;
}
body,
html {
	overflow: hidden;
}
.container {
	width: 100%;
	height: 100vh;
	background: #232323;
	display: flex;
	justify-content: center;
	align-items: center;
}
.container .box {
	width: 500px;
	height: 250px;
	position: relative;
	display: flex;
	justify-content: center;
	flex-direction: column;
}
.container .box .title {
	width: 100%;
	position: relative;
	display: flex;
	align-items: center;
	height: 100px;
}
.container .box .title .block {
	width: 0%;
	height: inherit;
	background: #ffb510;
	position: absolute;
	animation: mainBlock 2s cubic-bezier(0.74, 0.06, 0.4, 0.92) forwards;
	display: flex;
}
.container .box .title h1 {
	font-family: 'Poppins';
	color: #fff;
	font-size: 3rem;
	animation: mainFadeIn 2s forwards;
	animation-delay: 1.6s;
	opacity: 0;
	display: flex;
	align-items: baseline;
	position: relative;
}
.container .box .role {
	width: 100%;
	position: relative;
	display: flex;
	align-items: center;
	height: 30px;
	margin-top: -10px;
}
.container .box .role .block {
	width: 0%;
	height: inherit;
	background: #e91e63;
	position: absolute;
	animation: mainBlock 2s cubic-bezier(0.74, 0.06, 0.4, 0.92) forwards;
	animation-delay: 2s;
	display: flex;
}
.container .box .role p {
	animation: secFadeIn 2s forwards;
	animation-delay: 3.2s;
	opacity: 0;
	font-weight: 400;
	font-family: 'Lato';
	color: #fff;
	font-size: 12px;
	line-height: 1.5;
	text-transform: uppercase;
	letter-spacing: 5px;
}

```
So , this is the styling for all elements. So here to create our reveal effect, we will firstly , make the block to cover all the width of text and make the opacity of text as 0. So after that  we will make width of that block 0 and opacity of text back to 1. So lets see how we can frame these animations through CSS code.

## Creating and Adding Animations Through CSS Keyframes
```css

@keyframes mainBlock {
	0% {
		width: 0%;
		left: 0;
	}
	50% {
		width: 100%;
		left: 0;
	}
	100% {
		width: 0;
		left: 100%;
	}
}
@keyframes mainFadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}
@keyframes secFadeIn {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 0.5;
	}
}


```
- mainBlock - The animations for both blocks before revealing actual text.
- mainFadeIn - The animations for heading text.
- secFadeIn - The animation for subtitle/role text.


So that't it. With this much small code we have build really very **Beautiful and Awesome Text Animation**. I hope this will help you to enhance your CSS skills. Thank you for reading !!
.