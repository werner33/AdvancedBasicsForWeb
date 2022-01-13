# SCSS And BEM

As a web project grows, it can be quite difficult to manage ever growing CSS files and nested HTML elements. In this lesson, we're going to learn some approaches and tools that can help us manage this complexity.

# SCSS

SCSS (called Sass, as in, don't give me that sass!) is a CSS engine that allows us to nest our css, similar to how we nest HTML elements. Before we implement it in a React project, let's give it try by starting out on [jsFiddle.net](https://www.jsfiddle.net). 

First, in the CSS box, select SCSS from the drop down menu. You can see this is in the following image:

<img width="588" alt="Screen Shot 2021-12-06 at 1 35 51 PM" src="https://user-images.githubusercontent.com/692461/144902723-c5ef5cb0-a45d-4beb-a81a-c76937524416.png">

Let's build a simple component with a title and a bit of text:

<img width="359" alt="Screen Shot 2022-01-13 at 2 30 45 PM" src="https://user-images.githubusercontent.com/692461/149396750-ca0c3e22-7715-452a-bdcb-96228b952e73.png">

First, let's write out all the HTML:

``` HTML

<div class="infoCard">
  <div class="title">Info Card</div>
  <div class="text"> 
    This is an info card with some content.
  </div>
</div>

```

Next we move to the styling with CSS. Without SCSS, we would need to write our styles like this: 

``` CSS 

.infoCard {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
}

.infoCard .title {
   font-weight: 600;
   padding: 10px;
}
```

However, as long as we have selected the SCSS from the dropdown (as shown above), we can start to use one of the features of SCSS - nested styling.

``` CSS
.infoCard {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  
  .title {
   font-weight: 600;
   padding: 10px;
  }
  
}
```

We have only scratched the surface of what is possible through SCSS, but hopefully this demonstrates that it is just CSS with a few extra capabilities. You can always run vanilla CSS in a file ending with `.scss'. 

Before we move into working on a React project, [let's improve our Info Card by using BEM notation]().

