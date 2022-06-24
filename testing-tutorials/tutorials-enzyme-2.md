# Shallow Rendering with Enzyme

> Here, _“shallow rendering”_ simply refers to a _“light”_ rendering of your React components. Rather than using a complete DOM and fully rendering each one of your components and their children, as you’d need to actually get your app up and running, this API allows you to render them only _“one level deep”_—just enough for testing purposes.

**_Install Enzyme_**

> `npm install --save-dev enzyme`
> Then run `npm -v` to check which version of npm you have:

- if you have a higher version installed, run `npm install --save-dev --legacy-peer-deps @wojtekmaj/enzyme-adapter-react-17`
- if not run `npm install --save-dev @wojtekmaj/enzyme-adapter-react-17`
