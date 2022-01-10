
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
 
 APP
   |----- StudentCollection
   |----- Schedule
   
The respective API calls should be made from the component showing the data. 

 APP
   |----- StudentCollection
        - fetch student data here
   |----- Schedule
        - fetch schedule of events here 

4. Code Splitting in React



``` javascript
  const About = React.lazy(() => import('../about/About'));
```

5. Caching in Session Storage

Imagine we are working on a weather API that shows the current days weather but additionally shows the past ten days of weather. It's reasonable to think that the user may want to refresh the data to see if the forecast has changed, but what will not change is the weather from the past ten days. We don't want to requery both APIs whenever we refresh our app. 

We can handle a situation like this by storing the past data to session storage. Our API will first check if the data is stored in the browser, if so, no round trip is necessary. If it is not, we will make a call for the past data. The current data will always be called on refresh because its reasonable to think the user may be looking for the latest forecast. 

``` javascript 

if(sessionStorage.pastWeather ){
   setPastWeather([...JSON.parse(sessionStorage.pastWeather), ...pastWeather])
} else {
    let url = 'https://weather.com/pastWeather';

    fetch(url)
        .then(res => res.json())
        .then((result) => {
            setPastWeather([...pastWeather]); 
            sessionStorage.setItem('pastWeather', JSON.stringify(result))
        },

            (error) => {
            console.log(error);
            }
        );
}
``` 
