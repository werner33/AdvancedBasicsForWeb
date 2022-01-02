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
  
  describe('this is a component to load and display a random cat fact', () => {
    
    it('renders CatFact component', () => {
        render(<CatFact />);
    });
    
  }

```

Then, we'll go ahead and write assertions for each of these two elements inside the describe block: 


``` javascript
  ...
  
  describe('this is a component to load and display a random cat fact', () => {
   
    it('renders CatFact component', () => { 
        render(<CatFact />);
    });
    
    it('has an area to display the text of a cat fact', () => {
        const {getByTestId} = render(<CatFact />);
        
        expect(getByTestId('catFact__textContainer')).toBeInTheDocument()
    })
    
     it('has a button to load a new cat fact', () => {
        const {getByTestId, getByText} = render(<CatFact />);
        
        expect(getByTestId('catFact__button')).toBeInTheDocument();
        expect(getByText('Load Cat Fact')).toBeInTheDocument();

    })
  }

```

Write the code to make these tests pass. 

3. 
