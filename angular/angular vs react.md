### **🔹 In Angular:**

A **Component** is a TypeScript class + template + metadata that controls a patch of the UI.


### **🔹 In React:**

A **Component** is a JavaScript/TypeScript function or class that returns JSX to render UI.



| **Feature**               | **Angular**                           | **React**                               |
| ------------------------- | ------------------------------------- | --------------------------------------- |
| Language                  | TypeScript + HTML templates           | JSX (JavaScript + XML)                  |
| Component Declaration     | Decorators (@Component)               | Function or Class                       |
| Rendering Mechanism       | Template compiled to JS at build time | JSX compiled to JS at runtime           |
| Change Detection          | Zone.js + full tree change detection  | Fine-grained via virtual DOM diffing    |
| State Management          | Inputs, Services, RxJS, NgRx          | useState, useReducer, Redux, Context    |
| Dependency Injection      | Built-in, hierarchical                | Not built-in (manual via props/context) |
| Routing                   | Angular Router                        | React Router (separate package)         |
| Component Style Isolation | Scoped via ViewEncapsulation          | CSS Modules or Styled Components        |
| Lifecycle Hooks           | ngOnInit, ngOnChanges, ngDestroy…     | useEffect, componentDidMount…           |