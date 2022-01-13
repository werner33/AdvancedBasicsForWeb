# Using SCSS in Your Own Project

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
