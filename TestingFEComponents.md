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

    Here we see the primary building block of testing. We have a function called `test` that takes two arguments: 
       
        1. A human readable message describing what the test is looking for. Here we have the message 'renders react link'.

        2. A call back function that usually starts by setting up the component and checking some expectation of that component.

    ```
        test('renders learn react link', () => {
            render(<App />);
            const linkElement = screen.getByText(/learn react/i);
            expect(linkElement).toBeInTheDocument();
        });
    ```

    Finally, we look at the content of the callback function. First we render the component. Then, we set a variable called `linkElement` and we grab this element by searching the 'screen' for the text 'learn react'.
    On the last line, we complete the test with our `expect` function. Expect takes one argument that is some element we want to target. Then we use one of several methods, `toBeInTheDocument()`, in this case to express what we expect.

    So if we were to translate this to plain english we might say: 
    "Go ahead and render the App component. Search that component for an element that includes the text 'learn react' and give it a name of `linkElement`. At last, check to make sure that the element is in the component that we rendered. 

3. Let's Write a New Test

    Inside the same test file, let's add a new test. Given that we are now following Test Driven Development (TDD), we expect this test to fail after we write it. 

    Add this to the end of `src/App.test.js`: 

    ```
        test('renders learn react link', () => {
            render(<App />);
            const linkElement = screen.getByText(/Hello Friend/i);
            expect(linkElement).toBeInTheDocument();
        });
    ```

    After you have added this, go ahead and run `npm test`. 

    You should see something like this: 

    ```
    Test Suites: 1 failed, 1 total
    Tests:       1 failed, 1 passed, 2 total
    Snapshots:   0 total
    Time:        3.786 s
    Ran all test suites related to changed files.

    Watch Usage
    › Press a to run all tests.
    › Press f to run only failed tests.
    › Press q to quit watch mode.
    › Press p to filter by a filename regex pattern.
    › Press t to filter by a test name regex pattern.
    › Press Enter to trigger a test run.
    ```
    


