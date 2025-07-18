I’ll divide it like this:

| **Level**     | **Category**                       | **Type of Questions**                                |
| ------------- | ---------------------------------- | ---------------------------------------------------- |
| Basic         | Core Concepts                      | Syntax, Components, JSX, State, Props                |
| Intermediate  | React Hooks                        | useState, useEffect, useRef, useMemo, useCallback    |
| Advanced      | Performance Optimization           | Memoization, Lazy Loading, Splitting, Reconciliation |
| Practical     | Project/Scenario-Based Questions   | Real-world examples, debugging, scaling              |
| Architectural | State Management, Folder Structure | Context, Redux, RTK, Project Design                  |
| Integration   | API Handling & Forms               | Fetch, Axios, Error handling, Forms (Formik, RHF)    |
| Testing       | React Testing                      | Testing Library, Jest, Integration tests             |
 

---

Now here’s the **full list** you asked:

---

# **✨ Core React (Basics - 20 Questions)**

1. What is JSX? Why do we use it?
    
2. Difference between a functional and a class component?
    
3. What are props? How are they different from state?
    
4. How does state work in a React component?
    
5. Explain component lifecycle in class components.
    
6. What is the purpose of keys in React lists?
    
7. Why must React components return a single parent element?
    
8. How would you create a controlled vs uncontrolled input field?
    
9. How does conditional rendering work in React?
    
10. How does React handle events (like onClick)? How is it different from vanilla JS?
    
11. How do you pass data from parent to child?
    
12. How do you lift state up in React?
    
13. What are fragments in React? Why use them?
    
14. How would you dynamically render a list of items?
    
15. What happens if you update the state directly instead of using setState()?
    
16. What is the Virtual DOM and how does React use it?
    
17. Difference between component composition vs inheritance?
    
18. How does error boundary work?
    
19. What are defaultProps and propTypes?
    
20. How would you optimize re-renders at a basic level?
    

---

# **⚡ React Hooks (Intermediate - 20 Questions)**

1. What is the useState hook? How does it work internally?
    
2. Explain useEffect. What are its common use cases?
    
3. What’s the dependency array in useEffect? What happens if you skip it?
    
4. Explain how useRef is used.
    
5. Difference between useRef and createRef?
    
6. Why do we use useMemo? Give an example.
    
7. What is useCallback and why would you need it?
    
8. Can you call hooks conditionally inside components?
    
9. Custom hooks — what are they and when would you create one?
    
10. Explain the rules of hooks.
    
11. What is a stale closure problem in React hooks? How to fix it?
    
12. How would you debounce an input field using hooks?
    
13. How does useReducer differ from useState?
    
14. How would you share logic across multiple components?
    
15. How would you fetch API data inside a hook safely?
    
16. Can you trigger an effect only when a specific prop changes?
    
17. How does useLayoutEffect differ from useEffect?
    
18. Can you use async/await inside useEffect? How?
    
19. Explain dependency array pitfalls with objects and arrays.
    
20. How would you write a custom hook to detect if a user is online/offline?
    

---

# **🔥 Performance Optimization (Advanced - 20 Questions)**

1. How do you prevent unnecessary re-renders in React?
    
2. What is React.memo and when should you use it?
    
3. How does PureComponent help?
    
4. How would you lazy-load a component?
    
5. What is code splitting? How to implement it in React?
    
6. How does React Suspense work?
    
7. What is reconciliation? Explain in detail.
    
8. How can you optimize performance for a huge list (10k+ items)?
    
9. When would you use windowing (react-window or react-virtualized)?
    
10. How would you measure performance in a React app?
    
11. How does useTransition from React 18 help?
    
12. What are concurrent features in React 18?
    
13. What is hydration in React?
    
14. How does server-side rendering (SSR) help performance?
    
15. How would you cache API responses inside a React component?
    
16. How would you throttle or debounce expensive functions in React?
    
17. How do you prevent unnecessary API calls with hooks?
    
18. How would you optimize image loading in React apps?
    
19. What are render props? Why are they performance heavy sometimes?
    
20. What are the main causes of memory leaks in React?
    

---

# **🛠️ Project / Scenario-Based (Real-world - 20 Questions)**

1. How would you structure a large React project?
    
2. How do you handle loading states globally?
    
3. Suppose a button click triggers 3 API calls, how do you manage it?
    
4. How would you create a reusable table component?
    
5. How would you handle role-based authentication in a React app?
    
6. How would you make a dynamic multi-step form?
    
7. How do you debug a slow React app?
    
8. If a form is freezing while typing, what could be wrong?
    
9. How would you implement a dark/light theme toggle?
    
10. Suppose a user leaves a form mid-way — how would you save the progress?
    
11. How would you implement infinite scroll in a React app?
    
12. How would you handle file uploads in a React form?
    
13. If a user submits a form and closes the page mid-submit, how would you prevent data loss?
    
14. How would you show a notification/toast system globally?
    
15. How would you create a dynamic dashboard layout?
    
16. Suppose a React app’s bundle is 8MB — how would you reduce it?
    
17. How would you design a component library for your organization?
    
18. How would you detect and show if a user’s connection is slow?
    
19. What’s your strategy if you need to migrate a Class component project to Hooks?
    
20. How would you secure your React frontend against XSS attacks?
    

---

# **🏛️ State Management + Folder Structure (Advanced)**

1. What are the different ways to manage state in React?
    
2. What is Context API? How is it used?
    
3. When should you use Redux instead of Context?
    
4. Difference between Redux Toolkit (RTK) and vanilla Redux?
    
5. How would you structure Redux slices for a large app?
    
6. How does Redux persist data across refreshes?
    
7. What is thunk middleware in Redux?
    
8. What is the difference between thunk and saga?
    
9. What is Recoil? How is it different from Redux?
    
10. How would you optimize Context API usage to avoid prop drilling?
    
11. How would you create a global error handler with Context API?
    
12. Folder structure best practices for React apps?
    
13. How do you manage feature modules inside a React project?
    
14. What is a service layer pattern? Why would you use it?
    
15. Where would you put constants, utilities, and services?
    
16. What is the container-presentational pattern?
    
17. How would you organize tests inside a project?
    
18. How do you modularize API calls?
    
19. How would you handle environment variables in React?
    
20. How would you differentiate between business logic and UI logic?
    

---

# **🌐 API Handling + Forms (Intermediate)**

1. How do you handle API calls in React apps?
    
2. How would you cancel an API call if the component unmounts?
    
3. Difference between Fetch and Axios?
    
4. How would you globally manage API errors?
    
5. How would you retry a failed API call automatically?
    
6. How would you design a dynamic form in React?
    
7. Difference between Formik and React Hook Form?
    
8. How would you validate fields with Formik?
    
9. How would you show backend validation errors on a form?
    
10. How do you disable a submit button while submitting a form?
    
11. How would you auto-save form data every 10 seconds?
    
12. How would you upload a file using a form in React?
    
13. How do you show a progress bar for a file upload?
    
14. How would you handle authentication tokens in API requests?
    
15. How would you refresh a token automatically?
    
16. How would you handle cascading dropdowns in a form?
    
17. How would you fetch dependent dropdown options from an API?
    
18. How would you debounce search inputs that query an API?
    
19. How would you bulk upload data through a form?
    
20. How would you prevent double submissions on a form?
    

---

# **🧪 Testing React Components (Advanced Basics)**

1. How do you test a React component using React Testing Library?
    
2. What is the difference between shallow render and full render?
    
3. How do you test a button click event?
    
4. How would you mock an API call in a test?
    
5. How do you test form validation errors?
    
6. How do you simulate a user typing into an input field?
    
7. What is jest.fn() and why is it used?
    
8. How would you test a component that uses useEffect?
    
9. How would you test context API providers?
    
10. How would you test Redux store-connected components?
    
11. How would you test route changes (React Router)?
    
12. How do you test custom hooks?
    
13. How would you mock window.localStorage in tests?
    
14. How would you mock timers (setTimeout) inside tests?
    
15. How do you test lazy-loaded components?
    
16. What is snapshot testing? What are its pros and cons?
    
17. How would you organize your tests in a large app?
    
18. How would you set up test coverage thresholds?
    
19. How would you handle flaky tests in React?
    
20. What are the best practices for writing maintainable React tests?
    

---

# **⚡ Summary for you:**

  

If you practice these **140 questions** deeply (with code examples where needed + project experiences), **even a beginner can survive a 6+ years senior React interview**.

---

