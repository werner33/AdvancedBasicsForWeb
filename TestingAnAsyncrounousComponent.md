# Testing an Asynchronous Component

We've come very far in understanding how to test our frontend components. Many times, a frontend component calls out to an API for some data to show to the user. We don't know how long the response will take or if we will get exactly what we expected. In this case, we need our test to pause while we wait for the response and then assert that we got the expected response. 

1. Create a New Component Called CatFact

Let's set up a directory for a new component called `CatFact`. As with the previous exercises in this section, the directory should have a component called `CatFact.js` and a directory to hold the test file, `__test__`. 

As always, lets follow a Test Driven Development Approach to this component. We'll start with a test file called `catFact.test.js`. and the contents should look like this: 

``` javascript 

  import { render } from '@testing-library/react';

  import CatFact from '../CatFact';
```

Go ahead and run your tests at the command line with `npm test catFact`.

Fix the failing test, by putting together a basic functional component. 

2. Component Layout

This component will have two basic elements. First, there will be an area to display a cat fact and second, a button that will load a new cat fact. Let's write the tests for each of these now.

We'll start by writing our `describe` block with a basic text to render the component: 

``` javascript

  import { render } from '@testing-library/react';

  import CatFact from '../CatFact';
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
    
    it('renders CatFact component', () => {
        render(<CatFact />);
    });
    
  }

```

Then, we'll go ahead and write assertions for each of these two elements inside the describe block: 


``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   
    it('renders CatFact component', () => { 
        render(<CatFact />);
    });
    
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

3. Writing the Tests for Initial Mount

<!-- Until now, we have tested that our component will load correctly and that the elements of the component are in place. We need to go one big step further however and  verify that new cat facts can be loaded by clicking on the button. 

In order to set up out asynchronous tests, we must think through what will happen when we click our button. In this case, let's say that the button text should immediately change to say 'loading'. Once the call is returned, we expect the text to change to the new cat fact and then button text should return to 'Load Cat Fact'.

Checking for the button text to change immediately is a synchronous change, no different than what we did with the Counter component in the previous section. Let's set that up now: -->

``` javascript
  ...
  
  describe('CatFact displays random catfact on mount and a new one on each button click', () => {
   ...
   
    it('button text initializes to "Loading..." on mount', () => {
        
        const{getByText} = render(<CatFact />);

        expect(getByText('Loading...')).toBeInTheDocument();

    });
    
    it('has no text in textContainer on mount', () => {
        const{getByTestId} = render(<CatFact />);

        expect(getByTestId('catFact__textContainer')).toBeEmptyDOMElement()
    })
  }

```

Write the code to make this test pass. Note that you do not need to set up an API call, nor change the text back to 'Load Cat Fact' for this test to pass. 

4. Writing Tests for Component On Mount

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

    it('displays a catfact on successful mount', async () => {
        const {getByTestId, findByText} = render(<CatFact />);

        await findByText('Load Cat Fact');

        expect(getByTestId('catFact__textContainer')).not.toBeEmptyDOMElement();
    })
  })

```

5. Writing the Tests for Asynchronous Behavior

Finally, we will wrap up our testing by making assertions for the asynchronous behaviors of our component. When the button is clicked, the component should make a call to `https://catfact.ninja/fact`. The response will look something like this: 

``` json
  {
    "fact":"All cats have three sets of long hairs that are sensitive to pressure - whiskers, eyebrows,and the hairs between their paw pads.",
    "length":128
  }
```

We need to check that once the call is returned, the button text is back to 'Load Cat Fact' and then fact itself has changed. We will use a new Jest method called `findByTestId` and `findByText` to do this. Using `findBy` tells our test to look for something and to remain looking for it for up to 4 seconds. If it is not found after 4 seconds, the test will fail. Otherwise the test will pass. Under any normal circumstances, our API should return the expected result in less than 4 seconds. 

Let's start by writing the test for the button text returning to 'Load Cat Fact'. Note that because we are testing asynchronous behavior, we need to preface our callback with the `async` keyword. When we use the `findByText` query we will use the corresponding `await` keyword. 

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

Write the code to make this test pass. At this point, you will need to write an API call and set a hook to track the loading status as we've done in previous lessons.

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

