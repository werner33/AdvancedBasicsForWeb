# SCSS And BEM

As a web project grows, it can be quite difficult to manage ever growing CSS files and nested HTML elements. In this lesson, we're going to learn some approaches and tools that can help us manage this complexity.

# SCSS

SCSS (called Sass, as in, don't give me that sass!) is a CSS engine that allows us to nest our css, similar to how we nest HTML elements. Let's give it try by starting out on [jsFiddle.net](https://www.jsfiddle.net). 

First, in the CSS box, select SCSS from the drop down menu.

<img width="588" alt="Screen Shot 2021-12-06 at 1 35 51 PM" src="https://user-images.githubusercontent.com/692461/144902723-c5ef5cb0-a45d-4beb-a81a-c76937524416.png">

Let's build something simple like this:

<img width="359" alt="Screen Shot 2022-01-13 at 2 30 45 PM" src="https://user-images.githubusercontent.com/692461/149396750-ca0c3e22-7715-452a-bdcb-96228b952e73.png">


Let's outline the whole card up with HTML:

``` HTML

<div class="infoCard">
  <div class="title" />
  <div class="text" />
</div>

```


Then each element under that, we can nest in our SCSS:

``` CSS
.infoCard {
  text-align: center;
  
  .title {
   font-weight: 600;
  }
  
}
```

Let's work through styling more of this card, nesting our styling as we go.

