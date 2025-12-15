# React Interview Questions - Complete Guide

Based on the React Developer Roadmap from [roadmap.sh](https://roadmap.sh/react), this document covers interview questions for all topics in the React ecosystem.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [React Basics](#react-basics)
3. [React Hooks](#react-hooks)
4. [State Management](#state-management)
5. [Routing](#routing)
6. [Forms and Validation](#forms-and-validation)
7. [Styling](#styling)
8. [Performance Optimization](#performance-optimization)
9. [Testing](#testing)
10. [TypeScript with React](#typescript-with-react)
11. [Next.js](#nextjs)
12. [Build Tools](#build-tools)
13. [Authentication & Security](#authentication--security)
14. [API Integration](#api-integration)
15. [Advanced Patterns](#advanced-patterns)
16. [Error Handling](#error-handling)
17. [Accessibility](#accessibility)
18. [Deployment](#deployment)

---

## Prerequisites

### HTML & CSS

1. **What is the difference between semantic and non-semantic HTML elements?**

**Answer:** Semantic HTML elements clearly describe their meaning in a human- and machine-readable way (e.g., `<header>`, `<nav>`, `<article>`, `<section>`, `<footer>`). Non-semantic elements like `<div>` and `<span>` don't convey meaning about their content. Semantic HTML improves accessibility, SEO, and code maintainability.

2. **Explain CSS Box Model and its components.**

**Answer:** The CSS Box Model describes how elements are rendered as rectangular boxes. It consists of four parts: content (the actual content), padding (space between content and border), border (the border around padding), and margin (space outside the border). The total width/height = content + padding + border + margin.

3. **What are CSS Flexbox and Grid, and when would you use each?**

**Answer:** Flexbox is a one-dimensional layout system (row or column) ideal for component-level layouts, aligning items, and distributing space. CSS Grid is a two-dimensional layout system (rows and columns) ideal for page-level layouts and complex grid structures. Use Flexbox for navigation bars, card layouts, and centering. Use Grid for overall page layouts, complex designs, and when you need both row and column control.

4. **What is CSS specificity and how does it work?**

**Answer:** CSS specificity determines which CSS rule is applied when multiple rules target the same element. It's calculated using a scoring system: inline styles (1000), IDs (100), classes/attributes/pseudo-classes (10), and elements/pseudo-elements (1). Higher specificity wins. When specificity is equal, the last rule in the stylesheet wins.

5. **Explain the difference between `display: block`, `display: inline`, and `display: inline-block`.**

**Answer:** `display: block` elements take full width, start on a new line, and can have width/height set (e.g., `<div>`, `<p>`). `display: inline` elements only take necessary width, don't start new lines, and can't have width/height set (e.g., `<span>`, `<a>`). `display: inline-block` combines both: elements stay inline but can have width/height set.

6. **What are CSS variables (custom properties) and how are they useful?**

**Answer:** CSS variables (custom properties) are values defined with `--variable-name` that can be reused throughout stylesheets. They're defined in `:root` for global scope or in specific selectors for local scope, and accessed with `var(--variable-name)`. They enable theming, easier maintenance, and dynamic styling via JavaScript.

7. **What is the difference between `margin` and `padding`?**

**Answer:** `padding` is the space inside an element, between the content and the border. `margin` is the space outside an element, between the border and adjacent elements. Padding affects the element's background, while margin doesn't. Negative values are allowed for margin but not padding.

8. **Explain CSS media queries and responsive design principles.**

**Answer:** Media queries allow CSS to apply styles based on device characteristics (screen size, resolution, orientation). They use `@media` syntax with breakpoints. Responsive design principles include mobile-first approach, flexible layouts (using relative units), flexible images, and breakpoints for different screen sizes (typically 768px, 1024px, etc.).

### JavaScript Fundamentals

9. **What are closures in JavaScript, and how are they used in React?**

**Answer:** Closures allow inner functions to access variables from their outer (enclosing) scope even after the outer function has returned. In React, closures are used in event handlers, `useEffect` hooks, and callbacks to maintain access to component state and props. For example, event handlers often form closures over component state.

10. **Explain the concept of prototypal inheritance in JavaScript.**

**Answer:** Prototypal inheritance is JavaScript's mechanism where objects inherit properties and methods from other objects through a prototype chain. Every object has a prototype, and when a property isn't found on an object, JavaScript looks up the prototype chain. This differs from class-based inheritance in languages like Java.

11. **What is the difference between `null` and `undefined`?**

**Answer:** `undefined` means a variable has been declared but not assigned a value, or a property doesn't exist. `null` is an intentional absence of value (explicitly set). `typeof null` returns `"object"` (a JavaScript bug), while `typeof undefined` returns `"undefined"`. Both are falsy values.

12. **Explain the difference between `var`, `let`, and `const`.**

**Answer:** `var` is function-scoped, hoisted, and can be redeclared. `let` and `const` are block-scoped and cannot be redeclared. `let` allows reassignment, while `const` doesn't (though objects/arrays can be mutated). `let` and `const` are not hoisted in the same way as `var` (temporal dead zone).

13. **What are promises and async/await? How do they differ from callbacks?**

**Answer:** Promises represent eventual completion of an async operation with `.then()` and `.catch()`. `async/await` is syntactic sugar over promises, making async code look synchronous. Callbacks are functions passed as arguments, leading to "callback hell." Promises and async/await provide better error handling and avoid deeply nested code.

14. **What is the event loop in JavaScript?**

**Answer:** The event loop is JavaScript's mechanism for handling asynchronous operations. It continuously checks the call stack and message queue. When the call stack is empty, it moves tasks from the queue to the stack. This allows non-blocking I/O operations and enables JavaScript's single-threaded, asynchronous nature.

15. **Explain `this` keyword in JavaScript and its behavior in different contexts.**

**Answer:** `this` refers to the execution context. In global scope, it's `window` (browser) or `global` (Node). In methods, it's the object calling the method. In arrow functions, `this` is lexically bound (from enclosing scope). In constructors, it's the new instance. `call()`, `apply()`, and `bind()` can explicitly set `this`.

16. **What are arrow functions and how do they differ from regular functions?**

**Answer:** Arrow functions (`() => {}`) have shorter syntax, don't have their own `this` (lexically bound), don't have `arguments` object, can't be used as constructors, and can't be hoisted. Regular functions have their own `this`, have `arguments`, can be constructors, and are hoisted.

17. **Explain destructuring assignment in JavaScript.**

**Answer:** Destructuring extracts values from arrays or properties from objects into distinct variables. Examples: `const [a, b] = [1, 2]` or `const {name, age} = person`. It supports default values, rest elements, and nested destructuring. Commonly used in React for props and state.

18. **What are template literals and when would you use them?**

**Answer:** Template literals use backticks (`` ` ``) and allow embedded expressions via `${expression}`. They support multi-line strings and string interpolation. Use them for dynamic strings, multi-line text, and when you need to embed variables/expressions in strings.

19. **Explain the spread operator and rest parameters.**

**Answer:** The spread operator (`...`) expands iterables (arrays, objects) into individual elements. Rest parameters (`...args`) collect remaining arguments into an array. Examples: `[...arr1, ...arr2]` (combine arrays), `{...obj1, ...obj2}` (merge objects), `function(...args)` (collect arguments).

20. **What is hoisting in JavaScript?**

**Answer:** Hoisting moves variable and function declarations to the top of their scope during compilation. `var` declarations are hoisted and initialized with `undefined`. `let` and `const` are hoisted but not initialized (temporal dead zone). Function declarations are fully hoisted, while function expressions are not.

21. **Explain the difference between `==` and `===`.**

**Answer:** `==` (loose equality) performs type coercion before comparison. `===` (strict equality) checks both value and type without coercion. Always prefer `===` to avoid unexpected type conversions. Example: `"5" == 5` is `true`, but `"5" === 5` is `false`.

22. **What are higher-order functions? Give examples.**

**Answer:** Higher-order functions are functions that take other functions as arguments or return functions. Examples: `map()`, `filter()`, `reduce()`, `forEach()`, `setTimeout()`, `addEventListener()`. They enable functional programming patterns and code reusability.

23. **Explain `map`, `filter`, and `reduce` array methods.**

**Answer:** `map()` transforms each element and returns a new array of the same length. `filter()` returns a new array with elements that pass a test. `reduce()` accumulates values into a single result. All are non-mutating and commonly used in React for transforming data.

24. **What is the difference between `call`, `apply`, and `bind`?**

**Answer:** All three set `this` context. `call()` invokes immediately with individual arguments. `apply()` invokes immediately with an array of arguments. `bind()` returns a new function with bound `this` and optional arguments, without immediate invocation. Example: `func.call(obj, 1, 2)`, `func.apply(obj, [1, 2])`, `const bound = func.bind(obj)`.

---

## React Basics

### JSX

25. **What is JSX, and why is it used in React?**

**Answer:** JSX (JavaScript XML) is a syntax extension that allows writing HTML-like code in JavaScript. It's transpiled to `React.createElement()` calls. JSX makes React code more readable, provides syntax highlighting, and catches errors at compile time. It's not required but is the recommended way to write React components.

26. **Can you write React without JSX?**

**Answer:** Yes, React can be written without JSX using `React.createElement()`. However, JSX is more readable and maintainable. Example: `React.createElement('div', {className: 'container'}, 'Hello')` vs `<div className="container">Hello</div>`.

27. **What are the rules of JSX?**

**Answer:** JSX rules include: must return a single root element (or Fragment), use `className` instead of `class`, use `htmlFor` instead of `for`, self-closing tags must have `/`, use camelCase for attributes, and JavaScript expressions must be wrapped in `{}`.

28. **How do you write comments in JSX?**

**Answer:** Comments in JSX use `{/* comment */}` syntax. Regular JavaScript comments (`//` or `/* */`) don't work inside JSX expressions. Example: `{/* This is a comment */}`.

29. **What is the difference between JSX and HTML?**

**Answer:** JSX is JavaScript, HTML is markup. Key differences: JSX uses camelCase attributes (`onClick`, `className`), requires closing tags, uses `{}` for JavaScript expressions, and must return a single root element. HTML uses lowercase attributes, allows self-closing tags, and doesn't support embedded JavaScript.

30. **How do you embed JavaScript expressions in JSX?**

**Answer:** JavaScript expressions are embedded using curly braces `{}`. You can use variables, function calls, ternary operators, and any valid JavaScript expression. Example: `<h1>{name}</h1>` or `<p>{isLoggedIn ? 'Welcome' : 'Please login'}</p>`.

### Components

31. **What is a React component?**

**Answer:** A React component is a reusable piece of UI that encapsulates its own structure, logic, and styling. Components can be functions or classes that return JSX. They accept props as input and can maintain internal state. Components enable code reusability and modularity.

32. **Explain the difference between functional and class components.**

**Answer:** Functional components are JavaScript functions that return JSX. Class components are ES6 classes extending `React.Component`. Functional components use Hooks for state and lifecycle, while class components use `this.state` and lifecycle methods. Functional components are now preferred and simpler.

33. **What are the advantages of functional components over class components?**

**Answer:** Advantages include: simpler syntax, easier to test, better performance (no `this` binding), easier to understand, better tree-shaking, and Hooks provide all functionality. Functional components are the recommended approach in modern React.

34. **What is a pure component in React?**

**Answer:** `React.PureComponent` (class) or `React.memo()` (functional) prevents re-renders when props/state haven't changed. Pure components perform shallow comparison. Use them for performance optimization when components receive the same props frequently.

35. **What are stateless and stateful components?**

**Answer:** Stateless components (presentational) don't manage state and only receive props. Stateful components (container) manage state using `useState` or `this.state`. Stateless components are simpler and easier to test, while stateful components handle logic and data.

36. **How do you create a component in React?**

**Answer:** Functional: `function Component(props) { return <div>...</div> }` or `const Component = (props) => <div>...</div>`. Class: `class Component extends React.Component { render() { return <div>...</div> } }`. Modern React prefers functional components with Hooks.

37. **What is component composition?**

**Answer:** Component composition is building complex UIs by combining smaller, reusable components. It's achieved by nesting components, using `children` prop, or passing components as props. Composition is preferred over inheritance in React.

38. **Explain the difference between container and presentational components.**

**Answer:** Container components (smart components) handle data fetching, state management, and business logic. Presentational components (dumb components) only handle UI rendering and receive data via props. This separation improves reusability and testability.

### Props

39. **What are props in React, and how are they used?**

**Answer:** Props (properties) are read-only data passed from parent to child components. They enable component communication and reusability. Props are accessed via the function parameter or `this.props` in class components. They should not be mutated by the receiving component.

40. **How do you pass props to a component?**

**Answer:** Props are passed as attributes in JSX: `<Component name="John" age={25} />`. String values use quotes, expressions use `{}`. Props are received as an object parameter: `function Component({ name, age })` or `function Component(props)`.

41. **What is the difference between props and state?**

**Answer:** Props are passed from parent to child and are immutable within the child. State is internal to a component and can be changed using `setState` or `useState`. Props flow down, state is managed locally. Changes to props cause re-renders, changes to state also cause re-renders.

42. **Can props be changed? Why or why not?**

**Answer:** No, props are read-only and should not be mutated. React follows unidirectional data flow: props flow down from parent to child. To change data, update state in the parent component, which will pass new props down. Mutating props breaks React's predictability.

43. **What are default props?**

**Answer:** Default props provide fallback values when props aren't passed. In functional components: `Component.defaultProps = { name: 'Guest' }` or using default parameters: `function Component({ name = 'Guest' })`. In class components: `Component.defaultProps = { name: 'Guest' }`.

44. **What is PropTypes and why is it useful?**

**Answer:** PropTypes validate the types of props at runtime in development. It helps catch bugs and documents component APIs. Example: `Component.propTypes = { name: PropTypes.string.isRequired }`. TypeScript is now preferred for type checking, but PropTypes remains useful for JavaScript projects.

45. **How do you pass children to a component?**

**Answer:** Children are passed between opening and closing tags: `<Component>Hello</Component>`. Access via `props.children` or destructure `{ children }`. Children can be strings, elements, arrays, or functions. Useful for layout components and composition patterns.

46. **What is the difference between props and children?**

**Answer:** Props are named attributes passed to components. `children` is a special prop containing content between component tags. All props including `children` are part of the props object, but `children` is commonly used for component composition and wrapper patterns.

### State

47. **What is state in React?**

**Answer:** State is data that belongs to a component and can change over time. When state changes, the component re-renders. State is managed using `useState` Hook in functional components or `this.state` in class components. State should be used for data that affects rendering.

48. **What is the difference between state and props?**

**Answer:** State is internal and mutable within a component. Props are external and immutable (passed from parent). State changes trigger re-renders of the component and its children (if passed as props). Props changes trigger re-renders of the receiving component.

49. **How do you update state in class components?**

**Answer:** Use `this.setState()` with an object or function: `this.setState({ count: this.state.count + 1 })` or `this.setState((prevState) => ({ count: prevState.count + 1 }))`. Never mutate `this.state` directly. `setState` is asynchronous and batches updates.

50. **What is the correct way to update state in React?**

**Answer:** For functional components: use the setter from `useState`: `setCount(count + 1)` or `setCount(prev => prev + 1)`. For class components: use `this.setState()`. Always use the updater function when new state depends on previous state. Never mutate state directly.

51. **Why should you not mutate state directly?**

**Answer:** Direct mutation doesn't trigger re-renders, breaks React's reconciliation algorithm, and can cause bugs. React uses reference equality to detect changes. Mutating objects/arrays directly means React won't detect the change. Always create new objects/arrays when updating state.

52. **What happens when you call `setState` in React?**

**Answer:** `setState` schedules a state update and component re-render. React batches multiple `setState` calls for performance. The update is asynchronous, so `this.state` may not reflect the new value immediately. React merges the update with existing state and triggers reconciliation.

53. **Explain the difference between synchronous and asynchronous state updates.**

**Answer:** State updates in React are asynchronous and batched for performance. `setState` and `useState` setters don't immediately update state. React batches updates and processes them together. Use functional updates (`setState(prev => ...)`) when new state depends on previous state to ensure correctness.

54. **What is the purpose of the callback function in `setState`?**

**Answer:** The callback in `setState(newState, callback)` executes after the state update and re-render complete. It's useful for side effects that depend on the updated state, like API calls or DOM manipulation. In functional components, use `useEffect` instead for this purpose.

### Event Handling

55. **How do you handle events in React?**

**Answer:** Events are handled using camelCase attributes: `onClick`, `onChange`, `onSubmit`. Pass a function reference: `<button onClick={handleClick}>`. In class components, bind methods or use arrow functions. React uses SyntheticEvent wrapper for cross-browser compatibility.

56. **What are synthetic events in React?**

**Answer:** SyntheticEvent is React's wrapper around native browser events. It provides a consistent API across browsers, normalizes event behavior, and includes methods like `preventDefault()` and `stopPropagation()`. It pools events for performance (in older React versions).

57. **How do synthetic events differ from native DOM events?**

**Answer:** Synthetic events are React's cross-browser wrapper. They have the same interface as native events but work consistently across browsers. In React 17+, events are no longer pooled. You can access the native event via `event.nativeEvent`, but it's rarely needed.

58. **How do you pass parameters to event handlers?**

**Answer:** Use arrow functions: `<button onClick={() => handleClick(id)}>` or bind: `<button onClick={handleClick.bind(this, id)}>`. For class components, create arrow function methods. The event object is passed as the last parameter automatically.

59. **What is event pooling in React?**

**Answer:** Event pooling (removed in React 17) reused event objects for performance. After the event handler, the event properties were nullified. This required calling `event.persist()` if you needed the event asynchronously. Modern React no longer pools events.

60. **How do you prevent default behavior in React?**

**Answer:** Call `event.preventDefault()` in the event handler. Example: `function handleSubmit(e) { e.preventDefault(); ... }`. This prevents default browser behavior like form submission or link navigation. Works the same as native DOM events.

61. **Explain event delegation in React.**

**Answer:** React uses event delegation by attaching event listeners to the root container instead of individual elements. Events bubble up to the root, where React handles them using the SyntheticEvent system. This improves performance and memory usage, especially with many elements.

### Conditional Rendering

62. **How do you conditionally render elements in React?**

**Answer:** Use `if/else` statements, ternary operators (`condition ? <A /> : <B />`), logical `&&` operator (`condition && <Component />`), or early returns. Ternary is best for two options, `&&` for single conditional rendering, and `if/else` for complex logic.

63. **What is the difference between `&&` and ternary operators for conditional rendering?**

**Answer:** `&&` renders when true, nothing when false: `{isLoggedIn && <Dashboard />}`. Ternary always returns something: `{isLoggedIn ? <Dashboard /> : <Login />}`. Use `&&` for optional rendering, ternary when you need an alternative.

64. **How do you conditionally render multiple elements?**

**Answer:** Use arrays: `{[condition && <Element1 />, condition2 && <Element2 />]}`. Use fragments: `{condition ? <><Element1 /><Element2 /></> : null}`. Use variables: `const elements = condition ? [<A />, <B />] : [<C />]`. Extract to separate functions for complex logic.

65. **What are the best practices for conditional rendering?**

**Answer:** Keep conditions simple and readable. Extract complex logic to variables or functions. Use early returns in components. Avoid deeply nested ternaries. Consider extracting conditional rendering to separate components. Use `&&` for simple cases, ternary for two options.

### Lists and Keys

66. **How do you render lists in React?**

**Answer:** Use `map()` to transform arrays into JSX elements: `{items.map(item => <Item key={item.id} data={item} />)}`. Always provide a unique `key` prop. Keys help React identify which items changed, were added, or removed.

67. **What is the purpose of keys in React lists?**

**Answer:** Keys help React identify which items changed, were added, or removed. They enable efficient reconciliation and prevent bugs when list order changes. Keys should be unique among siblings and stable across re-renders.

68. **What happens if you don't provide a key prop?**

**Answer:** React will warn in development. Without keys, React uses array indices, which can cause bugs when items are reordered, added, or removed. Components may maintain incorrect state, and performance can degrade. Always provide keys.

69. **Can you use index as a key? When should you avoid it?**

**Answer:** Index can be used when the list is static (no reordering, additions, or removals). Avoid index when items can be reordered, added, or removed, as it causes state bugs and performance issues. Prefer unique, stable IDs from your data.

70. **What makes a good key value?**

**Answer:** Good keys are unique among siblings, stable across re-renders, and predictable. Use IDs from your data (e.g., `user.id`, `item.uuid`). Avoid random values, timestamps, or indices (unless list is truly static). Keys don't need to be globally unique, only unique among siblings.

### Component Lifecycle (Class Components)

71. **What are the different phases of a React component's lifecycle?**

**Answer:** Three main phases: Mounting (component created and inserted into DOM), Updating (component re-renders due to props/state changes), and Unmounting (component removed from DOM). Each phase has specific lifecycle methods that React calls automatically.

72. **Explain the mounting phase lifecycle methods.**

**Answer:** Mounting methods: `constructor()` (initialize state, bind methods), `getDerivedStateFromProps()` (derive state from props), `render()` (return JSX), `componentDidMount()` (side effects, API calls). Called once when component is first rendered.

73. **Explain the updating phase lifecycle methods.**

**Answer:** Updating methods: `getDerivedStateFromProps()`, `shouldComponentUpdate()` (optimize re-renders), `render()`, `getSnapshotBeforeUpdate()` (capture DOM info), `componentDidUpdate()` (side effects after update). Called when props or state change.

74. **Explain the unmounting phase lifecycle methods.**

**Answer:** Unmounting has one method: `componentWillUnmount()`. Called before component is removed from DOM. Use it for cleanup: canceling network requests, clearing timers, removing event listeners, cleaning up subscriptions. Prevents memory leaks.

75. **What is the purpose of `componentDidMount`?**

**Answer:** `componentDidMount()` runs after the component is mounted (inserted into DOM). It's the best place for side effects: API calls, setting up subscriptions, DOM manipulation, starting timers. It runs once after the initial render. In functional components, use `useEffect` with empty dependency array.

76. **What is the purpose of `componentDidUpdate`?**

**Answer:** `componentDidUpdate()` runs after updates are flushed to the DOM. Use it for side effects that depend on prop/state changes: API calls when props change, DOM updates, logging. It receives previous props and state. In functional components, use `useEffect` with dependencies.

77. **What is the purpose of `componentWillUnmount`?**

**Answer:** `componentWillUnmount()` runs before component removal. It's essential for cleanup: canceling API requests, clearing intervals/timeouts, removing event listeners, cleaning up subscriptions. Prevents memory leaks. In functional components, return cleanup function from `useEffect`.

78. **What is `getDerivedStateFromProps` and when is it used?**

**Answer:** `getDerivedStateFromProps()` is a static method that runs before every render. It returns an object to update state or `null`. Rarely needed - usually indicates a design problem. Consider using `key` prop or moving state to a parent instead. Use cases: animating based on prop changes.

79. **What is `getSnapshotBeforeUpdate` and when is it used?**

**Answer:** `getSnapshotBeforeUpdate()` runs right before DOM updates are committed. It can capture information (scroll position, etc.) and return a value passed to `componentDidUpdate()`. Rarely used. Example: preserving scroll position during updates.

80. **What are deprecated lifecycle methods and why were they deprecated?**

**Answer:** Deprecated methods: `componentWillMount`, `componentWillReceiveProps`, `componentWillUpdate`. Deprecated because they encouraged unsafe patterns, caused bugs with async rendering, and will be removed in future React versions. Use `getDerivedStateFromProps` and `getSnapshotBeforeUpdate` instead, or better yet, use Hooks.

---

## React Hooks

### Introduction to Hooks

81. **What are React Hooks, and why were they introduced?**

**Answer:** Hooks are functions that let you "hook into" React features (state, lifecycle, context) from functional components. They were introduced to enable stateful logic in functional components, reduce complexity, improve code reuse, and eliminate the need for class components. Hooks make React code simpler and more maintainable.

82. **What are the rules of Hooks?**

**Answer:** Two main rules: 1) Only call Hooks at the top level - not inside loops, conditions, or nested functions. 2) Only call Hooks from React functions - functional components or custom Hooks. These rules ensure Hooks are called in the same order every render, which React relies on.

83. **Why can't Hooks be called conditionally?**

**Answer:** React relies on the order of Hook calls to maintain state between renders. Conditional calls would change the order, causing React to associate state with the wrong Hooks. This would lead to bugs, incorrect state, and crashes. Always call Hooks unconditionally at the top level.

84. **Can Hooks be called inside loops or nested functions?**

**Answer:** No. Hooks must be called at the top level of the component or custom Hook. Calling them in loops or nested functions violates the Rules of Hooks and causes bugs. React uses the call order to track which state belongs to which Hook, so the order must be consistent.

85. **What is the difference between Hooks and class component lifecycle methods?**

**Answer:** Hooks allow functional components to use state and lifecycle features. `useState` replaces `this.state`, `useEffect` replaces lifecycle methods (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`). Hooks are more composable, reusable, and don't require `this` binding. They enable better code organization.

### useState Hook

86. **How does the `useState` hook work?**

**Answer:** `useState` returns an array with two elements: the current state value and a function to update it. React preserves state between re-renders. When you call the setter function, React schedules a re-render with the new state value. Example: `const [count, setCount] = useState(0)`.

87. **What is the syntax of `useState`?**

**Answer:** `const [state, setState] = useState(initialValue)`. The initial value can be a primitive, object, array, or function. The setter function can accept a new value or a function that receives the previous state: `setState(newValue)` or `setState(prev => prev + 1)`.

88. **How do you update state using `useState`?**

**Answer:** Call the setter function: `setCount(count + 1)` or `setCount(prevCount => prevCount + 1)`. For objects: `setUser({...user, name: 'John'})`. Use functional updates when new state depends on previous state. State updates are asynchronous and batched.

89. **What is the difference between `useState` and class component `setState`?**

**Answer:** `useState` doesn't merge objects automatically - you must spread existing state. `setState` in classes automatically merges objects. `useState` replaces the entire state value, while `setState` merges. `useState` setter can accept a function for updates, similar to functional `setState`.

90. **How do you initialize state with a function using `useState`?**

**Answer:** Pass a function to `useState`: `const [state, setState] = useState(() => expensiveCalculation())`. The function runs only once during initial render, not on every render. This is useful for expensive initializations. Example: `useState(() => JSON.parse(localStorage.getItem('data')))`.

91. **What is functional state updates and when should you use them?**

**Answer:** Functional updates pass a function to the setter: `setCount(prev => prev + 1)`. The function receives the previous state and returns the new state. Use them when new state depends on previous state, to avoid stale closures, and when updates might be batched. Essential for correct async updates.

### useEffect Hook

92. **What is the purpose of the `useEffect` hook?**

**Answer:** `useEffect` handles side effects in functional components: API calls, subscriptions, DOM manipulation, timers. It runs after render and can optionally clean up. It combines `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` into a single API.

93. **How does `useEffect` replicate lifecycle behaviors?**

**Answer:** `useEffect` with empty deps `[]` runs once after mount (like `componentDidMount`). With dependencies, it runs after updates (like `componentDidUpdate`). The cleanup function runs before unmount (like `componentWillUnmount`). One Hook replaces multiple lifecycle methods.

94. **What is the dependency array in `useEffect`?**

**Answer:** The dependency array is the second argument: `useEffect(() => {}, [deps])`. It tells React when to re-run the effect. If a dependency value changes, the effect runs again. Empty array `[]` means run once. No array means run every render. Include all values from component scope used in the effect.

95. **What happens if you don't provide a dependency array?**

**Answer:** The effect runs after every render. This can cause infinite loops if the effect updates state. Usually a bug. Always provide a dependency array unless you specifically need the effect to run on every render (rare). React will warn about missing dependencies.

96. **What happens if you provide an empty dependency array?**

**Answer:** The effect runs only once after the initial render (mount). It never runs again, even if props or state change. Use this for one-time setup: API calls on mount, setting up subscriptions, initializing third-party libraries. The cleanup function runs on unmount.

97. **How do you perform cleanup in `useEffect`?**

**Answer:** Return a cleanup function from `useEffect`: `useEffect(() => { const timer = setInterval(...); return () => clearInterval(timer); }, [])`. The cleanup function runs before the effect runs again or when the component unmounts. Use it to cancel subscriptions, clear timers, remove event listeners.

98. **What is the cleanup function in `useEffect`?**

**Answer:** The cleanup function is returned from `useEffect`. It runs: 1) Before the effect runs again (if dependencies changed), 2) Before the component unmounts. It prevents memory leaks by cleaning up subscriptions, timers, and event listeners. Essential for proper resource management.

99. **How do you handle async operations in `useEffect`?**

**Answer:** Define an async function inside `useEffect` and call it: `useEffect(() => { async function fetchData() { const data = await api.get(); setData(data); } fetchData(); }, [])`. Don't make the effect callback itself async. Alternatively, use `.then()` with promises. Handle errors with try/catch.

100. **What is the difference between `useEffect` and `componentDidMount`?**

**Answer:** `useEffect` runs after render, `componentDidMount` runs after mount. `useEffect` can run multiple times based on dependencies, while `componentDidMount` runs once. `useEffect` combines mount, update, and unmount logic. `useEffect` is more flexible and composable.

### useContext Hook

101. **What is the `useContext` hook?**

**Answer:** `useContext` is a Hook that lets you subscribe to React Context without nesting. It accepts a Context object and returns the current context value. It's simpler than using `<Context.Consumer>`. Example: `const value = useContext(MyContext)`.

102. **How do you use Context API with `useContext`?**

**Answer:** 1) Create context: `const MyContext = createContext()`. 2) Provide value: `<MyContext.Provider value={value}>`. 3) Consume: `const value = useContext(MyContext)` in functional components. The Hook returns the nearest Provider's value or the default value.

103. **What is the difference between `useContext` and props?**

**Answer:** `useContext` accesses context values without prop drilling. Props must be passed through every component in the tree. Context allows accessing values from any component within the Provider tree. Use props for direct parent-child communication, Context for deeply nested or global data.

104. **When should you use Context API?**

**Answer:** Use Context for: theme, authentication, language/i18n, user preferences, or any data needed by many components at different nesting levels. Avoid for frequently changing data (causes re-renders) or when props would work. Context is not a replacement for state management libraries.

105. **What are the limitations of Context API?**

**Answer:** Limitations include: all consumers re-render when context value changes (even if they only need part of it), not optimized for high-frequency updates, can cause performance issues if overused, and splitting contexts can be complex. Consider splitting contexts or using state management libraries for complex apps.

### useReducer Hook

106. **What is the `useReducer` hook?**

**Answer:** `useReducer` is an alternative to `useState` for managing complex state logic. It follows the Redux pattern: `const [state, dispatch] = useReducer(reducer, initialState)`. It's useful when state logic is complex or when next state depends on previous state.

107. **How does `useReducer` differ from `useState`?**

**Answer:** `useReducer` uses a reducer function to update state, while `useState` uses direct setters. `useReducer` is better for complex state logic, multiple sub-values, or when state updates depend on previous state. `useState` is simpler for basic state. `useReducer` provides more predictable state updates.

108. **When should you use `useReducer` instead of `useState`?**

**Answer:** Use `useReducer` when: state logic is complex, you have multiple related state values, next state depends on previous state, or you want to centralize state update logic. Use `useState` for simple, independent state values. `useReducer` is also useful for forms with multiple fields.

109. **What is a reducer function?**

**Answer:** A reducer is a pure function that takes current state and an action, then returns new state: `(state, action) => newState`. It should be pure (no side effects), predictable, and return new state objects rather than mutating. Similar to Redux reducers.

110. **How do you dispatch actions with `useReducer`?**

**Answer:** Call `dispatch` with an action object: `dispatch({ type: 'INCREMENT', payload: 1 })`. The reducer receives the action and returns new state. Actions typically have a `type` and optional `payload`. Dispatch triggers a re-render with the new state returned by the reducer.

### useMemo Hook

111. **What is the `useMemo` hook?**

**Answer:** `useMemo` memoizes expensive calculations: `const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b])`. It only recalculates when dependencies change. Returns the memoized value. Use it to optimize performance by avoiding unnecessary recalculations.

112. **What is the purpose of `useMemo`?**

**Answer:** `useMemo` caches the result of expensive computations and only recalculates when dependencies change. It prevents unnecessary recalculations on every render, improving performance. It's similar to `React.memo` but for values instead of components.

113. **How does `useMemo` help with performance optimization?**

**Answer:** `useMemo` skips expensive recalculations when dependencies haven't changed. Without it, expensive operations run on every render. With it, the value is cached and reused until dependencies change. This reduces CPU usage and improves render performance, especially for complex calculations.

114. **When should you use `useMemo`?**

**Answer:** Use `useMemo` for: expensive calculations (filtering large arrays, complex math), creating objects/arrays that are dependencies of other Hooks, or preventing unnecessary re-renders of child components. Don't overuse it - React is already fast. Profile first, then optimize.

115. **What is the difference between `useMemo` and `useEffect`?**

**Answer:** `useMemo` computes and returns a value during render, synchronously. `useEffect` runs side effects after render, asynchronously. `useMemo` is for memoizing computed values. `useEffect` is for side effects (API calls, subscriptions). They serve different purposes.

### useCallback Hook

116. **What is the `useCallback` hook?**

**Answer:** `useCallback` memoizes a function: `const memoizedCallback = useCallback(() => { doSomething(a, b); }, [a, b])`. It returns the same function reference until dependencies change. Useful for preventing unnecessary re-renders of child components that receive the function as a prop.

117. **What is the purpose of `useCallback`?**

**Answer:** `useCallback` prevents function recreation on every render. It returns a memoized callback that only changes when dependencies change. This is useful when passing callbacks to optimized child components (wrapped in `React.memo`), as it prevents unnecessary re-renders.

118. **How does `useCallback` help with performance optimization?**

**Answer:** By memoizing functions, `useCallback` ensures child components receiving the function as a prop don't re-render unnecessarily. Without it, a new function is created on every render, causing `React.memo` child components to re-render even if their props haven't meaningfully changed.

119. **When should you use `useCallback`?**

**Answer:** Use `useCallback` when: passing callbacks to `React.memo` child components, functions are dependencies of other Hooks (`useEffect`, `useMemo`), or you have performance issues from function recreation. Don't overuse it - the memoization itself has a cost. Profile first.

120. **What is the difference between `useMemo` and `useCallback`?**

**Answer:** `useMemo` memoizes the result of a computation (returns a value). `useCallback` memoizes the function itself (returns a function). `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`. Use `useMemo` for values, `useCallback` for functions.

### useRef Hook

121. **What is the `useRef` hook?**

**Answer:** `useRef` returns a mutable ref object: `const ref = useRef(initialValue)`. The `.current` property persists across renders and doesn't cause re-renders when changed. Used for: accessing DOM elements, storing mutable values, or keeping previous values.

122. **What is the difference between `useRef` and `useState`?**

**Answer:** `useRef` changes don't trigger re-renders, while `useState` changes do. `useRef` returns a mutable object with `.current`, while `useState` returns state and setter. Use `useRef` for values that don't need to trigger renders (like timers, DOM refs). Use `useState` for values that affect rendering.

123. **How do you access DOM elements using `useRef`?**

**Answer:** Create a ref: `const inputRef = useRef(null)`. Attach to element: `<input ref={inputRef} />`. Access: `inputRef.current.focus()`. The `.current` property holds the DOM element. Useful for focus management, measuring elements, or integrating with third-party libraries.

124. **Can `useRef` be used to store values that persist across renders?**

**Answer:** Yes. `useRef` can store any mutable value that persists across renders without causing re-renders. Useful for: storing previous props/state, keeping interval IDs, caching expensive values, or any value you need to persist but don't want to trigger renders.

125. **What is the difference between `useRef` and creating a variable with `let`?**

**Answer:** A `let` variable inside a component is recreated on every render and doesn't persist. `useRef` persists across renders and maintains the same `.current` value. `let` variables are reset each render, while `useRef` maintains state between renders without causing re-renders.

### Custom Hooks

126. **What are custom Hooks?**

**Answer:** Custom Hooks are JavaScript functions that start with "use" and can call other Hooks. They extract component logic into reusable functions. They enable sharing stateful logic between components without changing component hierarchy. Examples: `useFetch`, `useLocalStorage`, `useAuth`.

127. **How do you create a custom Hook?**

**Answer:** Create a function starting with "use" that can call other Hooks: `function useCustomHook() { const [state, setState] = useState(); useEffect(() => {...}); return state; }`. Use it in components: `const value = useCustomHook()`. Custom Hooks can return anything.

128. **What are the naming conventions for custom Hooks?**

**Answer:** Custom Hooks must start with "use" (e.g., `useAuth`, `useFetch`, `useLocalStorage`). This convention ensures React can check that Hooks are called correctly. The "use" prefix tells React and other developers that the function follows the Rules of Hooks.

129. **What are some common use cases for custom Hooks?**

**Answer:** Common use cases: data fetching (`useFetch`), form handling (`useForm`), authentication (`useAuth`), local storage (`useLocalStorage`), API calls (`useApi`), timers (`useInterval`), debouncing (`useDebounce`), and any reusable stateful logic shared between components.

130. **Can custom Hooks use other Hooks?**

**Answer:** Yes, custom Hooks can call other Hooks (built-in or custom). This is how they work - they compose Hooks to create reusable logic. Example: `function useAuth() { const [user, setUser] = useState(); useEffect(() => {...}); return user; }` uses `useState` and `useEffect`.

### Other Hooks

131. **What is the `useLayoutEffect` hook and how does it differ from `useEffect`?**

**Answer:** `useLayoutEffect` runs synchronously after DOM mutations but before browser paint. `useEffect` runs asynchronously after paint. Use `useLayoutEffect` when you need to read layout and synchronously re-render (e.g., measuring DOM, preventing visual flicker). Most cases use `useEffect`.

132. **What is the `useImperativeHandle` hook?**

**Answer:** `useImperativeHandle` customizes the instance value exposed when using `ref` with `forwardRef`. It's used with `forwardRef` to expose specific methods to parent components. Rarely needed. Example: exposing `focus()` method from a custom input component to parent.

133. **What is the `useDebugValue` hook?**

**Answer:** `useDebugValue` displays a label for custom Hooks in React DevTools. It only runs in development. Use it to make custom Hooks easier to debug: `useDebugValue(isOnline ? 'Online' : 'Offline')`. It doesn't affect functionality, only DevTools display.

134. **What is the `useId` hook?**

**Answer:** `useId` generates unique IDs stable across server and client renders: `const id = useId()`. Useful for accessibility attributes (`htmlFor`, `aria-describedby`) that need unique IDs. Prevents hydration mismatches. Returns a string like `:r1:`.

135. **What is the `useTransition` hook?**

**Answer:** `useTransition` (React 18+) marks state updates as non-urgent transitions: `const [isPending, startTransition] = useTransition()`. Wraps updates: `startTransition(() => setState(...))`. Allows React to keep UI responsive during heavy updates. Useful for large list filtering, search, etc.

136. **What is the `useDeferredValue` hook?**

**Answer:** `useDeferredValue` (React 18+) defers updating a value: `const deferredValue = useDeferredValue(value)`. Returns a deferred version that "lags behind" the original. Useful for keeping UI responsive during expensive updates. Similar to debouncing but integrated with React's rendering.

---

## State Management

### Local State vs Global State

137. **What is the difference between local and global state?**

**Answer:** Local state is managed within a single component using `useState` or `useReducer`. Global state is shared across multiple components, managed via Context API, Redux, or other state management libraries. Local state is simpler and isolated. Global state enables sharing data across the component tree.

138. **When should you use local state vs global state?**

**Answer:** Use local state for: component-specific UI state (toggles, form inputs), data only needed in one component, or temporary values. Use global state for: user authentication, theme preferences, shopping cart, or any data needed by many components. Start with local state, lift it up when needed.

139. **How do you decide what state should be global?**

**Answer:** Make state global if: it's needed by multiple unrelated components, it represents app-wide concerns (auth, theme), or lifting state up would cause prop drilling. Keep it local if: it's only used in one component or a small subtree. Consider: "Do many components need this?" and "Is prop drilling becoming unwieldy?"

### Context API

140. **What is the Context API?**

**Answer:** Context API provides a way to pass data through the component tree without prop drilling. It consists of `createContext()`, `Provider`, and `useContext()`. It's built into React and useful for sharing "global" data like themes, authentication, or language preferences.

141. **How do you create and use Context in React?**

**Answer:** 1) Create: `const MyContext = createContext(defaultValue)`. 2) Provide: `<MyContext.Provider value={value}>`. 3) Consume: `const value = useContext(MyContext)` in functional components or `<MyContext.Consumer>` in class components. The value comes from the nearest Provider.

142. **What are the advantages and disadvantages of Context API?**

**Answer:** Advantages: avoids prop drilling, built into React, simple API. Disadvantages: all consumers re-render when context changes (even if they only need part of it), not optimized for frequent updates, can cause performance issues if overused. Not a replacement for state management libraries in complex apps.

143. **When should you use Context API?**

**Answer:** Use Context for: theme, authentication, language/i18n, user preferences, or data needed by many components at different nesting levels. Avoid for: frequently changing data, high-frequency updates, or when props would work. Context is best for relatively static or slowly changing data.

144. **How do you avoid unnecessary re-renders with Context API?**

**Answer:** Split contexts by concern (separate contexts for theme, auth, etc.), use `React.memo` on consumer components, split Provider values into multiple contexts, or use state management libraries for complex scenarios. Memoize context values if they're objects/arrays. Consider using selectors.

145. **What is the difference between Context API and prop drilling?**

**Answer:** Prop drilling passes props through every component in the tree, even if intermediate components don't use them. Context API allows components to access values directly without passing through intermediate components. Context eliminates the need to thread props through unrelated components.

### Redux

146. **What is Redux and why is it used?**

**Answer:** Redux is a predictable state container for JavaScript apps. It provides a single source of truth, makes state changes predictable through pure functions, enables time-travel debugging, and works well with React. Used for managing complex application state that needs to be shared across many components.

147. **What are the core principles of Redux?**

**Answer:** Three principles: 1) Single source of truth (state in one store), 2) State is read-only (changed only by dispatching actions), 3) Changes are made with pure functions (reducers). These principles make state predictable, debuggable, and testable.

148. **Explain the Redux data flow.**

**Answer:** 1) Component dispatches an action, 2) Action goes to reducer, 3) Reducer returns new state, 4) Store updates, 5) Components subscribed to store re-render. Flow is unidirectional: Action → Reducer → Store → Component. This makes state changes predictable and traceable.

149. **What are actions, reducers, and store in Redux?**

**Answer:** Actions are plain objects describing what happened (`{ type: 'INCREMENT' }`). Reducers are pure functions that take current state and action, return new state. Store holds the state tree and provides methods to dispatch actions and subscribe to changes. Store is created with `createStore(reducer)`.

150. **What is the difference between Redux and Context API?**

**Answer:** Redux provides: predictable state updates, middleware, DevTools, time-travel debugging, and better performance for frequent updates. Context API is simpler, built-in, but causes all consumers to re-render. Redux is better for complex apps with lots of state changes. Context is better for simple, static data.

151. **When should you use Redux?**

**Answer:** Use Redux when: you have large amounts of application state, state is needed in many places, state updates are complex, you need time-travel debugging, or you need middleware (logging, async actions). Don't use it for simple apps - `useState` or Context may be sufficient.

152. **What is Redux Toolkit and why is it recommended?**

**Answer:** Redux Toolkit (RTK) is the official, opinionated way to write Redux. It includes: `createSlice` (reduces boilerplate), `configureStore` (simplified setup), built-in Immer (mutations), and better TypeScript support. It's recommended because it simplifies Redux code and follows best practices.

153. **What are Redux middleware? Give examples.**

**Answer:** Middleware intercept actions before they reach reducers. Examples: `redux-thunk` (async actions), `redux-saga` (complex async flows), `redux-logger` (logging), `redux-persist` (persist state). Middleware sits between dispatch and reducer, enabling side effects and async operations.

154. **What is `redux-thunk` and when is it used?**

**Answer:** `redux-thunk` allows action creators to return functions instead of objects. These functions receive `dispatch` and `getState`. Used for async operations: `dispatch => { fetchData().then(data => dispatch({ type: 'SUCCESS', data })) }`. Simplest way to handle async in Redux.

155. **What is `redux-saga` and how does it differ from `redux-thunk`?**

**Answer:** `redux-saga` uses generator functions for complex async flows. It's more powerful than thunks: easier testing, cancellation, complex flows, and better error handling. Thunks are simpler for basic async. Sagas are better for complex scenarios with multiple async operations, cancellation, or race conditions.

156. **How do you connect a React component to Redux store?**

**Answer:** Use `connect()` from `react-redux`: `export default connect(mapStateToProps, mapDispatchToProps)(Component)`. Or use Hooks: `useSelector()` and `useDispatch()`. `connect()` is the older approach, Hooks are modern. Both subscribe components to store updates.

157. **What is the difference between `mapStateToProps` and `mapDispatchToProps`?**

**Answer:** `mapStateToProps` selects data from store and passes as props: `(state) => ({ count: state.count })`. `mapDispatchToProps` binds action creators and passes as props: `(dispatch) => ({ increment: () => dispatch(increment()) })`. Both are optional. With Hooks, use `useSelector` and `useDispatch`.

158. **What are Redux selectors?**

**Answer:** Selectors are functions that extract and derive data from Redux state: `const getVisibleTodos = (state) => state.todos.filter(t => !t.completed)`. They enable: computed values, memoization (with `reselect`), and reusable logic. Selectors keep components decoupled from state structure.

### Other State Management Libraries

159. **What is Zustand and how does it compare to Redux?**

**Answer:** Zustand is a small, fast state management library. It's simpler than Redux: less boilerplate, no actions/reducers, direct state mutations (with Immer), and built-in React integration. Good for medium-sized apps. Redux is better for very large apps needing time-travel debugging and middleware.

160. **What is Jotai and how does it work?**

**Answer:** Jotai is an atomic state management library. State is split into atoms (small pieces). Components subscribe to specific atoms, not the whole store. This prevents unnecessary re-renders. It's inspired by Recoil but simpler. Good for fine-grained reactivity and avoiding re-render issues.

161. **What is Recoil and what are its key features?**

**Answer:** Recoil is Facebook's state management library for React. Key features: atoms (small state pieces), selectors (derived state), async support, and fine-grained subscriptions. Components only re-render when their subscribed atoms change. Good for complex state with many derived values.

162. **What is MobX and how does it differ from Redux?**

**Answer:** MobX uses observable state and automatic reactions. It's more object-oriented and requires less boilerplate than Redux. State is mutable, and MobX tracks changes automatically. Redux is functional and immutable. MobX is easier to learn but less predictable. Redux is more explicit and debuggable.

163. **What is Valtio and when would you use it?**

**Answer:** Valtio makes proxy-state simple for React. You create state with `proxy()`, mutate it directly, and components auto-update. It's very simple and requires minimal code. Good for rapid prototyping or when you prefer mutable state. Less popular than Redux or Zustand.

---

## Routing

### React Router

164. **What is React Router and why is it used?**

**Answer:** React Router is a routing library for React that enables navigation without page refreshes (SPA). It maps URLs to components, handles browser history, and provides navigation components. Essential for multi-page React applications. It keeps UI in sync with the URL.

165. **What is the difference between client-side and server-side routing?**

**Answer:** Client-side routing (React Router) handles navigation in the browser without server requests. The server serves one HTML file, and JavaScript handles routing. Server-side routing requires a server request for each route. Client-side is faster and provides a smoother user experience for SPAs.

166. **How do you install and set up React Router?**

**Answer:** Install: `npm install react-router-dom`. Wrap app with router: `<BrowserRouter><App /></BrowserRouter>`. Define routes: `<Routes><Route path="/" element={<Home />} /></Routes>`. Use `<Link>` for navigation. React Router v6 uses `Routes` and `Route` with `element` prop.

167. **What is the difference between `<BrowserRouter>` and `<HashRouter>`?**

**Answer:** `<BrowserRouter>` uses HTML5 history API (`/about`). Requires server configuration for direct URL access. `<HashRouter>` uses hash (`/#/about`). Works without server config but URLs look less clean. Prefer `BrowserRouter` for production. Use `HashRouter` if you can't configure the server.

168. **What is the difference between `<Switch>` and `<Routes>`?**

**Answer:** `<Switch>` is React Router v5, renders the first matching route. `<Routes>` is v6, more powerful, uses `element` prop instead of `component`, and supports nested routes better. `<Routes>` is the modern approach. Both render only the first matching route.

169. **How do you create routes in React Router?**

**Answer:** In v6: `<Routes><Route path="/" element={<Home />} /><Route path="/about" element={<About />} /></Routes>`. Use `path` for URL and `element` for component. For v5: `<Route path="/" component={Home} />`. Routes are matched top-to-bottom, first match wins.

170. **What is the difference between `<Route>` and `<Link>`?**

**Answer:** `<Route>` defines which component to render for a URL path. `<Link>` is a navigation component that renders an anchor tag and prevents full page reload. `<Link to="/about">About</Link>` navigates to `/about`, and the matching `<Route>` renders the component.

171. **How do you implement nested routes in React Router?**

**Answer:** In v6: use `<Outlet />` in parent component and nested `<Route>` elements: `<Route path="users" element={<Users />}><Route path=":id" element={<UserDetail />} /></Route>`. In v5: use `component` prop and nested routes. `<Outlet />` renders child routes.

172. **What is the `useNavigate` hook?**

**Answer:** `useNavigate` (v6) replaces `useHistory`. Returns a navigate function: `const navigate = useNavigate(); navigate('/about')`. Can navigate programmatically, go back/forward: `navigate(-1)`, or replace history: `navigate('/path', { replace: true })`. More flexible than `useHistory`.

173. **What is the `useParams` hook?**

**Answer:** `useParams` returns URL parameters as an object: `const { id } = useParams()`. For route `/users/:id`, accessing `/users/123` gives `{ id: '123' }`. Used to extract dynamic route segments. Essential for dynamic routing and fetching data based on URL parameters.

174. **What is the `useLocation` hook?**

**Answer:** `useLocation` returns the current location object with `pathname`, `search`, `hash`, `state`, and `key`. Useful for: getting current path, reading query strings, accessing location state passed via `navigate()`. Example: `const location = useLocation(); location.pathname`.

175. **What is the `useSearchParams` hook?**

**Answer:** `useSearchParams` (v6) provides access to URL search parameters: `const [searchParams, setSearchParams] = useSearchParams()`. Read: `searchParams.get('query')`. Update: `setSearchParams({ query: 'new' })`. Replaces manual parsing of `window.location.search`.

176. **How do you pass data between routes?**

**Answer:** Methods: 1) URL params: `/users/:id`, 2) Query strings: `?key=value`, 3) State via `navigate('/path', { state: { data } })` and read with `useLocation().state`, 4) Global state (Context/Redux). State is best for complex objects, URL params for simple IDs.

177. **What are route guards and how do you implement them?**

**Answer:** Route guards protect routes (e.g., require authentication). Create a wrapper component: `<ProtectedRoute><Component /></ProtectedRoute>`. Check auth in the wrapper, redirect if not authenticated: `if (!isAuth) return <Navigate to="/login" />`. Or use `<Route element={<ProtectedRoute />}>`.

178. **What is lazy loading routes and how do you implement it?**

**Answer:** Lazy loading loads route components only when needed, reducing initial bundle size. Use: `const About = lazy(() => import('./About'))` and wrap with `<Suspense fallback={<Loading />}><About /></Suspense>`. This code-splits routes automatically. Improves initial load time.

179. **How do you handle 404 pages in React Router?**

**Answer:** Add a catch-all route at the end: `<Route path="*" element={<NotFound />} />`. This matches any unmatched path. In v5: `<Route component={NotFound} />` without a path, or use `path="*"`. The 404 component should inform users the page doesn't exist.

180. **What is the difference between `exact` and `strict` props in React Router?**

**Answer:** `exact` (v5) requires the path to match exactly. Without it, `/about` matches `/about/team`. `strict` makes trailing slashes matter: `/about/` ≠ `/about`. In v6, routes are exact by default. `strict` is rarely needed. Both help with precise route matching.

---

## Forms and Validation

### Controlled Components

181. **What are controlled components in React?**

**Answer:** Controlled components have their value controlled by React state. The input value is stored in state and updated via `onChange`: `<input value={name} onChange={(e) => setName(e.target.value)} />`. React controls the input, making it the "single source of truth". Preferred approach in React.

182. **What are uncontrolled components in React?**

**Answer:** Uncontrolled components store their state in the DOM. Use `ref` to access values: `<input ref={inputRef} />`, then `inputRef.current.value`. Form data is handled by the DOM, not React state. Less React-like but sometimes simpler for basic forms or integrating with non-React code.

183. **What is the difference between controlled and uncontrolled components?**

**Answer:** Controlled: React state controls value, `value` prop and `onChange` handler required, React is source of truth. Uncontrolled: DOM controls value, use `ref` to access, DOM is source of truth. Controlled is preferred for React apps. Uncontrolled can be simpler for simple forms.

184. **When would you use controlled vs uncontrolled components?**

**Answer:** Use controlled for: most React forms, when you need validation, when you need to format input, or when input affects other parts of UI. Use uncontrolled for: simple forms, file inputs, or when integrating with non-React libraries. Controlled is generally preferred.

185. **How do you handle form submissions in React?**

**Answer:** Use `onSubmit` on the form: `<form onSubmit={handleSubmit}>`. Prevent default: `function handleSubmit(e) { e.preventDefault(); ... }`. Access form data from state (controlled) or refs (uncontrolled). Submit to API, validate, show errors, or navigate. Controlled approach is recommended.

186. **How do you handle multiple inputs in a form?**

**Answer:** For controlled: use one state object: `const [formData, setFormData] = useState({ name: '', email: '' })`. Update with: `setFormData({...formData, [e.target.name]: e.target.value})`. Use `name` attributes matching state keys. Or use separate state for each field. Object approach scales better.

### Form Validation

187. **How do you perform form validation in React?**

**Answer:** Validate in `onChange` (real-time) or `onSubmit` (on submit). Store errors in state: `const [errors, setErrors] = useState({})`. Check rules: `if (!email.includes('@')) setErrors({...errors, email: 'Invalid email'})`. Display errors near inputs. Can use libraries like Formik or React Hook Form.

188. **What are some popular form validation libraries for React?**

**Answer:** Popular libraries: React Hook Form (performance, minimal re-renders), Formik (popular, feature-rich), Yup (schema validation, often used with Formik), Zod (TypeScript-first validation), and React Final Form. React Hook Form is currently most popular due to performance benefits.

189. **How do you validate forms on submit vs on change?**

**Answer:** On submit: validate all fields when form is submitted, show errors, prevent submission if invalid. On change: validate as user types, provide immediate feedback. Best practice: validate on change for better UX, validate on submit as final check. Combine both approaches.

190. **How do you display validation errors to users?**

**Answer:** Store errors in state: `const [errors, setErrors] = useState({})`. Display near inputs: `{errors.email && <span className="error">{errors.email}</span>}`. Use conditional rendering, style with CSS, and ensure errors are accessible (ARIA attributes). Show errors clearly and helpfully.

191. **What is Formik and how does it work?**

**Answer:** Formik is a form library that handles: form state, validation, error handling, and submission. It provides `useFormik` Hook or `<Formik>` component. Works with Yup for schema validation. Reduces boilerplate but can cause performance issues with many fields due to re-renders.

192. **What is React Hook Form and what are its advantages?**

**Answer:** React Hook Form is a performant form library using uncontrolled components and refs. Advantages: minimal re-renders (better performance), smaller bundle size, easier validation, better TypeScript support, and less boilerplate. Currently the most popular React form library.

193. **How do you handle file uploads in React forms?**

**Answer:** Use `<input type="file" />` (always uncontrolled). Access via ref: `const fileRef = useRef(); <input ref={fileRef} type="file" />`, then `fileRef.current.files[0]`. Or use `onChange`: `onChange={(e) => setFile(e.target.files[0])}`. Upload using FormData or fetch API. Validate file size/type.

---

## Styling

### CSS Approaches

194. **What are the different ways to style React components?**

**Answer:** Ways to style: 1) Regular CSS files (import in component), 2) CSS Modules (scoped styles), 3) Inline styles (object with camelCase), 4) CSS-in-JS (Styled Components, Emotion), 5) Utility-first CSS (Tailwind), 6) Sass/SCSS. Each has trade-offs between simplicity, scoping, and performance.

195. **What are CSS Modules and how do they work?**

**Answer:** CSS Modules scope CSS to components by generating unique class names. Import: `import styles from './Component.module.css'`. Use: `<div className={styles.container}>`. Build tools transform class names to be unique, preventing style conflicts. File must end in `.module.css`.

196. **What are the advantages of CSS Modules?**

**Answer:** Advantages: automatic scoping (no conflicts), familiar CSS syntax, good tooling support, can be used with Sass, and no runtime cost. Styles are scoped to the component, making it safe to use generic class names. Better than global CSS for component-based architecture.

197. **What is the difference between CSS Modules and regular CSS?**

**Answer:** Regular CSS is global - classes can conflict. CSS Modules are scoped - each component gets unique class names. CSS Modules require `.module.css` extension and importing as an object. Regular CSS is imported as a side effect. CSS Modules prevent style conflicts automatically.

198. **How do you use inline styles in React?**

**Answer:** Pass a style object: `<div style={{ color: 'red', fontSize: '16px' }}>`. Use camelCase for properties: `fontSize` not `font-size`. Can use variables: `const style = { color: 'blue' }; <div style={style}>`. Inline styles have highest specificity and override CSS.

199. **What are the limitations of inline styles?**

**Answer:** Limitations: no pseudo-classes (`:hover`, `:focus`), no media queries, no keyframe animations, harder to maintain, no CSS features (selectors, inheritance), and increases JS bundle size. Use for dynamic styles, prefer CSS for static styles. Not suitable for complex styling.

### CSS-in-JS

200. **What is CSS-in-JS?**

**Answer:** CSS-in-JS writes CSS using JavaScript. Styles are defined in JS files, scoped to components, and can use JS features (variables, functions). Libraries: Styled Components, Emotion, JSS. Benefits: scoped styles, dynamic styling, and component co-location. Trade-off: runtime cost and larger bundle.

201. **What is Styled Components and how does it work?**

**Answer:** Styled Components is a CSS-in-JS library. Create styled elements: `const Button = styled.button\`color: blue;\``. It generates unique class names, scopes styles, and enables dynamic styling via props. Styles are co-located with components. Popular for React applications.

202. **What are the advantages and disadvantages of CSS-in-JS?**

**Answer:** Advantages: scoped styles, dynamic styling, component co-location, no class name conflicts, and theme support. Disadvantages: runtime cost, larger bundle size, learning curve, harder to debug, and no browser DevTools support (though some libraries add it). Good for component libraries.

203. **What is Emotion and how does it compare to Styled Components?**

**Answer:** Emotion is similar to Styled Components but offers: better performance, smaller bundle, more flexible API, and can work without Babel plugin. Both support styled API and CSS prop. Emotion is faster and more flexible. Styled Components has larger community. Both are excellent choices.

204. **What is the `styled` function in Styled Components?**

**Answer:** `styled` is a function that creates styled React components. Syntax: `const Button = styled.button\`css here\`` or `styled('div')\`css\``. It returns a React component with the styles applied. Can accept props for dynamic styling: `styled.button\`color: ${props => props.color};\``.

205. **How do you handle theming with Styled Components?**

**Answer:** Wrap app with `<ThemeProvider theme={theme}>`. Access theme in styled components: `styled.div\`color: ${props => props.theme.colors.primary};\``. Theme is passed as prop to all styled components. Change theme by updating ThemeProvider. Enables easy theme switching and dark mode.

### Utility-First CSS

206. **What is Tailwind CSS?**

**Answer:** Tailwind is a utility-first CSS framework. Instead of components, it provides utility classes: `className="flex items-center justify-between p-4"`. You compose utilities to build designs. Highly customizable via config. Popular for rapid UI development. Requires build process to purge unused styles.

207. **What are the advantages of utility-first CSS frameworks?**

**Answer:** Advantages: rapid development, consistent design, no naming conflicts, small bundle (with purging), highly customizable, and responsive utilities. Disadvantages: HTML can get verbose, learning curve for class names, and requires build setup. Good for rapid prototyping and consistent designs.

208. **How do you use Tailwind CSS with React?**

**Answer:** Install: `npm install -D tailwindcss`. Configure `tailwind.config.js`. Add to CSS: `@tailwind base; @tailwind components; @tailwind utilities;`. Use classes: `<div className="flex p-4 bg-blue-500">`. Build process purges unused styles. Works with Create React App, Next.js, Vite.

209. **What is the difference between Tailwind CSS and Bootstrap?**

**Answer:** Tailwind is utility-first (compose utilities), Bootstrap is component-based (pre-built components). Tailwind: more flexible, smaller bundle (with purging), requires more HTML classes. Bootstrap: faster to start, larger bundle, less flexible. Tailwind is more popular in modern React development.

210. **How do you customize Tailwind CSS?**

**Answer:** Customize via `tailwind.config.js`: extend theme (colors, spacing, fonts), add custom utilities, configure plugins, and set breakpoints. Can override defaults or extend. Example: `theme: { extend: { colors: { brand: '#...' } } }`. Then use: `className="bg-brand"`.

### Sass/SCSS

211. **How do you use Sass/SCSS with React?**

**Answer:** Install: `npm install sass`. Rename `.css` to `.scss` or `.sass`. Import: `import './styles.scss'`. Use Sass features: variables, nesting, mixins, functions. Works with Create React App, Next.js, and most build tools. Sass compiles to CSS during build.

212. **What are the advantages of using Sass?**

**Answer:** Advantages: variables (DRY principle), nesting (better organization), mixins (reusable code), functions, and partials (modular CSS). Makes CSS more maintainable and powerful. Still compiles to regular CSS, so browser compatibility is the same. Popular for large projects.

213. **What are Sass variables and mixins?**

**Answer:** Variables store values: `$primary-color: #3498db; color: $primary-color;`. Mixins are reusable code blocks: `@mixin flex-center { display: flex; align-items: center; }` then `@include flex-center;`. Both reduce repetition and improve maintainability. Variables for values, mixins for patterns.

---

## Performance Optimization

### React Performance Basics

214. **What is React's Virtual DOM?**

**Answer:** Virtual DOM is a JavaScript representation of the real DOM. React creates a virtual tree of components/elements. When state changes, React creates a new virtual tree, compares it with the previous one (diffing), and updates only the changed parts in the real DOM. This is more efficient than direct DOM manipulation.

215. **How does React's reconciliation process work?**

**Answer:** Reconciliation is how React updates the DOM. Process: 1) State/props change, 2) React creates new virtual tree, 3) Compares (diffs) with previous tree, 4) Identifies minimal changes needed, 5) Updates real DOM efficiently. React batches updates and uses heuristics to minimize DOM operations.

216. **What is the difference between Virtual DOM and Real DOM?**

**Answer:** Real DOM is the browser's representation, slow to update, and causes reflows/repaints. Virtual DOM is React's lightweight JavaScript representation, fast to create/compare, and only updates changed parts in real DOM. Virtual DOM is a programming concept, real DOM is what browsers render.

217. **Why is React's Virtual DOM efficient?**

**Answer:** Virtual DOM is efficient because: 1) Batching updates (multiple changes in one update), 2) Diffing algorithm minimizes changes, 3) Only updates what changed (not entire tree), 4) Avoids expensive DOM queries, 5) Predictable updates. However, it's not always faster than manual optimization - it's about developer experience.

218. **What is the diffing algorithm in React?**

**Answer:** Diffing compares old and new virtual trees to find minimal changes. Rules: 1) Elements of different types → replace, 2) Same type → update attributes, 3) List items → use keys to match. React uses heuristics assuming: same position = same component, keys identify items. Efficient but not perfect.

### Optimization Techniques

219. **What is `React.memo` and how does it help with performance?**

**Answer:** `React.memo` is a higher-order component that memoizes functional components. It only re-renders if props change (shallow comparison). Wraps component: `export default React.memo(Component)`. Prevents unnecessary re-renders when parent re-renders but props haven't changed. Similar to `PureComponent` for classes.

220. **What is the difference between `React.memo` and `useMemo`?**

**Answer:** `React.memo` memoizes entire components (prevents re-render if props unchanged). `useMemo` memoizes computed values within a component. `React.memo` is for components, `useMemo` is for expensive calculations. Both optimize performance but at different levels.

221. **When should you use `React.memo`?**

**Answer:** Use `React.memo` when: component receives same props frequently, component is expensive to render, or parent re-renders often but props don't change. Don't overuse - memoization has cost. Profile first. Most components don't need it. Useful for list items or frequently re-rendered components.

222. **What is `useMemo` and when should you use it?**

**Answer:** `useMemo` memoizes expensive calculations: `const value = useMemo(() => expensiveCalc(a, b), [a, b])`. Only recalculates when dependencies change. Use for: expensive computations, creating objects/arrays that are dependencies, or preventing child re-renders. Don't overuse - React is already fast.

223. **What is `useCallback` and when should you use it?**

**Answer:** `useCallback` memoizes functions: `const fn = useCallback(() => {...}, [deps])`. Returns same function reference until deps change. Use when: passing functions to `React.memo` children, functions are Hook dependencies, or preventing unnecessary re-renders. Don't overuse - has its own cost.

224. **How do you prevent unnecessary re-renders?**

**Answer:** Methods: 1) `React.memo` for components, 2) `useMemo` for values, 3) `useCallback` for functions, 4) Split contexts (avoid large context values), 5) Lift state down (keep state local), 6) Use `useReducer` for complex state, 7) Profile with DevTools. Start with profiling, then optimize.

225. **What is code splitting and how do you implement it?**

**Answer:** Code splitting splits code into smaller chunks loaded on demand. Implement: `const Component = lazy(() => import('./Component'))` with `Suspense`. Or use dynamic imports: `import('./module').then(...)`. Webpack automatically splits code. Reduces initial bundle size, improves load time.

226. **What is lazy loading and how do you implement it in React?**

**Answer:** Lazy loading loads components/code only when needed. Use `React.lazy`: `const Component = React.lazy(() => import('./Component'))`. Wrap with `Suspense`: `<Suspense fallback={<Loading />}><Component /></Suspense>`. Component loads when first rendered. Reduces initial bundle size.

227. **What is the `React.lazy` function?**

**Answer:** `React.lazy` enables code splitting for components. Takes a function returning dynamic import: `const Component = React.lazy(() => import('./Component'))`. Returns a lazy component that loads on first render. Must be used with `Suspense`. Only works with default exports.

228. **What is the `Suspense` component?**

**Answer:** `Suspense` shows fallback UI while lazy components load. Wrap lazy components: `<Suspense fallback={<Loading />}><LazyComponent /></Suspense>`. Displays fallback during loading, then component when ready. Also used for data fetching in React 18+. Enables better loading states.

229. **How do you optimize images in React?**

**Answer:** Methods: 1) Use `next/image` (Next.js) or similar, 2) Lazy load images (`loading="lazy"`), 3) Use appropriate formats (WebP, AVIF), 4) Responsive images (`srcset`), 5) Compress images, 6) Use CDN, 7) Blur placeholders. Images are often the largest assets - optimization is crucial.

230. **What is bundle size optimization?**

**Answer:** Bundle size optimization reduces JavaScript bundle size. Methods: code splitting, tree shaking (remove unused code), minification, compression (gzip/brotli), analyze and remove large dependencies, use dynamic imports, and optimize images. Smaller bundles = faster load times, better UX.

231. **How do you analyze bundle size?**

**Answer:** Tools: 1) `webpack-bundle-analyzer` (visualize bundle), 2) `source-map-explorer`, 3) Build tool stats, 4) Chrome DevTools (Network tab), 5) `npm run build -- --analyze`. Identify large dependencies, unused code, and optimization opportunities. Regular analysis prevents bundle bloat.

232. **What are the React DevTools Profiler and how do you use them?**

**Answer:** React DevTools Profiler measures component render performance. Record a session, interact with app, stop recording. Shows: render time per component, why components rendered, and commit details. Helps identify slow components and unnecessary re-renders. Essential for performance optimization.

### Advanced Performance

233. **What is React Fiber?**

**Answer:** React Fiber is React's reconciliation algorithm (rewrite of core). It enables: incremental rendering (split work into chunks), priority-based updates, interruption and resumption of work, and better error boundaries. Fiber is the underlying architecture that powers React's rendering.

234. **How does React Fiber improve performance?**

**Answer:** Fiber improves performance by: 1) Breaking work into units (can pause/resume), 2) Prioritizing updates (urgent vs non-urgent), 3) Enabling concurrent features, 4) Better scheduling (doesn't block main thread), 5) Time slicing (spread work over multiple frames). Makes UI more responsive.

235. **What is concurrent rendering in React?**

**Answer:** Concurrent rendering (React 18+) allows React to interrupt rendering to handle urgent updates. React can start rendering, pause for urgent work, then continue. Enables features like `startTransition` and `useDeferredValue`. Keeps UI responsive during heavy updates. Backward compatible.

236. **What is time slicing in React?**

**Answer:** Time slicing breaks rendering work into chunks spread across multiple frames. React can pause rendering, handle user input, then resume. Prevents blocking the main thread, keeping UI responsive. Part of React Fiber architecture. Enables smooth 60fps even during heavy updates.

237. **What are the benefits of concurrent features in React 18+?**

**Answer:** Benefits: 1) Better responsiveness (doesn't block on updates), 2) `startTransition` for non-urgent updates, 3) `useDeferredValue` for deferred values, 4) Automatic batching improvements, 5) Better Suspense integration. Makes apps feel faster and more responsive, especially on slower devices.

---

## Testing

### Testing Basics

238. **What are the common testing libraries used in React applications?**

**Answer:** Common libraries: Jest (test runner, assertions, mocking), React Testing Library (component testing, user-centric), Enzyme (older, less recommended), Cypress (E2E), Playwright (E2E), MSW (API mocking). Jest + React Testing Library is the standard combination for React testing.

239. **What is Jest and why is it used?**

**Answer:** Jest is a JavaScript test runner by Facebook. Features: test runner, assertions, mocking, code coverage, snapshot testing, and watch mode. Works out of the box with Create React App. Fast, well-documented, and the standard for React testing. Handles test execution and assertions.

240. **What is React Testing Library and how does it differ from Enzyme?**

**Answer:** React Testing Library focuses on testing from user perspective (what users see/interact with). Enzyme tests implementation details (internal state, methods). RTL encourages better practices, is simpler, and aligns with React's philosophy. Enzyme is older and less maintained. RTL is recommended.

241. **What are the principles of React Testing Library?**

**Answer:** Principles: 1) Test like a user (queries by role, text, label), 2) Avoid testing implementation details, 3) Prefer queries that are accessible, 4) Test behavior, not implementation. Philosophy: "The more your tests resemble how your software is used, the more confidence they can give you."

242. **What is the difference between unit tests, integration tests, and E2E tests?**

**Answer:** Unit tests: test individual functions/components in isolation. Integration tests: test how components work together. E2E tests: test entire user flows in a real browser. Unit: fast, many. Integration: medium speed, test interactions. E2E: slow, test critical paths. Use all three for confidence.

### Writing Tests

243. **How do you write a unit test for a React component?**

**Answer:** Import: `import { render, screen } from '@testing-library/react'`. Render component: `render(<Component />)`. Query elements: `screen.getByText('Hello')`. Assert: `expect(element).toBeInTheDocument()`. Test behavior, not implementation. Example: `test('renders button', () => { render(<Button />); expect(screen.getByRole('button')).toBeInTheDocument(); })`.

244. **What is snapshot testing and when should you use it?**

**Answer:** Snapshot testing captures component output and compares to saved snapshot. Use `toMatchSnapshot()`. Useful for: catching unintended changes, testing complex output, or regression testing. Limitations: can be brittle, requires maintenance. Use sparingly, prefer testing behavior. Good for stable components.

245. **How do you test user interactions in React components?**

**Answer:** Use `@testing-library/user-event`: `import userEvent from '@testing-library/user-event'`. Simulate interactions: `await userEvent.click(button)`, `await userEvent.type(input, 'text')`. More realistic than `fireEvent`. Tests actual user behavior. Example: `await userEvent.click(screen.getByRole('button'))`.

246. **How do you test async operations in React components?**

**Answer:** Use `waitFor` or `findBy` queries: `await waitFor(() => expect(screen.getByText('Loaded')).toBeInTheDocument())` or `await screen.findByText('Loaded')`. `findBy` queries wait automatically. Handle promises, use async/await. Mock async functions. Example: `const data = await screen.findByText('Data loaded')`.

247. **How do you test components that use Hooks?**

**Answer:** Test normally - Hooks work in tests. Render component using Hooks: `render(<ComponentWithHooks />)`. Test behavior, not Hook implementation. If testing custom Hooks, use `@testing-library/react-hooks` (or renderHook in newer versions). Hooks are transparent in component tests.

248. **How do you test components that use Context?**

**Answer:** Wrap component with Provider in test: `render(<Context.Provider value={mockValue}><Component /></Context.Provider>)`. Or create test wrapper: `const wrapper = ({ children }) => <Context.Provider value={mockValue}>{children}</Context.Provider>`. Test with real context or mock values.

249. **How do you test components that use Redux?**

**Answer:** Wrap with `Provider` from `react-redux`: `render(<Provider store={mockStore}><Component /></Provider>)`. Create mock store or use `@reduxjs/toolkit` test utilities. Or use `@testing-library/react` with Redux setup. Test component behavior, not Redux internals. Mock store for isolation.

250. **How do you mock API calls in tests?**

**Answer:** Methods: 1) Mock fetch: `global.fetch = jest.fn()`, 2) Use MSW (Mock Service Worker) - intercepts requests, 3) Mock axios, 4) Mock modules. MSW is recommended - more realistic. Example: `global.fetch = jest.fn(() => Promise.resolve({ json: () => ({ data: 'test' }) }))`.

251. **What is the purpose of `render` and `screen` in React Testing Library?**

**Answer:** `render` renders a component into a container (returns utilities and container). `screen` provides queries that search the entire document (recommended). Use `screen` for queries: `screen.getByText(...)`. `render` returns container and queries, but `screen` is preferred for simplicity.

252. **What are query methods in React Testing Library?**

**Answer:** Query methods find elements: `getBy*` (throws if not found), `queryBy*` (returns null), `findBy*` (async, waits), `getAllBy*` (returns array). Prefer accessible queries: `getByRole`, `getByLabelText`, `getByText`. Avoid `getByTestId` unless necessary. Queries prioritize accessibility.

### Testing Tools

253. **What is Cypress and when would you use it?**

**Answer:** Cypress is an E2E testing framework. Runs tests in a real browser, provides time-travel debugging, automatic waiting, and great DX. Use for: testing user flows, critical paths, integration between frontend/backend. Slower than unit tests but tests real user experience. Good for confidence in releases.

254. **What is Playwright and how does it compare to Cypress?**

**Answer:** Playwright is Microsoft's E2E testing framework. Comparison: Playwright supports multiple browsers (Chrome, Firefox, Safari), faster, better for CI/CD, can test multiple tabs. Cypress: better DX, time-travel, easier to learn, single browser focus. Both are excellent - choose based on needs.

255. **What is MSW (Mock Service Worker) and why is it useful?**

**Answer:** MSW intercepts network requests at the service worker level. Benefits: realistic API mocking, works in Node and browser, no code changes needed, can test error scenarios. More realistic than mocking fetch/axios. Use for: testing API integration, E2E tests with mocked APIs, or development.


---

## TypeScript with React

### TypeScript Basics

256. **What is TypeScript and why use it with React?**

**Answer:** TypeScript is JavaScript with static types. Benefits: catch errors at compile time, better IDE support (autocomplete, refactoring), self-documenting code, easier refactoring, and better team collaboration. Reduces bugs and improves developer experience. Popular in React projects.

257. **How do you set up TypeScript with React?**

**Answer:** Create React App: `npx create-react-app my-app --template typescript`. Or manually: install `typescript`, `@types/react`, `@types/react-dom`, create `tsconfig.json`. Next.js has TypeScript built-in. Vite: `npm create vite@latest my-app -- --template react-ts`. Most tools support TypeScript out of the box.

258. **What are the benefits of using TypeScript in React projects?**

**Answer:** Benefits: type safety (catch errors early), better autocomplete, refactoring confidence, self-documenting APIs, easier onboarding, and fewer runtime errors. Trade-offs: learning curve, more code to write, compilation step. Worth it for larger projects and teams.

### Typing React Components

259. **How do you type functional components in TypeScript?**

**Answer:** Define props interface: `interface Props { name: string }`. Type component: `function Component(props: Props) { ... }` or `const Component: React.FC<Props> = (props) => { ... }`. `React.FC` is optional - many prefer explicit return types. TypeScript infers return type from JSX.

260. **How do you type props in React components?**

**Answer:** Create interface: `interface ButtonProps { label: string; onClick: () => void; disabled?: boolean; }`. Use in component: `function Button({ label, onClick, disabled }: ButtonProps) { ... }`. Optional props use `?`. Can extend: `interface Props extends HTMLButtonElementProps { custom: string }`.

261. **How do you type state in React components?**

**Answer:** `useState` infers type from initial value: `const [count, setCount] = useState(0)` (number). Explicit: `useState<string | null>(null)`. For objects: `interface User { name: string }` then `useState<User | null>(null)`. TypeScript infers setter types automatically.

262. **How do you type event handlers in TypeScript?**

**Answer:** Use React types: `onChange={(e: React.ChangeEvent<HTMLInputElement>) => {}}`. For buttons: `onClick={(e: React.MouseEvent<HTMLButtonElement>) => {}}`. React provides types for all events. Can extract: `const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {}`.

263. **What is `React.FC` and should you use it?**

**Answer:** `React.FC` (FunctionComponent) types functional components. Includes `children` prop and return type. Many avoid it because: `children` is always included (even when not needed), harder to type props with generics, and explicit typing is clearer. Prefer: `function Component(props: Props) { ... }`.

264. **How do you type children in React components?**

**Answer:** Include in props: `interface Props { children: React.ReactNode }`. `React.ReactNode` accepts: elements, strings, numbers, fragments, arrays. More specific: `React.ReactElement` (single element) or `string` (only strings). `ReactNode` is most flexible and commonly used.

265. **How do you type refs in TypeScript?**

**Answer:** Use `useRef` with type: `const inputRef = useRef<HTMLInputElement>(null)`. Access: `inputRef.current?.focus()`. For component refs with `forwardRef`: `const Component = forwardRef<HTMLDivElement, Props>((props, ref) => <div ref={ref} />)`. Type the element or component being referenced.

266. **How do you type Hooks in TypeScript?**

**Answer:** Most Hooks infer types: `useState(0)` is `number`. Explicit: `useState<string | null>(null)`. `useRef<HTMLInputElement>(null)`. `useContext` needs typed context: `createContext<ContextType>(defaultValue)`. Custom Hooks: return type is inferred or explicit: `function useHook(): ReturnType { ... }`.

### Advanced TypeScript

267. **How do you create generic components in TypeScript?**

**Answer:** Use generics: `function List<T>({ items, render }: { items: T[]; render: (item: T) => React.ReactNode }) { ... }`. Or: `interface ListProps<T> { items: T[]; render: (item: T) => React.ReactNode }` then `function List<T>({ items, render }: ListProps<T>) { ... }`. Type is inferred from usage.

268. **How do you type Context API in TypeScript?**

**Answer:** Type the context value: `interface ContextType { user: User | null; setUser: (user: User) => void }`. Create: `const MyContext = createContext<ContextType | undefined>(undefined)`. Use: `const context = useContext(MyContext)` then check: `if (!context) throw new Error()`. Or provide default.

269. **How do you type Redux in TypeScript?**

**Answer:** Type actions: `interface Action { type: string; payload?: any }`. Type state: `interface RootState { ... }`. Type selectors: `const selectUser = (state: RootState) => state.user`. Redux Toolkit provides better types: `createSlice` auto-generates action types. Use `TypedUseSelectorHook` for hooks.

270. **What are utility types in TypeScript and how are they useful?**

**Answer:** Utility types transform types: `Partial<T>` (all optional), `Pick<T, K>` (select keys), `Omit<T, K>` (exclude keys), `Required<T>` (all required), `Readonly<T>`. Useful for: creating variations of types, making types flexible, and avoiding duplication. Example: `type PartialUser = Partial<User>`.

---

## Next.js

### Next.js Basics

271. **What is Next.js and why is it used?**

**Answer:** Next.js is a React framework for production. Features: SSR, SSG, API routes, file-based routing, automatic code splitting, image optimization, and built-in CSS support. Used for: better SEO, faster page loads, server-side rendering, and production-ready React apps. Simplifies React development.

272. **What are the advantages of Next.js over Create React App?**

**Answer:** Advantages: SSR/SSG (better SEO, performance), file-based routing (no React Router needed), API routes (backend in same project), automatic code splitting, image optimization, built-in CSS support, and production optimizations. CRA is simpler but Next.js is more powerful for production apps.

273. **What is the difference between client-side and server-side rendering?**

**Answer:** Client-side (CSR): JavaScript renders in browser, slower initial load, better interactivity. Server-side (SSR): HTML generated on server, faster initial load, better SEO, requires server. Next.js supports both. CSR: SPA experience. SSR: traditional web pages with React benefits.

274. **What is Static Site Generation (SSG)?**

**Answer:** SSG pre-renders pages at build time into static HTML. Pages are generated once, served as static files. Benefits: very fast, can be hosted on CDN, great SEO, secure. Use for: blogs, documentation, marketing sites. Next.js: `getStaticProps` generates pages at build time.

275. **What is Server-Side Rendering (SSR)?**

**Answer:** SSR renders pages on the server for each request. HTML is generated dynamically. Benefits: always fresh data, good SEO, fast initial load. Trade-off: requires server, slower than static. Use for: user-specific content, frequently changing data. Next.js: `getServerSideProps` runs on each request.

276. **What is Incremental Static Regeneration (ISR)?**

**Answer:** ISR (Next.js) combines SSG and SSR. Pages are statically generated but can be regenerated in the background. Set revalidation time: `getStaticProps` with `revalidate`. Benefits: static performance with dynamic updates. Best of both worlds: fast static pages that update periodically.

### Next.js Features

277. **What is the App Router in Next.js?**

**Answer:** App Router (Next.js 13+) uses `app` directory with file-based routing. Uses React Server Components by default, supports layouts, loading states, error boundaries, and nested routes. Modern approach with better data fetching and layouts. Replaces Pages Router for new projects.

278. **What is the Pages Router in Next.js?**

**Answer:** Pages Router (original) uses `pages` directory. Each file becomes a route. Uses `getStaticProps`, `getServerSideProps` for data fetching. Simpler but less flexible than App Router. Still supported and widely used. Good for existing projects or simpler needs.

279. **What is the difference between App Router and Pages Router?**

**Answer:** App Router: `app` directory, Server Components by default, layouts, better data fetching, nested routes. Pages Router: `pages` directory, client components, `getStaticProps`/`getServerSideProps`, simpler. App Router is newer and recommended for new projects. Pages Router is stable and mature.

280. **How do you create routes in Next.js?**

**Answer:** Pages Router: create files in `pages` directory (`pages/about.js` → `/about`). App Router: create folders in `app` directory (`app/about/page.js` → `/about`). Folders define routes, `page.js` is the route component. File-based routing - no configuration needed.

281. **What are API routes in Next.js?**

**Answer:** API routes are serverless functions in Next.js. Create in `pages/api` (Pages Router) or `app/api` (App Router). Example: `pages/api/users.js` exports handler function. Can handle GET, POST, etc. Build backend API alongside frontend. Deployed as serverless functions.

282. **How do you implement dynamic routes in Next.js?**

**Answer:** Pages Router: use brackets `[id].js` → `/users/[id]`. Access with `router.query.id`. App Router: `[id]` folder → `app/users/[id]/page.js`. Access with `params.id`. Both support catch-all: `[...slug].js` or `[[...slug]].js` for optional catch-all.

283. **What is `getStaticProps` and when is it used?**

**Answer:** `getStaticProps` (Pages Router) fetches data at build time for SSG. Runs on server during build, not in browser. Returns props to page component. Use for: data available at build time, static content, fast pages. Can use with `revalidate` for ISR.

284. **What is `getServerSideProps` and when is it used?**

**Answer:** `getServerSideProps` (Pages Router) fetches data on each request for SSR. Runs on server before rendering. Returns props to page. Use for: user-specific data, frequently changing data, or when you need request context (headers, cookies). Slower than SSG but always fresh.

285. **What is `getStaticPaths` and when is it used?**

**Answer:** `getStaticPaths` (Pages Router) defines which dynamic routes to pre-render at build time. Used with `getStaticProps` for dynamic SSG routes. Returns `paths` (which routes) and `fallback` (behavior for non-pre-rendered routes). Required for dynamic routes with SSG.

286. **How do you handle images in Next.js?**

**Answer:** Use `<Image>` component from `next/image`. Automatically optimizes: resizing, modern formats (WebP), lazy loading, and responsive images. Better than `<img>` tag. Example: `<Image src="/photo.jpg" width={500} height={300} alt="Photo" />`. Requires width/height or `fill` prop.

287. **What is Next.js Image component and why is it useful?**

**Answer:** `<Image>` component optimizes images automatically. Features: automatic format optimization (WebP/AVIF), lazy loading, responsive images, prevents layout shift, and CDN optimization. Improves performance and Core Web Vitals. Requires `next/image` import. Essential for production apps.

288. **How do you implement authentication in Next.js?**

**Answer:** Methods: 1) NextAuth.js (popular, handles OAuth, sessions), 2) Custom with JWT in API routes, 3) Third-party (Auth0, Clerk). Use middleware for protected routes. Store tokens in cookies or localStorage. NextAuth.js is recommended - handles complexity of auth.

289. **What is middleware in Next.js?**

**Answer:** Middleware (Next.js 12+) runs before requests complete. Create `middleware.js` in project root. Can: rewrite URLs, redirect, modify headers, or protect routes. Runs on edge runtime. Use for: authentication, A/B testing, geolocation, or request modification. Executes before page renders.

290. **How do you optimize performance in Next.js?**

**Answer:** Methods: 1) Use SSG/SSR appropriately, 2) Image optimization (`<Image>`), 3) Code splitting (automatic), 4) Dynamic imports, 5) API route optimization, 6) CDN for static assets, 7) Enable compression, 8) Monitor Core Web Vitals. Next.js handles many optimizations automatically.

---

## Build Tools

### Webpack

291. **What is Webpack and why is it used?**

**Answer:** Webpack is a module bundler. Bundles JavaScript, CSS, images, and other assets. Transforms code (JSX, TypeScript, Sass), optimizes bundles, and enables code splitting. Used in Create React App and many React projects. Handles dependencies and creates production-ready bundles.

292. **What is the purpose of Webpack in React applications?**

**Answer:** Purpose: bundle modules, transpile JSX/TypeScript, process CSS, optimize code (minification, tree shaking), enable code splitting, and handle assets (images, fonts). Transforms source code into browser-compatible bundles. Essential for modern React development workflow.

293. **What are Webpack loaders and plugins?**

**Answer:** Loaders transform files: `babel-loader` (JSX/ES6), `css-loader` (CSS), `file-loader` (assets). Plugins perform actions: `HtmlWebpackPlugin` (HTML), `MiniCssExtractPlugin` (CSS extraction). Loaders transform, plugins optimize and enhance. Both extend Webpack functionality.

294. **How do you configure Webpack for React?**

**Answer:** Create `webpack.config.js`. Configure: entry point, output, loaders (babel, css), plugins (HTML, CSS extraction), dev server, and optimization. Or use Create React App (pre-configured). Ejecting from CRA exposes config. Most developers use tools that hide Webpack complexity.

### Vite

295. **What is Vite and how does it differ from Webpack?**

**Answer:** Vite is a modern build tool. Differences: Vite uses native ES modules (faster dev server), esbuild for pre-bundling (faster), Rollup for production (smaller bundles). Webpack bundles everything. Vite is faster, especially for development. Both are excellent choices.

296. **What are the advantages of using Vite?**

**Answer:** Advantages: extremely fast dev server (native ESM), instant HMR, faster builds, smaller config, better out-of-the-box experience, and modern tooling. Faster than Webpack for development. Growing in popularity. Good alternative to Create React App.

297. **How do you set up Vite with React?**

**Answer:** Run: `npm create vite@latest my-app -- --template react`. Or manually: install `vite`, `@vitejs/plugin-react`, create `vite.config.js`. Start: `npm run dev`. Simple setup, fast development experience. Supports TypeScript, CSS preprocessors, and more.

298. **What is HMR (Hot Module Replacement)?**

**Answer:** HMR updates modules in browser without full page reload. Changes appear instantly, preserving component state. Faster than full refresh. Both Webpack and Vite support HMR. Vite's HMR is faster due to native ESM. Essential for good developer experience.

### Create React App

299. **What is Create React App (CRA)?**

**Answer:** CRA is a tool to create React apps with no build configuration. Sets up: Webpack, Babel, ESLint, and testing. Run: `npx create-react-app my-app`. Provides pre-configured setup. Good for learning and simple projects. Less recommended now (Vite/Next.js are preferred).

300. **What are the advantages and limitations of CRA?**

**Answer:** Advantages: zero config, easy start, well-documented, includes testing. Limitations: can't customize Webpack without ejecting, slower than Vite, larger bundle, and maintenance mode (not actively developed). Still works but Vite/Next.js are better choices for new projects.

301. **How do you eject from Create React App?**

**Answer:** Run: `npm run eject`. Irreversible - copies config files to project. Gives full control over Webpack config. Once ejected, can't go back. Consider alternatives: CRACO (customize without ejecting) or migrate to Vite/Next.js. Ejecting is rarely needed.

### Other Build Tools

302. **What is Parcel and how does it compare to Webpack?**

**Answer:** Parcel is a zero-config bundler. Comparison: Parcel requires no config (Webpack needs config), faster out of the box, simpler setup. Webpack: more flexible, larger ecosystem, more plugins. Parcel is good for simple projects. Webpack is more powerful but complex.

303. **What is esbuild and why is it fast?**

**Answer:** esbuild is a JavaScript bundler written in Go. Fast because: written in Go (compiled language), parallel processing, and no transformations by default. 10-100x faster than Webpack/Babel. Used by Vite for pre-bundling. Trade-off: less feature-complete than Webpack.

304. **What is SWC and how is it used with React?**

**Answer:** SWC (Speedy Web Compiler) is a Rust-based compiler. Replaces Babel for faster transpilation. Used by Next.js, Parcel. Faster than Babel (20x+). Compiles JSX, TypeScript, modern JavaScript. Growing adoption. Next.js uses SWC by default for faster builds.

---

## Authentication & Security

### Authentication

305. **How do you implement authentication in React applications?**

**Answer:** Methods: 1) JWT tokens (store in localStorage/cookies, send in headers), 2) Session-based (cookies, server sessions), 3) OAuth (third-party: Google, GitHub), 4) Libraries (NextAuth.js, Auth0). Flow: login → receive token → store → send with requests → protect routes. Use Context/state for auth state.

306. **What are JWT tokens and how are they used?**

**Answer:** JWT (JSON Web Token) is a compact token format. Contains: header, payload (user data), signature. Stateless - server doesn't store sessions. Flow: login → server returns JWT → client stores → sends in `Authorization: Bearer <token>` header. Decode to verify (don't store sensitive data).

307. **How do you store authentication tokens securely?**

**Answer:** Options: 1) httpOnly cookies (most secure, not accessible to JS, prevents XSS), 2) localStorage (accessible to JS, vulnerable to XSS), 3) sessionStorage (cleared on tab close). Best: httpOnly cookies for sensitive tokens. localStorage for non-sensitive data. Never store in regular cookies accessible to JS.

308. **What is the difference between authentication and authorization?**

**Answer:** Authentication: verifying who you are (login, identity). Authorization: verifying what you can do (permissions, roles). AuthN: "Are you logged in?" AuthZ: "Can you access this resource?" Both are needed. Example: login (authN) → check admin role (authZ) → access admin panel.

309. **How do you implement protected routes in React?**

**Answer:** Create wrapper component: `function ProtectedRoute({ children }) { const { isAuth } = useAuth(); return isAuth ? children : <Navigate to="/login" /> }`. Wrap routes: `<Route path="/dashboard" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />`. Or use route guard in router config.

310. **What are refresh tokens and how do you implement them?**

**Answer:** Refresh tokens are long-lived tokens used to get new access tokens. Access tokens are short-lived. Flow: access token expires → use refresh token to get new access token. Store refresh token securely (httpOnly cookie). Implement: API endpoint accepts refresh token, returns new access token.

311. **How do you handle token expiration?**

**Answer:** Methods: 1) Check expiration before requests, refresh if needed, 2) Intercept 401 responses, refresh token, retry request, 3) Use refresh tokens to get new access tokens, 4) Redirect to login if refresh fails. Use axios interceptors or fetch wrappers. Handle gracefully - don't break UX.

### Security

312. **What are common security vulnerabilities in React applications?**

**Answer:** Common vulnerabilities: XSS (cross-site scripting), CSRF (cross-site request forgery), insecure storage (tokens in localStorage), exposed API keys, SQL injection (if using backend), and dependency vulnerabilities. Always: sanitize input, use HTTPS, secure tokens, validate on server, and keep dependencies updated.

313. **What is XSS (Cross-Site Scripting) and how do you prevent it?**

**Answer:** XSS injects malicious scripts into pages. Prevent: 1) Never use `dangerouslySetInnerHTML` with user input, 2) Sanitize user input, 3) Use React's automatic escaping (safe by default), 4) Use libraries like DOMPurify, 5) Content Security Policy. React escapes by default, but be careful with `dangerouslySetInnerHTML`.

314. **What is CSRF (Cross-Site Request Forgery) and how do you prevent it?**

**Answer:** CSRF tricks users into performing actions they didn't intend. Prevent: 1) CSRF tokens (server generates, client sends), 2) SameSite cookies, 3) Verify origin/referer headers, 4) Use POST for state-changing operations. Backend handles most CSRF protection. Frontend: ensure tokens are sent with requests.

315. **How do you sanitize user input in React?**

**Answer:** Methods: 1) React escapes by default (safe), 2) Use DOMPurify for HTML: `import DOMPurify from 'dompurify'; const clean = DOMPurify.sanitize(userInput)`, 3) Validate input (regex, libraries like Yup/Zod), 4) Never trust client-side validation alone - validate on server. React is safe, but sanitize if using `dangerouslySetInnerHTML`.

316. **What is Content Security Policy (CSP)?**

**Answer:** CSP is a security header that restricts resources (scripts, styles, images) a page can load. Prevents XSS by whitelisting sources. Set via HTTP header or meta tag. Example: `Content-Security-Policy: default-src 'self'`. Controls what can execute/load on your page. Important security layer.

317. **How do you handle sensitive data in React applications?**

**Answer:** Never store in client code (visible to users). Methods: 1) Store in environment variables (`.env`, not committed), 2) Use backend API (server handles sensitive operations), 3) Encrypt if must store client-side, 4) Use secure storage (httpOnly cookies for tokens), 5) Never log sensitive data. Assume client code is public.

---

## API Integration

### Fetch API

318. **How do you make API calls in React?**

**Answer:** Methods: 1) `useEffect` with fetch/axios, 2) React Query (recommended for data fetching), 3) Custom Hooks, 4) Event handlers (on button click). Best practice: use `useEffect` for data on mount, React Query for complex scenarios. Handle loading, error, and success states.

319. **What is the Fetch API and how do you use it?**

**Answer:** Fetch is a native browser API for HTTP requests. Usage: `fetch('/api/data').then(res => res.json()).then(data => setData(data))`. Or with async/await: `const res = await fetch('/api/data'); const data = await res.json()`. Returns a Promise. Built into browsers, no library needed.

320. **What is the difference between Fetch and Axios?**

**Answer:** Fetch: native API, no library, returns Promises, manual error handling (check `res.ok`), no request cancellation (without AbortController). Axios: library, automatic JSON parsing, better error handling, request/response interceptors, request cancellation, and works in Node.js. Axios is more feature-rich.

321. **How do you handle errors in API calls?**

**Answer:** Methods: 1) Try/catch with async/await, 2) `.catch()` with Promises, 3) Check `res.ok` with fetch, 4) Axios catches HTTP errors automatically, 5) Use Error Boundaries for component errors. Display user-friendly messages. Log errors for debugging. Handle network errors separately.

322. **How do you handle loading states in API calls?**

**Answer:** Use state: `const [loading, setLoading] = useState(false)`. Set loading: `setLoading(true)` before request, `setLoading(false)` after. Display: `{loading ? <Spinner /> : <Content />}`. Or use React Query (handles loading automatically). Show loading indicators for better UX.

### Axios

323. **What is Axios and why is it used?**

**Answer:** Axios is a popular HTTP client library. Features: automatic JSON parsing, better error handling, interceptors, request cancellation, and works in browser and Node. Easier to use than fetch. Widely adopted. Good for: complex API interactions, authentication, and error handling.

324. **How do you set up Axios interceptors?**

**Answer:** Request interceptor: `axios.interceptors.request.use(config => { config.headers.Authorization = `Bearer ${token}`; return config; })`. Response interceptor: `axios.interceptors.response.use(res => res, error => { if (error.response?.status === 401) { // handle } })`. Interceptors run for all requests/responses.

325. **How do you handle authentication with Axios?**

**Answer:** Methods: 1) Interceptors: add token to headers automatically, 2) Default headers: `axios.defaults.headers.common['Authorization'] = 'Bearer ' + token`, 3) Per-request: `axios.get('/api', { headers: { Authorization: 'Bearer ' + token } })`. Interceptors are best for automatic token injection.

326. **How do you cancel requests with Axios?**

**Answer:** Use `AbortController` (or `CancelToken` in older Axios): `const controller = new AbortController(); axios.get('/api', { signal: controller.signal }); controller.abort()`. Or with `CancelToken`: `const source = axios.CancelToken.source(); axios.get('/api', { cancelToken: source.token }); source.cancel()`. Useful for cleanup.

### React Query / TanStack Query

327. **What is React Query (TanStack Query) and why is it used?**

**Answer:** React Query is a data-fetching library for React. Handles: server state, caching, synchronization, background updates, and error handling. Simplifies data fetching. Replaces manual `useEffect` + `useState` patterns. Essential for modern React apps with APIs. Now called TanStack Query.

328. **What are the advantages of using React Query?**

**Answer:** Advantages: automatic caching, background refetching, request deduplication, loading/error states, pagination support, infinite queries, optimistic updates, and devtools. Reduces boilerplate significantly. Makes data fetching declarative and efficient. Industry standard for React data fetching.

329. **How do you fetch data with React Query?**

**Answer:** Use `useQuery`: `const { data, isLoading, error } = useQuery('users', () => fetch('/api/users').then(res => res.json()))`. Or with query function: `useQuery(['users', id], () => getUser(id))`. Handles loading, error, and caching automatically. Key is used for caching.

330. **What is caching in React Query?**

**Answer:** React Query caches query results by key. Same key = cached data (no refetch). Configurable: `staleTime` (how long data is fresh), `cacheTime` (how long to keep in cache). Automatic background refetching when data is stale. Prevents unnecessary requests and improves performance.

331. **How do you handle mutations with React Query?**

**Answer:** Use `useMutation`: `const mutation = useMutation(newUser => createUser(newUser), { onSuccess: () => { queryClient.invalidateQueries('users') } })`. Call: `mutation.mutate(userData)`. Handles loading/error states. Use `invalidateQueries` to refetch related data after mutation.

332. **What is the difference between `useQuery` and `useMutation`?**

**Answer:** `useQuery`: for fetching/reading data, runs automatically, cached, can refetch. `useMutation`: for creating/updating/deleting, runs manually (call `mutate()`), not cached, handles side effects. Use `useQuery` for GET requests, `useMutation` for POST/PUT/DELETE. Both handle loading/error states.

333. **How do you handle pagination with React Query?**

**Answer:** Use `useQuery` with page in key: `useQuery(['users', page], () => fetchUsers(page))`. Or use `useInfiniteQuery` for infinite scroll. Update page state, React Query fetches new page. Can prefetch next page. `keepPreviousData: true` keeps previous data while loading next page.

334. **How do you handle infinite scrolling with React Query?**

**Answer:** Use `useInfiniteQuery`: `const { data, fetchNextPage, hasNextPage } = useInfiniteQuery('users', ({ pageParam = 0 }) => fetchUsers(pageParam), { getNextPageParam: (lastPage) => lastPage.nextPage })`. Call `fetchNextPage()` on scroll. Automatically manages pages and loading states.

### GraphQL

335. **What is GraphQL and how does it differ from REST?**

**Answer:** GraphQL is a query language for APIs. Differences: GraphQL has single endpoint, client specifies needed fields, strong typing, and can fetch related data in one request. REST: multiple endpoints, server decides response, less flexible. GraphQL: more efficient, over-fetching prevention. REST: simpler, caching easier.

336. **How do you use GraphQL with React?**

**Answer:** Use a GraphQL client: Apollo Client or Relay. Apollo: `const { data } = useQuery(gql\`query { users { name } }\`)`. Relay: uses fragments and queries. Both handle caching, loading states, and mutations. GraphQL queries are declarative. Fetch exactly what you need.

337. **What is Apollo Client and how does it work?**

**Answer:** Apollo Client is a GraphQL client for React. Features: caching, loading states, mutations, subscriptions, and DevTools. Setup: wrap app with `ApolloProvider`, use `useQuery`/`useMutation` Hooks. Automatically caches and normalizes data. Most popular GraphQL client for React.

338. **What is Relay and how does it compare to Apollo?**

**Answer:** Relay is Facebook's GraphQL client. Comparison: Relay requires GraphQL schema, uses fragments/colocation, more opinionated, better performance. Apollo: more flexible, easier to learn, larger community, works with any GraphQL server. Apollo is more popular, Relay is more performant for large apps.

---

## Advanced Patterns

### Higher-Order Components (HOCs)

339. **What are Higher-Order Components (HOCs) in React?**

**Answer:** HOCs are functions that take a component and return a new component with additional functionality. Pattern: `const EnhancedComponent = withHOC(BaseComponent)`. Used for: code reuse, cross-cutting concerns, and adding props/behavior. Common before Hooks. Still used but Hooks are preferred.

340. **How do you create a HOC?**

**Answer:** Function that takes component, returns new component: `function withAuth(Component) { return function AuthenticatedComponent(props) { if (!isAuth) return <Login />; return <Component {...props} /> } }`. Or arrow: `const withAuth = Component => props => isAuth ? <Component {...props} /> : <Login />`. Pass through props.

341. **What are the use cases for HOCs?**

**Answer:** Use cases: authentication (protect components), logging/analytics, data fetching, styling/theming, and code reuse. HOCs wrap components to add functionality. Example: `withRouter`, `connect` (Redux). Less common now - Hooks and custom Hooks replace many HOC use cases.

342. **What are the limitations of HOCs?**

**Answer:** Limitations: wrapper hell (nested HOCs), props collision, harder to debug, and static composition. Can create deep component trees. Hooks solve these issues: no wrapper hell, easier to compose, and better debugging. HOCs still work but Hooks are preferred for new code.

343. **How do HOCs compare to Hooks?**

**Answer:** HOCs: class-based pattern, wrapper components, harder to compose, props-based. Hooks: functional, no wrappers, easier to compose, direct API access. Hooks are preferred: simpler, more flexible, better performance, and easier to test. HOCs are legacy pattern, still supported.

### Render Props

344. **What is the render props pattern?**

**Answer:** Render props pass a function as a prop that returns JSX. Component calls the function with data: `<DataProvider render={data => <Display data={data} />} />`. Or `children` as function: `<DataProvider>{data => <Display data={data} />}</DataProvider>`. Enables sharing logic between components.

345. **How does render props differ from HOCs?**

**Answer:** Render props: function prop, dynamic composition, explicit data flow. HOCs: wrapper component, static composition, implicit props. Render props are more flexible and explicit. Both solve similar problems (code reuse). Hooks replace both patterns in most cases.

346. **What are the advantages and disadvantages of render props?**

**Answer:** Advantages: flexible, explicit data flow, no wrapper components, easy to understand. Disadvantages: callback hell (nested functions), less clean JSX, and performance concerns (new function each render). Hooks provide similar benefits without the disadvantages.

347. **When would you use render props over Hooks?**

**Answer:** Rarely needed now. Use render props if: working with class components that can't use Hooks, or library API requires it. Hooks are preferred: simpler, better performance, and more React-idiomatic. Render props are legacy pattern. Prefer custom Hooks.


### Compound Components

348. **What are compound components?**

**Answer:** Compound components are components that work together to form a complete UI. Example: `<Select><Select.Option>One</Select.Option><Select.Option>Two</Select.Option></Select>`. Components share implicit state through Context. Flexible API, good for component libraries. Used in libraries like Reach UI.

349. **How do you implement compound components?**

**Answer:** Use Context to share state: `const SelectContext = createContext()`. Parent provides context, children consume it. Example: `<Select>` provides state, `<Select.Option>` reads state. Can use `children` manipulation or Context API. Enables flexible composition while maintaining shared state.

350. **What are the advantages of compound components?**

**Answer:** Advantages: flexible API (users compose as needed), good separation of concerns, reusable patterns, and intuitive API. Users have control over structure. Good for component libraries. Example: `<Modal><Modal.Header /><Modal.Body /><Modal.Footer /></Modal>`. More flexible than single component.


### Portals

351. **What are React Portals?**

**Answer:** Portals render children into a DOM node outside the component tree. Syntax: `createPortal(children, domNode)`. Useful for: modals, tooltips, dropdowns that need to escape parent overflow/z-index. Renders in different DOM location but maintains React tree (events bubble to React tree).

352. **When would you use Portals?**

**Answer:** Use for: modals (escape z-index issues), tooltips (escape overflow hidden), dropdowns (escape clipping), and any UI that needs to render outside parent. Solves CSS issues (z-index, overflow). Events still work normally (React handles event delegation). Essential for overlay components.

353. **How do you create a Portal in React?**

**Answer:** Import: `import { createPortal } from 'react-dom'`. Use: `return createPortal(<Modal />, document.body)`. Or create container: `const portalRoot = document.getElementById('portal-root')` then `createPortal(children, portalRoot)`. Children render in target DOM node, React tree preserved.


### Error Boundaries

354. **What are Error Boundaries in React?**

**Answer:** Error Boundaries catch JavaScript errors in child component tree. Class component with `componentDidCatch` or `getDerivedStateFromError`. Prevents entire app from crashing. Displays fallback UI. Can't use Hooks - must be class component. Catches errors during render, lifecycle, constructors.

355. **How do you create an Error Boundary?**

**Answer:** Class component with error methods: `class ErrorBoundary extends React.Component { state = { hasError: false }; static getDerivedStateFromError(error) { return { hasError: true }; } componentDidCatch(error, info) { logError(error, info); } render() { if (this.state.hasError) return <Fallback />; return this.props.children; } }`.

356. **What errors can Error Boundaries catch?**

**Answer:** Catches: errors in render, lifecycle methods, constructors of child components. Does NOT catch: event handlers, async code (setTimeout, promises), server-side rendering, or errors in the boundary itself. Use try/catch for those. Boundaries catch rendering errors.

357. **What errors cannot be caught by Error Boundaries?**

**Answer:** Cannot catch: event handlers (use try/catch), async code (promises, setTimeout), errors during server-side rendering, errors in the boundary itself, or errors in error handling code. Use regular try/catch for these. Boundaries only catch errors during React rendering.

358. **How do you handle errors in functional components?**

**Answer:** Functional components can't be Error Boundaries (must be class). Options: 1) Wrap in class Error Boundary, 2) Use try/catch in event handlers/effects, 3) Use error handling libraries, 4) Handle in parent class component. For async: `useEffect(() => { try { await api() } catch(e) { setError(e) } }, [])`.


### Code Splitting

359. **What is code splitting and why is it important?**

**Answer:** Code splitting divides code into smaller chunks loaded on demand. Important because: reduces initial bundle size, faster initial load, better performance, and users only download what they need. Improves Time to Interactive (TTI) and First Contentful Paint (FCP). Essential for large apps.

360. **How do you implement code splitting in React?**

**Answer:** Use `React.lazy`: `const Component = React.lazy(() => import('./Component'))`. Wrap with `Suspense`: `<Suspense fallback={<Loading />}><Component /></Suspense>`. Or dynamic imports: `import('./module').then(module => ...)`. Webpack automatically creates separate chunks. Loads on first render.

361. **What is dynamic import and how does it work?**

**Answer:** Dynamic import: `import('./module')` returns a Promise. Loads module on demand, not at initial load. Syntax: `const module = await import('./module')` or `import('./module').then(module => ...)`. Webpack creates separate chunk. Used by `React.lazy` internally. Enables code splitting.

362. **What is route-based code splitting?**

**Answer:** Split code by routes - each route loads separately. Example: `const Home = lazy(() => import('./Home'))`, `const About = lazy(() => import('./About'))`. Each route is a separate chunk. Users only download route code when visiting. Most common splitting strategy. Improves initial load significantly.

---

## Error Handling

363. **How do you handle errors in React applications?**

**Answer:** Methods: 1) Error Boundaries (rendering errors), 2) try/catch (event handlers, async), 3) Promise `.catch()`, 4) Error state in components, 5) Global error handlers (`window.onerror`), 6) Error reporting services. Use appropriate method for error type. Always show user-friendly messages.

364. **What is the difference between Error Boundaries and try-catch?**

**Answer:** Error Boundaries: catch errors in child components during render, class components only, show fallback UI, prevent app crash. try/catch: catch errors in regular code, works everywhere, handle programmatically. Use Boundaries for rendering errors, try/catch for everything else. Complementary, not replacements.

365. **How do you handle async errors in React?**

**Answer:** Methods: 1) try/catch with async/await: `try { await api() } catch(e) { setError(e) }`, 2) `.catch()` with Promises, 3) Error state: `const [error, setError] = useState(null)`, 4) Error Boundaries don't catch async - use try/catch. Handle in `useEffect` or event handlers.

366. **How do you log errors in React applications?**

**Answer:** Methods: 1) `console.error()` (development), 2) Error reporting services (Sentry, LogRocket, Bugsnag), 3) Server logging (send to backend), 4) `componentDidCatch` in Error Boundaries, 5) Global handlers. Production: use error reporting services. Development: console is fine. Always log with context.

367. **What is error reporting and how do you implement it?**

**Answer:** Error reporting tracks errors in production. Services: Sentry (popular), LogRocket, Bugsnag. Setup: install SDK, initialize, errors automatically reported. Provides: error tracking, stack traces, user context, and alerts. Essential for production apps. Helps debug issues users encounter.

368. **How do you create a global error handler in React?**

**Answer:** Methods: 1) `window.onerror` (global JS errors), 2) `window.onunhandledrejection` (unhandled promises), 3) Error Boundary at root, 4) Error reporting service initialization. Example: `window.onerror = (msg, url, line) => { logError(msg, url, line) }`. Catches errors outside React.

---

## Accessibility

369. **What is accessibility in web development?**

**Answer:** Accessibility (a11y) ensures websites are usable by everyone, including people with disabilities. Includes: screen readers, keyboard navigation, color contrast, and semantic HTML. Legal requirement in many places. Makes apps better for all users. WCAG provides guidelines.

370. **Why is accessibility important in React applications?**

**Answer:** Important because: legal compliance (ADA, Section 508), larger audience, better UX for all, SEO benefits, and ethical responsibility. Accessible apps work for: screen readers, keyboard-only users, low vision, and motor impairments. React can help or hurt accessibility - must be intentional.

371. **What are ARIA attributes and how do you use them?**

**Answer:** ARIA (Accessible Rich Internet Applications) attributes enhance accessibility. Examples: `aria-label` (descriptive label), `aria-labelledby` (reference to label), `aria-hidden` (hide from screen readers), `role` (semantic role). Use when HTML semantics aren't enough. Don't overuse - prefer semantic HTML.

372. **How do you make React components accessible?**

**Answer:** Methods: 1) Semantic HTML (`<button>`, `<nav>`, not `<div>`), 2) ARIA attributes when needed, 3) Keyboard navigation, 4) Focus management, 5) Color contrast, 6) Alt text for images, 7) Form labels. Test with screen readers and keyboard. Use `eslint-plugin-jsx-a11y`.

373. **What is semantic HTML and why is it important?**

**Answer:** Semantic HTML uses elements that convey meaning: `<header>`, `<nav>`, `<main>`, `<article>`, `<button>` (not `<div onClick>`). Important because: screen readers understand structure, better SEO, clearer code, and built-in accessibility. Prefer semantic elements over generic `<div>`/`<span>`.

374. **How do you handle keyboard navigation in React?**

**Answer:** Methods: 1) Use semantic elements (built-in keyboard support), 2) `onKeyDown` handlers: `onKeyDown={(e) => e.key === 'Enter' && handleClick()}`, 3) `tabIndex` for focusable elements, 4) Arrow keys for custom components, 5) Focus traps for modals. Ensure all interactive elements are keyboard accessible.

375. **What is focus management in React?**

**Answer:** Focus management controls which element has keyboard focus. Methods: 1) `ref.current.focus()` to focus elements, 2) Focus traps (keep focus in modal), 3) Return focus on close, 4) `autoFocus` prop, 5) `useRef` to access DOM. Important for: modals, dropdowns, and keyboard navigation. Improves UX.

376. **How do you test accessibility in React applications?**

**Answer:** Methods: 1) Automated: `axe-core`, `eslint-plugin-jsx-a11y`, `@testing-library` (queries prioritize accessibility), 2) Manual: keyboard navigation, screen readers (NVDA, JAWS, VoiceOver), 3) Tools: WAVE, Lighthouse, 4) User testing. Test throughout development, not just at end.

377. **What are the WCAG guidelines?**

**Answer:** WCAG (Web Content Accessibility Guidelines) provides accessibility standards. Levels: A (minimum), AA (recommended), AAA (enhanced). Principles: Perceivable, Operable, Understandable, Robust. Covers: color contrast, keyboard access, screen readers, and more. AA level is common target for compliance.

378. **How do you make forms accessible in React?**

**Answer:** Methods: 1) `<label>` for inputs (`htmlFor` and `id`), 2) Error messages with `aria-describedby`, 3) Required fields with `aria-required`, 4) Group related fields (`<fieldset>`), 5) Clear error messages, 6) Keyboard accessible. Example: `<label htmlFor="email">Email</label><input id="email" aria-required="true" />`.

---

## Deployment

### Build Process

379. **How do you build a React application for production?**

**Answer:** Run build command: `npm run build` (Create React App) or `npm run build` (Vite/Next.js). Creates optimized `build` or `dist` folder with: minified code, optimized assets, and production-ready files. Deploy this folder to hosting. Build process: transpiles, minifies, optimizes, and bundles.

380. **What is the difference between development and production builds?**

**Answer:** Development: unminified, source maps, hot reload, larger bundles, debug info, slower. Production: minified, no source maps (or separate), optimized, smaller bundles, no debug code, faster. Production builds are optimized for performance and size. Development builds prioritize DX.

381. **How do you optimize a React build?**

**Answer:** Methods: 1) Code splitting, 2) Tree shaking (remove unused code), 3) Minification, 4) Compression (gzip/brotli), 5) Image optimization, 6) Analyze bundle (find large dependencies), 7) Remove unused dependencies, 8) Use production mode. Most build tools handle this automatically.

382. **What are environment variables and how do you use them?**

**Answer:** Environment variables store config values. Create React App: `.env` file, prefix with `REACT_APP_`: `REACT_APP_API_URL=...`. Access: `process.env.REACT_APP_API_URL`. Vite: `VITE_` prefix. Next.js: `NEXT_PUBLIC_` prefix. Never commit `.env` with secrets. Use for API URLs, feature flags.

### Deployment Platforms

383. **How do you deploy a React application to Vercel?**

**Answer:** Methods: 1) Connect GitHub repo (automatic deploys), 2) Vercel CLI: `vercel`, 3) Drag and drop build folder. Vercel detects React, configures automatically. Provides: CDN, HTTPS, custom domains, and preview deployments. Best for: Next.js, but works with any React app. Free tier available.

384. **How do you deploy a React application to Netlify?**

**Answer:** Methods: 1) Connect GitHub (auto-deploy), 2) Netlify CLI: `netlify deploy`, 3) Drag and drop. Configure: build command (`npm run build`), publish directory (`build`). Provides: CDN, HTTPS, forms, and functions. Good for: static React apps. Free tier available. Simple setup.

385. **How do you deploy a React application to AWS?**

**Answer:** Options: 1) S3 + CloudFront (static hosting), 2) Amplify (full-stack, easier), 3) EC2 (server), 4) Elastic Beanstalk. Amplify: connect repo, auto-deploys. S3: upload build folder, configure CloudFront. More complex but more control. AWS has learning curve but powerful.

386. **How do you deploy a React application using Docker?**

**Answer:** Create `Dockerfile`: `FROM nginx:alpine`, `COPY build /usr/share/nginx/html`. Build: `docker build -t react-app .`. Run: `docker run -p 80:80 react-app`. Or multi-stage: build in Node, serve with nginx. Deploy to: Docker Hub, AWS ECS, Kubernetes. Containerizes app for consistent deployment.

387. **What is CI/CD and how do you set it up for React applications?**

**Answer:** CI/CD (Continuous Integration/Continuous Deployment) automates testing and deployment. Setup: 1) GitHub Actions (`.github/workflows`), 2) GitLab CI, 3) CircleCI, 4) Jenkins. Flow: push code → run tests → build → deploy. Services: GitHub Actions (free for public repos), Vercel/Netlify (built-in). Automates releases.

### Performance in Production

388. **How do you monitor performance in production?**

**Answer:** Methods: 1) Google Analytics, 2) Real User Monitoring (RUM) tools, 3) Lighthouse CI, 4) Web Vitals library, 5) Custom performance APIs (`PerformanceObserver`), 6) Error tracking (Sentry includes performance). Monitor: load times, Core Web Vitals, errors, and user experience. Essential for optimization.

389. **What are Core Web Vitals?**

**Answer:** Core Web Vitals are Google's metrics for user experience: LCP (Largest Contentful Paint - loading), FID (First Input Delay - interactivity), CLS (Cumulative Layout Shift - visual stability). New metrics: FCP, TTI. Google uses for SEO ranking. Target: LCP < 2.5s, FID < 100ms, CLS < 0.1.

390. **How do you optimize Core Web Vitals in React applications?**

**Answer:** LCP: optimize images, reduce render-blocking, use CDN, code splitting. FID: reduce JavaScript, optimize event handlers, use Web Workers. CLS: set image dimensions, avoid inserting content above fold, use `font-display: swap`. Use React best practices: code splitting, lazy loading, memoization.

391. **What is lazy loading and how does it improve performance?**

**Answer:** Lazy loading loads resources (components, images) only when needed. Improves: initial bundle size, Time to Interactive, and First Contentful Paint. Users download less upfront. Implement: `React.lazy()` for components, `loading="lazy"` for images. Essential for large apps. Significant performance gain.

392. **How do you implement service workers in React?**

**Answer:** Methods: 1) Workbox (Google's tool, recommended), 2) `create-react-app` includes service worker, 3) Manual setup: register in `index.js`, create `service-worker.js`. Use for: offline support, caching, push notifications, and background sync. Workbox simplifies implementation. Enables PWA features.

---

## Miscellaneous

393. **What is the difference between React and React Native?**

**Answer:** React: web framework, renders to DOM, uses HTML/CSS, browser-based. React Native: mobile framework, renders to native components, uses native APIs, iOS/Android apps. Both: same concepts (components, props, state, Hooks), JSX syntax, and React patterns. React Native uses React but different rendering.

394. **What is the React ecosystem?**

**Answer:** React ecosystem includes: React core, React DOM, React Native, state management (Redux, Zustand), routing (React Router), forms (React Hook Form), testing (Jest, RTL), build tools (Webpack, Vite), frameworks (Next.js, Remix), and thousands of libraries. Large, active community and ecosystem.

395. **What are the latest features in React 18?**

**Answer:** React 18 features: Concurrent rendering, automatic batching, `startTransition`, `useDeferredValue`, Suspense improvements, `useId`, `useSyncExternalStore`, `useInsertionEffect`, and Server Components (experimental). Focus: better performance and user experience. Backward compatible - gradual adoption.

396. **What is Server Components in React?**

**Answer:** Server Components (React 18+, experimental) render on server, send to client. Benefits: zero bundle size, direct database access, secure (secrets on server), and faster. Can't use: state, effects, browser APIs. Use for: data fetching, static content. Client Components for interactivity. Next.js 13+ uses them.

397. **What is the difference between Server Components and Client Components?**

**Answer:** Server Components: render on server, no JavaScript sent, can't use Hooks/state, direct DB access, secure. Client Components: render in browser, JavaScript required, can use Hooks/state, browser APIs. Server: `async function Component()`. Client: `'use client'` directive (Next.js). Use both appropriately.

398. **How do you handle internationalization (i18n) in React?**

**Answer:** Libraries: 1) `react-i18next` (popular, i18next), 2) `react-intl` (FormatJS), 3) `next-intl` (Next.js). Setup: translation files (JSON), provider component, use translation hooks: `const { t } = useTranslation()`. Handle: text, dates, numbers, pluralization. Essential for global apps.

399. **What are React design patterns?**

**Answer:** Common patterns: Container/Presentational, Hooks pattern, Compound Components, Render Props, HOCs, Controlled/Uncontrolled components, Lifting State Up, Composition over Inheritance, and Custom Hooks. Patterns solve common problems: code reuse, state management, and component organization. Learn patterns for better code.

400. **What are best practices for React development?**

**Answer:** Best practices: 1) Functional components + Hooks, 2) Keep components small, 3) Extract custom Hooks, 4) Use TypeScript, 5) Test components, 6) Optimize performance (memo, useMemo, useCallback when needed), 7) Accessibility, 8) Code splitting, 9) Error boundaries, 10) Follow React patterns. Write maintainable, performant code.

---

## Conclusion

This comprehensive list covers all major topics from the React Developer Roadmap. These questions range from fundamental concepts to advanced topics, helping you prepare for React interviews at any level.

**Good luck with your React interview preparation!**

---

*Based on the React Developer Roadmap from [roadmap.sh](https://roadmap.sh/react)*

