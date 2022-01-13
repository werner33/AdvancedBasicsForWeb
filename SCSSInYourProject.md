# How to Include SCSS in your Project

You can add SCSS into an existing react project or create a new project. If you are working in an existing project, feel free to skip the next section. 

# Creating a new React App

If you don't have an app that you are currently working on, you can create a new project by opening your terminal and using `create-react-app`.

`$ npx create-react-app scss_exercise`

`$ cd scss_exercise`

Then you can start your server with `$ npm start`.

# Installing SCSS

We can install SCSS for React through NPM just like many other packages. Go to [Install SCSS](https://www.npmjs.com/package/node-sass) to learn more about this library. When you're ready, go ahead and run `npm install node-sass` in your project. 

Once the instlation is completed, go ahead and rename one of the files ending with `.css` file to `.scss`. Once you have made this change, make sure you also change the import statement for the css file.

Once you've made these changes, check to see that your application is still running correctly. If there are any errors, take time to resolve those now. 


# Nesting our SCSS

If you are working in an existing project, pick a small section of CSS that you can nest inside another, as we did when using jsfiddle. If you would rather build a new component, let's build an InfoCard based off the card we built earlier in this lesson. 

Make a file called `InfoCard.js` with the following content: 

``` javascript

 import React from 'react';
 
 import './InfoCard.scss'
 
 const InfoCard = () => {
  
  return (
    <div class="infoCard"> 
      <div class="infoCard__title">Info Card</div>
      <div class="infoCard__text"> 
        This is an info card with some content.
      </div>
    </div>
  )
 
 }

```

Then create a `.scss` file that you import into the previous component:


``` css

.infoCard {
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

Finally, import and render the InfoCard into your `App.js` file that was generated when you created your app.

``` js 

import React from 'react'

import InfoCard from './InfoCard';

function App() {
  
  return (
    <div className="app">
     <InfoCard />
    </div>
  );
}

export default App;

```

# Run the App

You should now have the `InfoCard` running in your browser with the `InfoCard.scss` file imported and the styles applied correctly to your component. 

Now that we have our app running with SCSS. Let's finish by [looking at a couple more things SCSS can do](). 

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
