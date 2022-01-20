
1. API Calls Overview

An API call is a request for some resources passed to us over the web. Modern web conventions have many APIs returning JavaScript Object Notation (JSON) that we can consume in a web application. 

In a typical React app we make an API call from the front end like this: 

``` javascript 

  fetch('https://catfact.ninja/fact')
    .then(res => res.json()
    .then(data => {
      console.log(data)
    });
  
```

We might use a library like Axios to save ourselves some work, but [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) is build right into JavaScript.

API calls have five HTTP Methods: GET, POST, PUT, PATCH and DELETE. We won't get into each of them now, but in very basic terms, we use GET to fetch information and we use POST to save information. The other three types are less common.

A great breakdown of how an API is accessed via an HTTP request can be found [here.](https://blog.uptrends.com/technology/the-anatomy-of-an-api-call/)


2. Setting Request Headers

We may want to make a call with special information or parameters. We can set a number of properties by specifying the Request Headers. Request headers are key/value pairs, passed as a second argument in a `fetch` request. 

``` javascript 

  fetch('https://catfact.ninja/fact', {method: 'POST'}) // we can add many other request headers here
    .then(res => res.json()
    .then(data => {
      console.log(data)
    });
  
```

[In this article](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#supplying_request_options) you can see a more fulsome example of how you supply request options. 


3. Where Should Calls Be Made in an Application? 

 In a React application, components are structured in a heirarchy. An API calls should typically be made at the highest level where the data is needed. 
 
 Here is a small example: 
 
 Imagine we are writing an app that will show the names of all students in the school and also, a schedule of after-school activities. 
 
 There are three main components structured like this: 
 
 App\
   |----- StudentCollection\
   |----- Schedule
   
The respective API calls should be made from the component showing the data. 

 App\
   |----- StudentCollection\
        - fetch student data here\
   |----- Schedule\
        - fetch schedule of events here

4. Code Splitting in React

When we send our React project to a client or browser, the whole application is sent by default. The components are not all rendered but the code is all included in the `bundle.js`. This is fine for a small application, but as our application grows, we should see if we can avoid sending code that a user may not use. One strategy we can employ is [Code Splitting](https://reactjs.org/docs/code-splitting.html). 

Let's look at an example where we 'split' one of our routes into its own bundle. 


``` javascript
  const About = React.lazy(() => import('../about/About'));
  
  ...
  
  
   <Suspense fallback={<div>Loading...</div>}>
        <About />
    </Suspense>
```

5. Caching in Session Storage

Imagine we are working on an app that suggests 10 random coffee types to a user each time they load our app. The randomness is seen as desirable as it keeps users coming back to learn about different coffees. However, once they load the randome coffees, in their browser, we don't want the coffee selection to change until they close that tab. For this, we might use a type of short term storage available through the browser called Session storage.

Session storage will store a key value pair where both the key and value are strings. This will be a bit tricky since we will be getting our coffee information back as JSON. 

First, let's look at the basic fetch request to get five random coffees. 

``` javascript 

    let url = 'https://random-data-api.com/api/coffee/random_coffee?size=5';
    
    useEffect( () => {
       fetch(url)
        .then(res => res.json())
        .then((result) => {
            setCoffees([result]); 
        },

          (error) => {
           console.log(error);
          }
        );
    }, [] )
``` 

This code should be familiar. If we include this in a React component it will grab 5 random coffees each time the component is mounted. 

What can we do to prevent getting 5 new random coffees on a refresh? We can save the data to session storage and load it from there.

Let's modify the code above to utilise session storage: 


``` javascript 

    let url = 'https://random-data-api.com/api/coffee/random_coffee?size=5';
    
    useEffect( () => {
    
      if(sessionStorage.coffees ){
        setCoffees([...JSON.parse(sessionStorage.coffees)])
      } else {
       fetch(url)
        .then(res => res.json())
        .then((result) => {
            setCoffees([result]); 
            sessionStorage.setItem('coffees', JSON.stringify(result))

        },
          (error) => {
           console.log(error);
          }
        );
    }, [] )
``` 

Right after we set our hook, we save the data to session storage. With this data saved  
