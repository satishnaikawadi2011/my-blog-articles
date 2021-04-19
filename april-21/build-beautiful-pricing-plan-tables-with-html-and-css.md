In this post , we will look at how we can easily create a beautiful ❤️ pricing plan tables with HTML and CSS. For this tutorial , you must have basic knowledge of HTML and CSS properties.

## ✨ Writing HTML
Our HTML code will be only few lines for the markup.The code is
```html
<section class="pricing-plan">
            <div class="pricing-plan__header">
                <h1 class="pricing-plan__title">
                    starter plan
                </h1>
                <h2 class="pricing-plan__summary">
                    Serious learning, best for students and self learners
                </h2>
            </div>
            <div class="pricing-plan__description">
                <ul class="pricing-plan__list">
                    <li class="pricing-plan__feature">
                        Everything included in free
                    </li>
                    <li class="pricing-plan__feature">
                        Access to all interactive courses
                    </li>
                    <li class="pricing-plan__feature">
                        Access to all hands-on practice projects
                    </li>
                    <li class="pricing-plan__feature">
                        Unlimited practice lab time
                    </li>
                    <li class="pricing-plan__feature">
                        Full access to learning paths
                    </li>
                </ul>
            </div>
            <div class="pricing-plan__actions">
                <p class="pricing-plan__cost">$75</p>
                <p class="pricing-plan__text">
                    per month
                </p>
                <a href="#" class="pricing-plan__button">
                    Buy
                </a>
                <p class="pricing-plan__text">Minimum spend $750 over 12 months</p>
            </div>
        </section>
```
Here we have 3 main parts in this HTML markup\
1.`div` with `class` of  **pricing-plan__header** which contains main title and short summary of the pricing plan.\
2.`div` with `class` of  **pricing-plan__description** which contains the list of all the features of pricing plan.\
3. `div` with `class` of  **pricing-plan__actions** which contains cost and button to buy the pricing plan.


## 🤩 Lets Style Our Pricing Plan Table With CSS
Below is the CSS styling for the above HTML markup.
```css
.pricing-plan {
	width: 300px;
	border-radius: 25px;
	box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
	overflow: hidden;
	font-family: sans-serif;
	font-size: 16px;
	line-height: 1.5;
	color: #555555;
	margin: 15px;
}

.pricing-plan__header {
	padding: 25px;
	background: #666699;
	color: white;
}

.pricing-plan__title,
.pricing-plan__summary {
	margin: 0;
	text-align: center;
	text-transform: capitalize;
}

.pricing-plan__title {
	font-size: 1.5rem;
	font-weight: 400;
}

.pricing-plan__summary {
	font-size: 1rem;
	font-weight: 300;
}

.pricing-plan__description {
	padding: 25px;
}

.pricing-plan__list {
	padding: 0;
	margin: 0;
}

.pricing-plan__feature {
	list-style: none;
	margin: 0;
	padding-left: 25px;
	position: relative;
	font-size: 0.95rem;
}

.pricing-plan__feature:not(:last-child) {
	margin-bottom: 0.5rem;
}

.pricing-plan__feature::before {
	content: '\2714';
	position: absolute;
	left: 0;
	color: #666699;
}

.pricing-plan__actions {
	padding: 25px;
	border-top: 1px solid #eeeeee;
	display: flex;
	flex-direction: column;
}

.pricing-plan__button {
	display: inline-block;
	margin: 15px auto;
	padding: 8px 20px;
	text-decoration: none;
	color: #666699;
	background: white;
	border-radius: 5px;
	border: 1px solid #666699;
	text-transform: uppercase;
	letter-spacing: 0.02rem;
	font-weight: bold;
	transition: all 300ms linear;
}

.pricing-plan__button:hover {
	background: #666699;
	color: white;
}

.pricing-plan__cost {
	margin: 0;
	text-align: center;
	font-size: 2rem;
	color: #000000;
}

.pricing-plan__text {
	font-size: 0.9rem;
	text-align: center;
	margin: 0 0 10px 0;
}

```
Now this will give us the following result.
![first-demo.png](https://res.cloudinary.com/dh1srz69c/image/upload/v1618685573/first_demo_d800f39cda.png)

We can also modify this pricing plan table by using some modifier classes. We will just add following simple classes to our CSS file and then add them to our  div in HTML.
```css
.pricing-plan__header--blue {
	background-color: #7f53ac;
	background: linear-gradient(315deg, #7f53ac 0%, #647dee 74%);
}

.pricing-plan__header--orange {
	background-color: #a40606;
	background: linear-gradient(315deg, #a40606 0%, #d98324 74%);
}

.pricing-plan--recommended {
	box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.2);
}
.pricing-plan__special-text {
	padding: 10px;
	text-align: center;
	font-weight: bolder;
	background: #ffc857;
	box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.2) inset;
}

.pricing-plan__header--special {
	background-color: #ffc857;
	background: linear-gradient(316deg, #ffc857 0%, #3e2f5b 74%);
}

```
And modify the HTML as below.
```html
<section class="pricing-plan">
    <div class="pricing-plan__header pricing-plan__header--orange">
        ...........
    </div>
    <div class="pricing-plan__description">
        ...........
    </div>
    <div class="pricing-plan__actions">
        ...........
    </div>
</section>
<section class="pricing-plan pricing-plan--recommended">
    <div class="pricing-plan__special-text">
        Recommended
    </div>
    <div class="pricing-plan__header pricing-plan__header--special">
        ...........
    </div>
    <div class="pricing-plan__description">
        ...........
    </div>
    <div class="pricing-plan__actions">
        ...........
    </div>
</section>
<section class="pricing-plan">
    <div class="pricing-plan__header pricing-plan__header--blue">
        ...........
    </div>
    <div class="pricing-plan__description">
        ...........
    </div>
    <div class="pricing-plan__actions">
        ...........
    </div>
</section>
```
Then we will get the result like below.
![pricing-plan-tables.png](https://res.cloudinary.com/dh1srz69c/image/upload/v1618684459/pricing_plan_tables_c193d1fc23.png)

That is it for this article. And we have created three cool CSS and HTML **Pricing Plan Tables**. Hope this will help you 😇. Thank you for reading.