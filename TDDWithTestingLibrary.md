# Test Driven Development with Testing Library

We worked with the provided test folder and test that comes built into a `create-react-app` project. Now, we will delete those starter tests and write tests for a custom component. 

To that end, please delete `App.test.js` and go ahead and delete all the boiler plate jsx in App.js. 

We will start by building an InfoCard component that will included a title and small block of text. This will be a static component with no user interaction. 

1. Create Directory to Hold Component and Tests

    Create a new directory called infoCard. 

    Inside this directory, create a second directory called `__test__`. This is the folder that will hold our test suite. Go ahead and create a file inside `/__test__` called InfoCard.test.js. 

    We Should have a file structure that looks like this:
    <pre>
    .
    +-- src
    |   +-- infoCard
            +-- __test__
                +-- InfoCard.test.js
    </pre>

2. Let's Write Our First Test

    Open `InfoCard.test.js`. Let's follow the example of our previous code and write our first test just to test if the component is rendering properly. 

    ```
    import { render, screen } from '@testing-library/react';
    import InfoCard from '.././InfoCard';

    test('renders InfoCard', () => {
        render(<InfoCard />);
    });

    ```

    We know we haven't even set up our component yet, so we expect this test to fail. 

    And here it is: 

    ```

        1 | import { render, screen } from '@testing-library/react';
      > 2 | import InfoCard from '.././InfoCard';
          | ^
        3 |
        4 | test('renders InfoCard', () => {
        5 |     render(<InfoCard />);
    ```

    Notice the carrot pointing to where this test has stopped. It can't import InfoCard because we haven't created it yet. Lets do that. 

3. Create `InfoCard`

    Let's create InfoCard and run the test again. It fails again, but we see the pointers have moved down to line that says `render(<InfoCard />)`. 

4. Let's Write the Barebones of the InfoCard

    Inside InfoCard.js add:

    ```
        import React from 'react';

        function InfoCard(props) {
            return (
                <div>
                    
                </div>
            );
        }

        export default InfoCard;
    ```

    If you haven't stopped your test, you'll see that the test runs automatically and now, it passes! 

    ```
     PASS  src/components/infoCard/__test__/InfoCard.test.js
        ✓ renders InfoCard (15 ms)

    Test Suites: 1 passed, 1 total
    Tests:       1 passed, 1 total
    Snapshots:   0 total
    Time:        1.527 s
    Ran all test suites related to changed files.

    Watch Usage: Press w to show more.
    ```

    As soon as we have a passing test, it's time to write a new test! 

5. Write a Test for the Card Title

    Until now, we have checked that a component renders properly or we've checked for specific test on the screen. With our info card, we want to be able to pass the title and body text as props when the component is first rendered. Let's make sure we check for both the element that will hold the text as well as the text itself. 

    When we want to target a specific element, we have the option of using `data-testid` as a property on our html element.

    Write a second test like this: 

    ```
    test('it has an element to hold the title text', () => {
        const {getByTestId} = render(<InfoCard />);
        expect(getByTestId('infoCard__title')).toBeInTheDocument();
    })
    ```

    And of course, that will fail! Always exciting. Notice that the failing test is telling us exactly what we need to do next. 

6. Add an Element with data-testid 

    We return to our InfoCard component and we'll add a `h3` element with the data-testid property.

    ```
        ...
        return (
                    <div>
                       <h3 data-testid="infoCard__title> 
                    </div>
                );
           
    ```

    As soon as you save that code, you should see the tests re-run and pass. 

7. Test for Specific Text
    We want to pass a title prop into our Info Card component with some text. That text should then render inside of our H3 element. Let's write a test that describes that: 
    
    ```
        test('it renders the title text passed as a prop', () => {
            const {getByText} = render(<InfoCard title="Info Card Title">);
            expect(getByText('Info Card Title')).toBeInTheDocument();
        })
    ```

    Add a title prop to your conponent and render it inside the H3 element. 

8. Repeat both Tests for the Content Area 

    Follow the example of the previous two tests except this time, test for a data-testid of 'infoCard__content' and then test that the prop content takes some text and renders it in the component. 

    I'll leave this implementation to you. 

    Lastly, change your component such that all the tests pass. You should have five tests at this point. 

    Our test file should look like this <add link>

9. Conclusion

    We've written a nice test suite for this rather static component. One thing to keep in mind is that we should never delete tests that we've previously written unless the requirements for the component change or if we discover we made some mistake in writing our tests. Tests build on one another as a sort of scafolding to ensure that the component does everything we expect it to do. 


    
 
    

