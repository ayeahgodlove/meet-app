# Test-driven and Behavior-driven Development

## Unit Testing with React and Jest

For your project, you’ll be using a test runner called Jest to conduct your tests. Jest is included by default in create-react-app

In unit testing, each test focuses on a single unit of code. A “unit,” in this case, is a function:

```
//simple unit test in Jest
test('test description', () => {
    expect(someFunc()).toBe(someValue);
})
```

The `expect()` is where you place the function you want to test, and the `toBe()` is the matcher, condition for passed, or failed test

**Creating multiple test cases)**

```
test('render Event component with correct name', () => {
  expect(Event.find('.name').text()).toBe(Events in Berlin');
});

test('render Event component with correct time', () => {
  expect(Event.find('.time').text()).toBe('14:00');
});
```

**_NOTE:_**
One of the above tests may interact with the `Event` component thus changing it's state or props, any subsequent test in your suite may no longer be correct as the state or props will change. For this reason, you should reset the `Event` component every time you conduct a test, giving it a blank state from which to start.

You use the `beforeEach()` and `afterEach()` functions. Any code you include in a `beforeEach()` function will be executed before each and every test you run likewise `afterEach()` which is the code executed aftereach test.

**NB**

- You could use this functionsto initialize and subsequently clear the state and props before and after eact test.

```
beforeEach(() => {
  initEventStateAndProps();
});

afterEach(() => {
  clearEventStateAndProps();
});

test('render Event component with correct name', () => {
  expect(Event.find('.name').text()).toBe(Events in Berlin');
});

test('render Event component with correct time', () => {
  expect(Event.find('.time').text()).toBe('14:00');
});
```

- However, when you only need to do something once before all of your tests, there's a function for this too. introducing Jest's `beforeAll()` and `afterAll()`

```
    beforeAll(() => {
        mountEventComponent();
    });

    afterAll(() => {
        unmountEventComponent();
    });

    test('render Event component with correct name', () => {
        expect(Event.find('.name').text()).toBe(Events in Berlin');
    });

    test('render Event component with correct time', () => {
        expect(Event.find('.time').text()).toBe('14:00');
    });
```

> The `beforeAll()`, `afterAll()`, `beforeEach()`, and `afterEach()` functions are a convenient way to perform the same actions on multiple tests within your test suite; however, you'll also find times where you only want to perform actions a=on certain tests within the suite. For example, say you want to test the props and state of a React component separately. To do so, _you'd want to group all props-testing test together in one group and all state-testing tests together in another group_

> Jest provides the `describe()` funtion for this purpose. With the `describe()`, you can combine multiple tests into one group called a **_SCOPE_**, then use the `beforeAll()`, `afterAll()`, `beforeEach()` and `afterEach()` functions only on tests withing that group.

_Examples_

```
//test with state
describe('test Event state', () => {
  beforeAll(() => {
    mountEventWithState();
  });

  afterAll(() => {
    unmountEvent();
  });

  beforeEach(() => {
    initEventState();
  });

  afterEach(() => {
    clearEventState();
  });


  test('description 1', () => { some code });
  test('description 2', () => { some code });

});
```

```
//test with props
describe('test Event props', () => {
  beforeAll(() => {
    mountEventWithProps();
  });

  afterAll(() => {
    unmountEvent();
  });

  beforeEach(() => {
      initEventProps();
    });

    afterEach(() => {
      clearEventProps();
    });


    test('description 1', () => { some code });
    test('description 2', () => { some code });

  });
```
***Here are five functions to help organize and manage the test cases within your suite***
1. `beforeAll()`: called once before every test case within a scope
2. `afterAll()`: called once after every test case within a scope
3. `beforeEach()`: called before each test case within a scope but after
4. `afterEach()`: called after each test within a scope and before afterAll()
5. `describe()`: groups tests into scopes

