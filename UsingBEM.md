# Using BEM in Your Project

It can be a challenge to set a consistent standard for how you are using class names across a web application. While there are many possible patterns you can follow, we will be learning one called BEM. BEM is an acronym standing for Block Element Modifier.

# Block

A block represents a piece of HTML that must stay together for it to be useful. As an example, usually a form is made up lables, inputs and a submit button. If we separate the inputs from the labels or the submit button from the form, it would no longer work properly. We can then say that our form is a block.

We give blocks a class name that represent what it is. We already followed this with our info card. 

``` HTML
  <div class="info-card"> <!-- This is our block-->
    <div class="title">Info Card</div>
    <div class="text"> 
      This is an info card with some content.
    </div>
  </div>
```

We write our class names in camel case. Usually, this class name will match the component name when working in React.

# Element

An element is one of the pieces that make up the block. For example, our info card has two elements: the title and the text. 

When using class names like 'title' or 'text', we run the risk of accidentally colliding with the same name in a different component. When following BEM, we will give each of them a class name made of three parts: 

1) the block name - 'info-card'
2) two underscores '__'
3) its own identifier = 'title'

When we put it all together it looks like this: 'info-card__title' and 'info-card__test'. By following this pattern, we have largely reduced our chances of duplicating a style somewhere else in the application to 0. 

Here's what it looks like when we've changed the class names on each element:

``` HTML
  <div class="info-card"> <!-- This is our block-->
    <div class="info-card__title">Info Card</div>
    <div class="info-card__text"> 
      This is an info card with some content.
    </div>
  </div>
```

# SCSS

Now that we've changed our class names to match the BEM paradigm, let's get our SCSS working again. We didn't change the class name of our parent div and we didn't apply any styling to the text on our card, so we have no worries with either of those. Our title has changed however. We previously had a class name of 'title' and now we are using 'info-card__title'. SCSS allows us to use the `&` character to represent all previous nested css selectors. This sounds more complicated than it is. First, here is what it looks like: 

``` css
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

So what is happening here? By the time the SCSS engine has run, it sees that the title is nested under '.info-card' and also that it has `&` meaning it should replace the `&` with the previous class. The result is css that looks like this: 

``` css

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

Don't worry if it doesn't make sense right away. It will become natural with repetition. 

# BEM

To learn more about BEM, head over to [Get BEM](http://getbem.com/naming/)

Let's move into [implementing this into a React project](https://github.com/werner33/AdvancedBasicsForWeb/blob/main/SCSSInYourProject.md). 
