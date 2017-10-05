# Meteor dynamic `import(...)` bug when using dynamic imports inside of a Meteor package

How to reproduce the bug: 

1. Start the app normally (with `npm start`) – the unminimized bundle size should be around 1MB
2. In the file `Task.jsx` in the `heavy` package, comment out the following lines: 

```
    // Uncommenting these three lines imports all of the dependencies of HeavyComponent

    // if (2===3) {
    //   import('./HeavyComponent.jsx');
    // }
```

Clearly that import statement should never be run. 

3. Start the app again 

The unminimized bundle size is now around 2.3MB, and you can clearly see that the imports from the `HeavyComponent.jsx` file have been imported into the client bundle. 

When you run practically the same code outside of a package (i.e. in an `imports` folder in the main folder), then this behavior does not occur, and the imports from `HeavyComponent.jsx` only get imported if the `import(./HeavyComponent.jsx)` statement is programmatically reached
