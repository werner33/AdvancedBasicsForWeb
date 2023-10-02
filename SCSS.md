# SCSS And BEM

As a web project grows, it can be quite difficult to manage ever growing CSS files and nested HTML elements. In this lesson, we're going to learn some approaches and tools that can help us manage this complexity.

# Prerequisites

Before beginning this lesson, you should be familiar with <br />
[HTML](https://github.com/joinpursuit/Pursuit-Core-Web/tree/master/html_css_dom/html_introduction_combined)  <br /> 
[CSS](https://github.com/joinpursuit/Pursuit-Core-Web/tree/master/html_css_dom/css_intro)  <br />
[Building a React Application](https://github.com/joinpursuit/Pursuit-Core-Web/blob/master/react/README.md) 

You can review any of those things at their respective links.

# SCSS

SCSS (called Sass, as in, don't give me that sass!) is a CSS engine that allows us to nest our css, similar to how we nest HTML elements. Before we implement it in a React project, let's give it try by starting out on [Codepen](https://codepen.io/). 

First, in the CSS box, select the gear icon:

<img width="573" alt="Screen Shot 2023-10-02 at 2 52 37 PM" src="https://github.com/werner33/AdvancedBasicsForWeb/assets/692461/2ff83fde-1ce1-4da1-ab5c-f7e1c43b5ca9">

This will open a settings panel. You can see this is in the following image:

<img width="783" alt="Screen Shot 2023-10-02 at 2 52 48 PM" src="https://github.com/werner33/AdvancedBasicsForWeb/assets/692461/575c7fe2-7cd1-4945-9f38-dcd22b836e54">

Click the dropdown and select SCSS from the list of pre-processors.


Let's build a simple component with a title and a bit of text:

<img width="359" alt="Screen Shot 2022-01-13 at 2 30 45 PM" src="https://user-images.githubusercontent.com/692461/149396750-ca0c3e22-7715-452a-bdcb-96228b952e73.png">

First, let's write out all the HTML. We'll use the component we built in the first part of this lession:

``` HTML

<div class="info-card">
  <div class="info-card__title">Info Card</div>
  <div class="info-card__text"> 
    This is an info card with some content.
  </div>
</div>

```

Next we move to the styling with CSS. Without SCSS, we would need to write our styles like this: 

``` CSS 

.info-card {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
}

.info-card .info-card__title {
   font-weight: 600;
   padding: 10px;
}
```

However, as long as we have selected the SCSS from the dropdown (as shown above), we can start to use one of the features of SCSS - nested styling.

``` CSS
.info-card {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  
  &__title {
   font-weight: 600;
   padding: 10px;
  }
}
```

We have only scratched the surface of what is possible through SCSS, but hopefully this demonstrates that it is just CSS with a few extra capabilities. 

NOTE: You can always run vanilla CSS in a file ending with `.scss`. In other words, you can change the file extension without having to re-write the whole file.

Before we move into working on a React project, [let's improve our Info Card by using BEM notation](https://github.com/werner33/AdvancedBasicsForWeb/blob/main/UsingBEM.md).

