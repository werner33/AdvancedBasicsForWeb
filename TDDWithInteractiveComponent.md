# Testing an Interactive Component

So far we've looked at the basic react app out of the box, then we moved on to testing a custom component. In this section, let's move into testing a component that has some interactivity. In the last section we'll include interactivity. 

1. Create a new Directory for a Counter

    You already know the drill: in the same project create a new directory called `/counter`. Like last time, let's start with the nested folder called `__test__`. And of course next well create our test file called `Counter.test.js`. 

    As with last time, we'll start by just writing a test to make sure our component renders properly, however, this time we will integrate one more Jest function, `describe`:

    ``` javascript
    import { render, screen } from '@testing-library/react';
    import Counter from '.././Counter';
    
    describe('the counter has a button to increment the count by one each time its clicked', () => {

        test('renders Counter', () => {
            render(<Counter />);
        });

    })

    ```
    Not much has changed here - we've simply wrapped our test function inside a describe function. This can be useful for grouping certain tests together and prefacing them with a general message describing our component. 

    Follow the same steps as last time to get this test to pass. 

2. Write Tests for the Static Elements

    We want our component to have two parts: a presentation for the current count, with a testid of 'counter__display', starting at 0 and a button with some text that says 'click me'. On every click, the counter should increment by one. 

    So first, use your knowledge from the previous lesson to write tests making sure the component has a '0' when it loads and a button with the text 'click me'. 

    You know what to do. If you feel stuck, check the [previous lesson for clues](https://github.com/werner33/AdvancedBasicsForWeb/blob/main/TDDWithTestingLibrary.md). 

3. Introducing Interactivity

    Now that we have the tests inplace for the static elements lets look at how to mock events like a user clicking on the button. 

    Lets grab the button by its text, click it one time, then check that the counter is displaying 1.

    ``` javascript
        ...
         describe('the counter has a button to increment the count by one each time its clicked', () => {

            ...

            test('counter increments by one when button is clicked' , () => {
                const {getByText, getByTestId} = render(<Counter />);

                getByText('click me').click();

                expect(getByTestId('counter__display')).toHaveTextContent('1')
            })

        })
    ```

    Modify the component to make this test pass. 

4. One Last Test

    Given that we want our clicker to be able to increment several times, lets add a test similar to the last, but click the button three times and check that the display is equal to 3. 

    ``` javascript
     test('counter increments by one when button is clicked' , () => {
        const {getByText, getByTestId} = render(<Counter />);

        getByText('click me').click();
        getByText('click me').click();
        getByText('click me').click();

        expect(getByTestId('counter__display')).toHaveTextContent('3')
    })
    ```

    That one should pass right away. 

5. Conclusion 

    If you would like to learn more about how to simulate interactivity in testing your components, testing library you can check out [Firing Events](https://testing-library.com/docs/dom-testing-library/api-events/).

    We've now looked at testing a static component and a dynamic but syncronous component. We'll now move onto [testing an asyncronous component](https://github.com/werner33/AdvancedBasicsForWeb/blob/main/TestingAnAsyncrounousComponent.md). 
