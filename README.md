# React Jest Testing
By using create react app you should already have all the required libraries for ject testing. Jest testing is component testing and not end to end testing. So we will test one component at a time. This means you will have one test file for every component you have. For runnnig tests you will end up using the command: 
```*.sh-session 
$ yarn test
``` 
Before you run this command check to make sure you have the following dependencies and script in your package.json, notice the addition of a couple of flags to the test script. The watchAll flag is to turn off watch which keeps the test script running. The second flag is to turn on coverage reports so you can monitor your testing on the components.
```json
{
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "react-scripts": "5.0.1",
  },
  "scripts": {
    "test": "react-scripts test --watchAll=false --coverage",
  }
}

```
in your command line. You might already have a couple of random tests and thats fine if you do, but we should organize this. If you have existing tests in there, you need to move them. In the ```src``` folder create a new folder called ```__test__```. Your folder structure should be something like this:
```
├── src
│   ├── __test__
│   ├── App.jsx
│   ├── index.js
├── public
├── node_modules
├── package.json
├── package-lock.json 
```
All of you jest tests should live in the ```__test__``` folder and the folders structure should match the structure of your source to make it easier to find tests. For jest testing you will be testing all your code. I would suggest the use of snapshots to see if code has changed and so you can see outputs. So a simple test for a basic component with snapshots would go as follows:
```javascript
import React from 'react';
import App from '../App';
import {render} from '@testing-library/react';
import userEvent from '@testing-library/user-event';

describe("Suite to test App component", ()=>{
    test('Snapshot of Body', () => {
        // import the App component and pass it title as a prop
        const {asFragment} = render(<App title="hello world"/>);
        // once imported it generates and matches the snapshot to the test.
        expect(asFragment()).toMatchSnapshot()
    });    
})
```
When testing with snapshots you will first need to generate them. Use the ```-u``` flag for this. Everytime you update the code and or update the test case you will need to use that flag to update the snapshot or the test will fail.
```*.sh-session 
$ yarn test -u
```
I cannot possibly cover all the testing scenarios here for your specific needs, but you might end up having to test hooks, lifecycle components, API calls, etc. The documentation for testing some of these different objects can be found with the product used [React Testing Library](https://testing-library.com/docs/react-testing-library/api).

---
# Node + Express Jest Testing

