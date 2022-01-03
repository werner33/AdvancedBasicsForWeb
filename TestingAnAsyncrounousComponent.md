# Testing an Asynchronous Component

We've come very far in understanding how to test our frontend components. Many times, a frontend component calls out to an API for some data to show to the user. We don't know how long the response will take or if we will get exactly what we expected. In this case, we need our test to pause while we wait for the response and then assert that we got the expected response. 

1. Render a New Component Called CatFact

Let's set up a directory for a new component called `CatFact`. As with the previous exercises in this section, the directory should have a component called `CatFact.js` and a directory to hold the test file, `__test__`. 

As always, lets follow a Test Driven Development approach to building this component. We'll start with a test file called `catFact.test.js`. and the contents should look like this: 

``` javascript 

  import { render } from '@testing-library/react';

  import CatFact from '../CatFact';
  
   describe('CatFact displays random catfact on mount and a new one on each button click', () => {
    
    it('renders CatFact component', () => {
        render(<CatFact />);
    });
    
  }
```

Go ahead and run your tests at the command line with `npm test catFact`.

Fix the failing test, by putting together a basic functional component. 

2. Component Layout

This component will have two basic elements. First, there will be an area to display a cat fact and second, a button that will load a new cat fact. Let's write the tests for each of these now.

``` javascript

  import { render } from '@testing-library/react';

  import CatFact from '../CatFact';
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
    
    ...
    it('has an element to display the text of a cat fact', () => {
        const {getByTestId} = render(<CatFact />);
        
        expect(getByTestId('catFact__textContainer')).toBeInTheDocument()
    })
    
    it('has a button to load a new cat fact', () => {
        const {getByTestId} = render(<CatFact />);
        
        expect(getByTestId('catFact__button')).toBeInTheDocument();
    });
    
  }

```

Write the code to make these tests pass. 

Remember that setting up a testid on any HTML element looks like this: 

``` HTML
  <div data-testid="catFact__button"></div>
```

3. Writing the Tests for Initial Mount

When our component initially loads, we need to query the API on mount to bring in the first random cat fact. Until the fact is returned, we want our button to display 'Loading...' and we expect our text container to be empty.

Let's write a test that asserts that the button should say 'Loading...' when we first render our component: 

``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   ...
   
    it('button text initializes to "Loading..."', () => {
        
        const{getByText} = render(<CatFact />);

        expect(getByText('Loading...')).toBeInTheDocument();

    });
  }

```

That's it. We are simply asserting that before anything happens, out button says 'Loading...'. If you run this in the browser when calling the API correctly, you may not even see the loading text. But our test is fast and will verify that the button defaults to 'Loading...' even if the API call is very fast.

Now, we don't have a fact when the component initially loads, so we expect our text container to be empty. Let's write a test for this: 

``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   ...
    
    it('has no text in textContainer on mount', () => {
        const{getByTestId} = render(<CatFact />);

        expect(getByTestId('catFact__textContainer')).toBeEmptyDOMElement()
    })
  }

```

Write the code to make this test pass. Note that you do not need to set up an API call, nor change the button text for this test to pass. 

4. Writing Tests for Asynchronous Behaviour On Mount

As soon as the component mounts, lets call out cat fact api. You can reach it here: `call to `https://catfact.ninja/fact`. The response from the API will look something like this: 

``` json
  {
    "fact":"All cats have three sets of long hairs that are sensitive to pressure - whiskers, eyebrows,and the hairs between their paw pads.",
    "length":128
  }
```

We want to do two thigs and we need a test to assert each of them. First, we want our button text to change to 'Load Cat Fact' once our API response is returned.

``` javascript
  ...

  describe('', () => {
  ...
    it('changes button text to "Load Cat Fact" on successful mount', async () => {
          const{getByText, findByText, queryByText} = render(<CatFact />);

          expect(getByText('Loading...')).toBeInTheDocument();

          await findByText('Load Cat Fact');

          expect(queryByText('Loading...')).not.toBeInTheDocument();
      })
  })

```

Note that with this test, since we are testing something asynchronous, we need to preface our callback with the `async` keyword. 

We need to check that once the call is returned, the button text is back to 'Load Cat Fact' and then fact itself has changed. We will use a new Jest method called `findByText` to do this. Using `findByText` tells our test to look for something and to remain looking for it for up to 4 seconds. If it is not found after 4 seconds, the test will fail. Otherwise the test will pass. Under any normal circumstances, our API should return the expected result in less than 4 seconds. 

To make this test pass, create a hook called `loading` that starts as true but is set to false when the API returns. Then make the text on the button dependent on the hook. When `loading` is true, the button test should be 'Loading...' and then when it is false, the button text should be 'Load Cat Fact'. 

We also introduce an assertion modifier here: `expect(queryByText('Loading...')).not.toBeInTheDocument();` We use not to say that we are looking for the opposite of the assertion. 

Let's move on to asserting that on a successful API call, we place the text of the cat fact in the text container. 

describe('', () => {
  ...
    it('displays a catfact on successful mount', async () => {
        const {getByTestId, findByText} = render(<CatFact />);

        await findByText('Load Cat Fact');

        expect(getByTestId('catFact__textContainer')).not.toBeEmptyDOMElement();
    })
  })

```

Here we assert that after the successful API call, the text container is not empty. You can handle this by setting a hook called `catFact`, setting it to an empty string when you start and set it to the cat fact when the API returns. 

5. Writing the Tests for Asynchronous Behavior on User Interaction

Finally, we will wrap up our testing by making assertions for the asynchronous behaviors of our component when the button is clicked. The component should make a call to `https://catfact.ninja/fact` and replace the old fact with the new one. 

We need to check that when the button is clicked, the text changes to 'Loading...'. Once the call is returned, the button text is back to 'Load Cat Fact'.

Additionally,  the fact itself will have changed. 

Let's start by writing the test for the button text changing and then returning to 'Load Cat Fact'. We will use the `click()` event here that we used in the last chapter. 

``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   ...
   
  it('changes button text on button click until API responds', async () => {
       
        const{getByTestId, findByText, queryByText} = render(<CatFact />);

        await findByText('Load Cat Fact');

        let button = getByTestId('catFact__button');
        
        button.click();

        await findByText('Load Cat Fact');
        
        expect(queryByText("Loading...")).not.toBeInTheDocument();
    })
  }

```

Write the code to make this test pass. 

Finally, we want to write a test to make sure the text changes when a new fact is loaded. Since the facts are randomly loaded, we will save the current fact text and then make sure that it is no longer in the DOM after a new fact is loaded. Let's do that now: 

``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   ...
   
   it('changes cat fact text on button click', async () => {
        const{getByTestId, findByText, queryByText, queryByTestId} = render(<CatFact />);

        await findByText('Load Cat Fact');

        let firstCatFact = getByTestId("catFact__textContainer").innerHTML;

        let button = getByTestId('catFact__button');
        
        button.click();

        await findByText('Load Cat Fact');

        expect(queryByText(firstCatFact)).not.toBeInTheDocument();
        expect(queryByTestId("catFact__textContainer")).not.toBeEmptyDOMElement();
    })
 })
```

Write code to change the cat fact on a successful API response and this test should pass just fine. We don't know what text we are expecting, but we can test that the old text is no longer shown. 

We have now written a good set of comprehensive tests for an asynchronous component. If you would like to go further, you can test for unsuccessful responses that result in errors and make sure your component is properly handling those as well. 

5. Conclusion

Testing is a deep subject and we have only gotten started here. Take a look at the Jest or Testing Library documentation to learn more about what you can do with frontend testing. 


