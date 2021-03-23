In this post , we will look at how we can easily create a beautiful ❤️ image hover text overlay effect with HTML and CSS. For this tutorial , 
you must have basic knowledge of HTML and CSS properties.

![body.gif](https://res.cloudinary.com/dh1srz69c/image/upload/v1614963998/body_356837f6aa.gif)

## ✨ Writing HTML
Our HTML code will be only few lines for the markup.The code is
```html
    <div class="image">
        <img class="image__img" src="https://cdn.pixabay.com/photo/2017/12/15/13/51/polynesia-3021072__340.jpg"
            alt="Bricks">
        <div class="image__overlay">
            <div class="image__title">Ocean</div>
            <p class="image__description">
                Enjoy the blue color of ocean.
            </p>
        </div>
    </div>
```
Here on top we have a `div` with `class` image which is parent 👨‍👧 of all the elements. After that inside this `div` we have `img` tag to render our image. Below that we have `div` with `class` image__overlay which will gets displayed when we hover on our image. Inside this we can put any text related to our image we want to display on overlay.

## 🤩 Lets Create Actual Effect With CSS
Here , first we will apply some basic styling to our `img` tag. We will make its `width` and `height` properties to take whole available size of its parent. 
```css
.image__img {
	display: block;
	width: 100%;
	height: 100%;
	background-size: cover;
}
```
We will make `position` property of a parent image container `relative` and that of overlay to `absolute` so that we can position the overlay with 
respect to dimensions of image container. So, after that we will make `top` and `left` properties of overlay to zero , so that it will start right from top left corner of image container. We will make its`width` and `height` to 100% , so it can fill entire width of the image container and covers it completely. Now we will make `background` of this overlay to black with little opacity so that we can see underlying image. We will also add some `CSS` for styling our text. After that , we add `transition` to overlay so that it feels smooth.\
```css
.image {
	position: relative;
	width: 30%;
}

.image__overlay {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: rgba(0, 0, 0, 0.6);
	color: #ffffff;
	font-family: 'Quicksand', sans-serif;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	transition: opacity 0.25s;
}
```
Now , most important 🛎️  part if we leave as it is , then we will see that overlay is present on the image from the start. But we only want it appear on `hover` over image. So , at beginning we will set `opacity` of overlay to zero and on `hover` we will make it 1.
```css
// at start
.image__overlay{
      opacity: 0;
}

// on hover
.image__overlay:hover {
	opacity: 1;
}
```
And thats it , we have completed our **Image Hover text Overlay Effect**  💪.\
We can also modify this overlay effect to have blurred overlay or solid color overlay. We will just add following simple classes to our CSS file and then add them to our overlay div in HTML.
```css
.image__overlay--blur {
	backdrop-filter: blur(5px);
}

.image__overlay--solid {
	background: #c51f5d;
}
```
As simple as that. And we have created three cool CSS Hover effects with such a liitle code. Hope this will help you 😇.