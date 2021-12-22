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

# How to Include SCSS in your Project

We can install SCSS for React through NPM just like many other packages. Go to [Install SCSS](https://www.npmjs.com/package/node-sass) to learn more about this library. When you're ready, go ahead and run `npm install node-sass` in your project, whereever your frontend files are. 

At this point, you can rename any `.css` file to `.scss`. Once you do that, you can nest any of your CSS as we did on jsFiddle. 

# What Can SCSS Do?

The reality is that SCSS doesn't take long to learn and significatly improves your front-end work flow. You can check out [Learn SASS](https://sass-lang.com/guide) to see the different things SCSS can do. 

We're going to spend the rest of class learning a few of them. 

# Variables

Just like with any other code, we may have values that are easier to access and remember when they are set to variables. 

Let's start with a simple example: colors. We often use the same colors over and over in a project. Lets create a variable for one of our colors and see how to use it. 

`$primary-color: #333;`

This will instantiate this variable and allow us to use it throughout our file. 

``` CSS
.userCard {
 .userName {
  color: $primary-color;
 }
}
```

Now, instead of working to remember the hexagonal number for our CSS color, we  can choose an eaasy to remember name that can be shared across the project. 

# Partials

CSS files can get very large as your project grows. Just like JavaScript files, you may want to share parts of CSS between more than one file. If you have a piece of styling, that you want to use in more than one file, you can set up a shared CSS file, known as a Partial, by naming it with a `_` to start. 

Let's make an example based on what we just learned with variables.

First, well name our file `colors` but preface it with a `_`: `_colors.scss`.

Then we will import it into another SCSS file by putting the following line at the top:
`@import './_colors' (Depending on how your project is layed out, you may need to alter the path.)

# BEM

[Get BEM](http://getbem.com/naming/)

