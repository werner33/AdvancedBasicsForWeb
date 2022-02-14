# Client Side Storage

In order to give users the best experience possible, we may want to store some data in the browser. This could be something relatively simple such as a set of user preferences or some JSON data, stored as a string. In this course, we looked at one example of this through using session storage to cut down on unneccessary API calls. 

Each of the four ways to store data in the browser has its pros and cons. Through this lesson, we'll look at the best way to work with each of them.

Let's begin with creating a new React project: `npx create-react-app client-side-storage`.


# Cookies

Cookies are the smallest most restrictive pieces of data we save to the client. All of our cookie are passed along with any API calls we make to the server. With this in mind, we should only save things as a cookie if we absolutely need them to make successful API calls. 

While there are many great libraries to help us set and get cookies, let's write our own functions now. 

Create a directory called `utils` and inside of it, let's make a file called `cookies.js`. 

First, let's write two functions called `setCookie` and `getCookie` and then export both. Your file should look like this: 

``` javascript

const setCookie = () => {
    
}

const getCookie = () => {
    
}

module.exports = {setCookie, getCookie};

```

When we create a cookie, it is composed of three parts: a key, a value and an expiration. Keys and values are likely familiar to you from working with Objects or JSON. One thing to note is that a cookie can only store a string as its value. Remember that for many datatypes, you can cast them to a string by called `toString` on them. 
