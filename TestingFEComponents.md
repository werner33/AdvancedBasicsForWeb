# Testing Front-End Components in React

Writing tests can help up define what we want a component to do, even before we've written the first line of code. A simple component may be used to render some static text. Still we should write a test to make sure that now, and in the future, the component has the elements we expect it to have. 

As we move into more dynamic components, such as those that query an API, wait for the data to be returned and then show that data, our tests need to account for what is happening with the component at each step. 

When working with React, the testing framework is included when we initialize our app with `npm create-react-app app-name`. This framework is called [Testing Library](https://testing-library.com/) and it is built on top of [Jest](https://jestjs.io/).

Let's go ahead and test our first component. We will largely follow a [Test Driven Development](https://www.guru99.com/test-driven-development.html) methodology when leaning to test.

1. Create a new React Application

    In your terminal enter: `npm create-react-app learning-to-test`

2. Testing is Built In

    Run `npm test` and voila, just like that you will run your first test and see it pass. 

    Go ahead and open `src/App.test.js`. You'll see code like this:
    
    ```

    import { render, screen } from '@testing-library/react';
    import App from './App';

    test('renders learn react link', () => {
        render(<App />);
        const linkElement = screen.getByText(/learn react/i);
        expect(linkElement).toBeInTheDocument();
    });

    ```

    Let's breakdown what is happening with this code: 
    
    ` import { render, screen } from '@testing-library/react';`

    We are importing the testing library methods that we'll use.

    `import App from './App';`

    We then import the component that we plan to test. 

    ```
    test('renders learn react link', () => {
       ...
    });
    ```


