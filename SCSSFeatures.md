# What More Can SCSS Do?

The reality is that SCSS doesn't take long to learn and significatly improves your front-end work flow. We're going to spend the rest of class looking at a few more SCSS features. 

# Variables

Let's imagine we want to set a background color for our `InfoCard`. Lets set a background color of `#99d6ff`. It's basically a light blue.

Let's update our `InfoCard.scss` file: 

``` css 
.info-card {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  background-color: #99d6ff;
  
  &__title {
   font-weight: 600;
   padding: 10px;
  } 
}

```

We often use the same colors in many places in an application. At the same time, it can be difficult to remember the hex number that represents a particular color.  Just like with any other code, we may have values that are easier to access and remember when they are set to variables. Let's use SASS to set a variable for this color.  

A variable name in SASS always starts with a `$` followed by a string. Let's call this color `$sky-blue`.

`$sky-blue: #99d6ff;`

In order to use this variable, lets set it at the top of our `InfoCard.scss` file and then use it like this: 

``` css 
$sky-blue: #99d6ff;

.info-card {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  background-color: $sky-blue;
  
  &__title {
   font-weight: 600;
   padding: 10px;
  }
}

```

We can now use this variable any number of times in this file.

# Partials

CSS files can get very large as your project grows. Just like JavaScript files, you may want to share parts of CSS between more than one file. If you have a piece of styling, that you want to use in more than one file, you can set up a shared CSS file, known as a Partial, by naming it with a `_` to start. 

Let's make an example based on what we just learned with variables.

First, we'll create a  file called `_colors.scss`. Note that because it will be imported into another SASS file, the file name starts with `_`. 

Let's move our variable `$sky-blue` into this `_colors.scss` file. 

``` css 
$sky-blue: #99d6ff;

```

For now, that is all we will put here, but we can build out a palatte of colors as our project grows.


Next, we will remove the `$sky-blue` variable from `InfoCard.scss` and import our `_colors.scss` file:

``` css 
@import './colors.scss'

.info-card {
  text-align: center;
  border: 1px solid black;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  background-color: $sky-blue;
  
  &__title {
   font-weight: 600;
   padding: 10px;
  }
}

```

(Depending on how your project is layed out, you may need to alter the import path.)

Although the partial is written with an underscore at the beginning of the name, the underscore is omitted when the file is imported. 

We are now set up to include and use this and any other variables we create throughout the application. 

# Continuing with SCSS

SCSS offers some additional wonderful features. You can learn more about them at [SASS Basics](https://sass-lang.com/guide)
