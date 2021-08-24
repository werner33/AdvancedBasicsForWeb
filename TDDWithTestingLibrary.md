# Test Driven Development with Testing Library

We worked with the provided test folder and test that comes built into a `create-react-app` project. Now, we will delete those starter tests and write tests for a custom component. 

To that end, please delete `App.test.js` and go ahead and delete all the boiler plate jsx in App.js. 

We will start by building an InfoCard component that will included a title and small block of text. This will be a static component with no user interaction. 

1. Create Directory to Hold Component and Tests

    Create a new directory called infoCard. 

    Inside this directory, create a second directory called `__test__`. This is the folder that will hold our test suite. Go ahead and create a file inside `/__test__` called InfoCard.test.js. 

    We Should have a file structure that looks like this:
    .
    +-- src
    |   +-- infoCard
            +-- __test__
                +-- InfoCard.test.js

