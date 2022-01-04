# SCSS And BEM

As a web project grows, it can be quite difficult to manage ever growing CSS files and nested HTML elements. In this lesson, we're going to learn some approaches and tools that can help us manage this complexity.

# SCSS

SCSS (called Sass, as in, don't give me that sass!) is a CSS engine that allows us to nest our css, similar to how we nest HTML elements. Let's give it try by starting out on [jsFiddle.net](https://www.jsfiddle.net). 

First, in the CSS box, select SCSS from the drop down menu.

<img width="588" alt="Screen Shot 2021-12-06 at 1 35 51 PM" src="https://user-images.githubusercontent.com/692461/144902723-c5ef5cb0-a45d-4beb-a81a-c76937524416.png">

Let's build something simple like this:

<img width="406" alt="Screen Shot 2021-12-06 at 1 40 53 PM" src="https://user-images.githubusercontent.com/692461/144903284-a859778a-7c17-4d8d-8350-b61e7dd9ea51.png">


Let's set the whole card up inside of a div with a class name of 'userCard'. Then each element under that, we can nest in our SCSS:

``` CSS
.userCard {
  .profileImage {
    border-radius: 20px;
    height: 40px;
  }
}
```
Let's work through styling more of this card, nesting our styling as we go. 

# BEM

[Get BEM](http://getbem.com/naming/)

