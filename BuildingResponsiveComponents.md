# Building Responsive Components

When building a React project, we will compose our page by utilizing many components. Since so many people access the internet on their cell phones, we want our site to be readable and usable on both desktop computers and cell phones. When a component is presentable and useable on desktop and mobile, we call this responsive.

We can make our component responsive by applying different styles through our SCSS files. In order to decide what styles to attach, we will use media queries.

# Media Queries

Media queries are conditional statements in our SCSS or CSS files that look at the size of the screen of a given user, and then conditionally attaches styles. Generally, we will query the pixel width of a screen to decide what styles to apply. 

Let's look at a basic media query. 

``` CSS
  @media only screen and (max-width: 440px) { 
    p {
      color: blue;
    }
  }
```

This query is saying on any device, with a width of 440px or less, the text color of a `<p>` element would be blue. On any screen wider than 440px, the color would be the default black. 

You can read more about media queries [here](https://www.w3schools.com/css/css_rwd_mediaqueries.asp).

# Building a Responsive Nav Bar

In this lesson, we will create a new React app and build a responsive nav bar with a logo and a list of nav links. 

To begin: 

1. Open a terminal and start a new React project: `npx create-react-app responsive-navbar`.

2. Move into the directory you just created: `cd responsive-navbar`

3. Install SCSS: `npm install sass`

4. Run the project: `npm start`

5. After you have verified that the project is running properly, remove all the code in the `<header>` element of `app.js` and everything inside `app.css`

With that, we are ready to start building our navbar! Let's move to the [next section]().
