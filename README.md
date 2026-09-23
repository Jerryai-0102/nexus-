# � Complete Interview Preparation Guide
## React, JavaScript, TypeScript & Web Development Concepts

---

## 📋 Table of Contents

1. [React Core Concepts](#react-core-concepts)
2. [React Hooks](#react-hooks)
3. [State Management](#state-management)
4. [Performance Optimization](#performance-optimization)
5. [JavaScript Fundamentals](#javascript-fundamentals)
6. [TypeScript](#typescript)
7. [DOM & Browser APIs](#dom--browser-apis)
8. [Event Handling](#event-handling)
9. [Async Programming](#async-programming)
10. [Design Patterns](#design-patterns)
11. [Build Tools & Bundlers](#build-tools--bundlers)
12. [Testing](#testing)
13. [Web Performance](#web-performance)
14. [Security](#security)
15. [Advanced React](#advanced-react)

---

## React Core Concepts

### Q1: What is React and why use it?
**Answer**: React is a JavaScript library for building user interfaces, particularly single-page applications. Key benefits include component-based architecture for code reusability, virtual DOM for efficient updates, unidirectional data flow for predictable state management, large ecosystem and community support, and excellent developer experience with tools like React DevTools. It focuses on the view layer and can integrate with other libraries.

### Q2: Explain Virtual DOM and how it works
**Answer**: Virtual DOM is a lightweight JavaScript representation of the actual DOM. When state changes, React creates a new virtual DOM tree, compares it with the previous one using a diffing algorithm, calculates the minimum changes needed, and updates only those specific parts of the real DOM. This process is called reconciliation. It's faster than direct DOM manipulation because DOM operations are expensive, while JavaScript object operations are cheap. React batches multiple updates together for efficiency.

### Q3: What is JSX and why do we use it?
**Answer**: JSX is a syntax extension that looks like HTML but is actually JavaScript. It gets transpiled to React.createElement calls. Benefits include better readability, type checking at compile time, prevention of injection attacks by escaping values, and familiar HTML-like syntax. JSX is not mandatory but recommended because it makes component structure clearer and catches errors during compilation rather than runtime.

### Q4: Controlled vs Uncontrolled components
**Answer**: Controlled components have their form data controlled by React state - every state mutation has an associated handler function, making React the single source of truth. Uncontrolled components store their own state internally in the DOM, accessed via refs. Controlled components offer better validation, conditional disabling, dynamic inputs, and enforcing formats. Uncontrolled are useful for file inputs or when integrating with non-React code. Most applications should use controlled components.


### Q5: What is reconciliation in React?
**Answer**: Reconciliation is the process React uses to update the DOM efficiently. When component state changes, React creates a new virtual DOM tree and compares it with the previous tree. It uses a diffing algorithm with two assumptions: elements of different types produce different trees, and developer can hint which child elements may be stable with a key prop. React then updates only the changed parts. This makes updates fast because it minimizes expensive DOM operations.

### Q6: Explain the component lifecycle
**Answer**: React components go through three phases: Mounting (component created and inserted into DOM), Updating (component re-renders due to props or state changes), and Unmounting (component removed from DOM). In class components, lifecycle methods include componentDidMount, componentDidUpdate, componentWillUnmount. In functional components, useEffect hook handles all lifecycle phases. The cleanup function in useEffect acts like componentWillUnmount. Dependencies array controls when effects run.

### Q7: What is the difference between Element and Component?
**Answer**: An Element is a plain object describing what should appear on screen - it's the return value of JSX or React.createElement. Elements are immutable and represent the DOM at a specific point in time. A Component is a function or class that accepts props and returns Elements. Components can be reused, maintain state, and have lifecycle methods. Think of Elements as the building blocks and Components as the blueprints.

### Q8: Props vs State - explain the difference
**Answer**: Props are inputs to components, passed from parent to child, immutable from the child's perspective, and used to configure components. State is internal to a component, mutable via setState or useState, determines component behavior, and when changed triggers re-renders. Props flow down (unidirectional data flow), while state is local. Props make components reusable, state makes them interactive. A component can convert props to state if needed.

### Q9: What is prop drilling and how to avoid it?
**Answer**: Prop drilling occurs when you pass props through multiple layers of components that don't need them, just to reach a deeply nested component. Problems include cluttered component APIs, maintenance difficulty, and tight coupling. Solutions include Context API for global state, component composition (passing children), custom hooks for shared logic, state management libraries like Redux or Zustand, and render props pattern. Choose based on how many components need the data.

### Q10: Explain React.Fragment and why it's useful
**Answer**: Fragment lets you group multiple elements without adding extra nodes to the DOM. Useful because React requires single root element, but sometimes you don't want wrapper divs for styling or semantic reasons. Fragments don't affect layout, DOM structure, or CSS selectors. They support key prop for lists but not other props. Short syntax is empty tags. Fragments help keep DOM clean and avoid CSS inheritance issues.


---

## React Hooks

### Q11: What are React Hooks and why were they introduced?
**Answer**: Hooks are functions that let you use state and lifecycle features in functional components. Introduced in React 16.8 to solve problems like hard-to-reuse stateful logic, complex components with lifecycle methods, confusion with classes and "this" keyword. Benefits include easier code sharing via custom hooks, better code organization, smaller bundle sizes, and no breaking changes to existing code. Hooks follow rules: only call at top level, only call from React functions.

### Q12: Explain useState in detail
**Answer**: useState adds state to functional components. Takes initial value, returns array with current state and updater function. Updater can take new value or function receiving previous state. State updates are asynchronous and batched for performance. Updater function triggers re-render. Functional updates important when new state depends on previous state to avoid stale closures. Can have multiple useState calls in one component. Initial value only used on first render.

### Q13: Explain useEffect and its use cases
**Answer**: useEffect runs side effects after render. Takes function and optional dependency array. Runs after every render by default, but dependencies control when it runs. Empty array means run once on mount. Return cleanup function for subscriptions, timers, or listeners. Use cases include data fetching, subscriptions, manual DOM changes, logging, setting up timers. Replaces componentDidMount, componentDidUpdate, and componentWillUnmount. Multiple useEffects better than one complex effect.

### Q14: What is the difference between useEffect and useLayoutEffect?
**Answer**: useEffect runs asynchronously after paint, doesn't block browser painting, suitable for most side effects. useLayoutEffect runs synchronously after DOM mutations but before paint, blocks visual updates, useful for DOM measurements or preventing flicker when updating styles. Use useLayoutEffect when you need to read layout or synchronously re-render. UseEffect is better for performance in most cases since it doesn't block painting.

### Q15: Explain useContext and when to use it
**Answer**: useContext accesses Context value without wrapping components. Takes Context object and returns current context value. Simpler than Consumer component syntax. Component using useContext re-renders when context value changes. Use for global data like theme, user info, or language. Avoid overuse as it can make components less reusable. Combine with useMemo to optimize. Better than prop drilling but consider if you really need global state first.

### Q16: What is useRef and its use cases?
**Answer**: useRef returns mutable object whose current property persists across renders. Doesn't trigger re-render when changed. Use cases include accessing DOM elements, storing mutable values that don't need to trigger renders, keeping previous values, storing timer IDs, and preventing infinite loops. Different from state because changes don't cause re-renders and updates are synchronous. Common pattern: useRef for tracking, useState for displaying.

### Q17: Explain useMemo and when to use it
**Answer**: useMemo memoizes expensive calculations, recomputes only when dependencies change. Returns memoized value. Use for computationally expensive operations, referential equality for objects passed to children, or preventing unnecessary re-renders of child components. Don't overuse as it adds overhead. React may discard memoized values to free memory. Not for side effects - use useEffect instead. Compare with useCallback which memoizes functions.

### Q18: What is useCallback and when is it useful?
**Answer**: useCallback memoizes function references, returns same function instance unless dependencies change. Prevents child component re-renders when passed as prop. Useful when passing callbacks to optimized child components using React.memo, in dependency arrays of other hooks, or with expensive inline functions. Every render creates new function, but useCallback prevents this. Similar to useMemo but specifically for functions.

### Q19: Explain useReducer and when to prefer it over useState
**Answer**: useReducer is alternative to useState for complex state logic. Takes reducer function and initial state, returns current state and dispatch function. Prefer when state has complex updates, multiple sub-values, next state depends on previous state, or when you want to optimize performance by passing dispatch instead of callbacks. Similar to Redux pattern. Easier to test state logic. Good for state machines. UseState simpler for independent values.

### Q20: What are custom hooks and how to create them?
**Answer**: Custom hooks extract reusable logic from components. Functions starting with "use" that can call other hooks. Enable sharing stateful logic without changing component hierarchy. Benefits include code reuse, separation of concerns, easier testing, and cleaner components. Examples include useFetch for data fetching, useLocalStorage for persistence, useWindowSize for responsive logic. Follow hook rules. Can compose multiple hooks together. Better than HOCs or render props in most cases.

### Q21: Explain the rules of hooks
**Answer**: Two main rules enforced by ESLint plugin. First: only call hooks at top level, not inside loops, conditions, or nested functions - ensures hooks called in same order every render, critical for React's internal tracking. Second: only call hooks from React functions (components or custom hooks), not regular JavaScript functions. This maintains predictable behavior. Breaking rules causes bugs because React relies on call order to associate state with components.

### Q22: What is useImperativeHandle?
**Answer**: useImperativeHandle customizes instance value exposed when using ref. Works with forwardRef to expose specific methods to parent. Use cases include focusing inputs, triggering animations, or accessing third-party library methods. Lets parent control child behavior imperatively. Should be avoided when possible as it breaks React's declarative pattern. Better to use props and state. Useful for specific cases like form libraries or animation libraries.

### Q23: Explain useDebugValue
**Answer**: useDebugValue displays label for custom hooks in React DevTools. Takes value and optional formatter function. Only works in custom hooks, not regular components. Useful for complex custom hooks where internal state is hard to inspect. Doesn't affect production performance. Formatter function only called when DevTools open. Helps debugging shared hooks. Not necessary for simple hooks.

### Q24: What is useTransition and how does it work?
**Answer**: useTransition marks state updates as non-urgent transitions, introduced in React 18. Returns isPending flag and startTransition function. Lets React interrupt long renders to handle more urgent updates like user input. Improves perceived performance by keeping UI responsive. Use for non-urgent updates like filtering lists, switching tabs, or updating charts. Different from setTimeout because React-aware. Part of concurrent features. Helps prevent UI freezing.

### Q25: Explain useDeferredValue
**Answer**: useDeferredValue defers updating part of UI, similar to debouncing. Takes value and returns deferred version that may lag behind. React updates urgent changes first, then deferred value when possible. Use for expensive renders that shouldn't block input. Different from useTransition: useDeferredValue for values, useTransition for actions. Both part of concurrent React. Helps optimize perceived performance. Works well with memoization.

---

## State Management

### Q26: What is lifting state up?
**Answer**: Lifting state up means moving state to common ancestor when multiple components need it. Makes ancestor the source of truth. Child components receive state via props and callbacks to update it. Maintains unidirectional data flow. Use when siblings need to share data. Alternative to context for simple cases. Keeps data flow predictable. Can lead to prop drilling if overused.

### Q27: Context API vs Redux - when to use which?
**Answer**: Context API built into React, good for simple global state, theme, locale, or auth. No extra dependency. Redux better for complex state logic, time-travel debugging, middleware for async actions, strict patterns, and devtools. Context causes re-renders of all consumers, Redux more optimized. For medium apps, Context sufficient. For large apps with complex state interactions, consider Redux or alternatives like Zustand, Jotai. Choice depends on team size, app complexity, and debugging needs.

### Q28: What is state colocation?
**Answer**: State colocation means keeping state as close as possible to where it's used. Benefits include easier maintenance, better performance, clearer data flow, and prevents unnecessary re-renders. Don't make everything global. Start with local state, lift up only when needed. Improves code organization and makes components more self-contained. Related to principle of proximity. Opposite of putting everything in Redux. Reduces cognitive load.

### Q29: Explain derived state and why it's better
**Answer**: Derived state is computed from existing state or props rather than stored separately. Prevents synchronization bugs, reduces state complexity, and ensures data consistency. Use useMemo for expensive derivations. No setState needed, just calculate during render. Example: fullName derived from firstName and lastName. Eliminates need to keep multiple states in sync. Reduces likelihood of bugs from stale state.

### Q30: What is the difference between local and global state?
**Answer**: Local state belongs to single component or small component tree, managed with useState or useReducer. Global state shared across app, managed with Context, Redux, or other libraries. Local state for form inputs, toggles, temporary UI state. Global for user authentication, theme, language preferences. Keep state as local as possible, lift up only when necessary. Global state easier to debug but harder to reason about. Balance based on needs.

---

## Performance Optimization

### Q31: Explain React.memo and when to use it
**Answer**: React.memo is HOC that memoizes component, preventing re-renders if props haven't changed. Does shallow comparison by default, custom comparison function optional. Use for expensive pure components, components receiving same props often, or components low in tree that re-render frequently. Don't overuse as adds overhead. Useless if props always change. Works with useCallback and useMemo for complete optimization. Class equivalent is PureComponent.

### Q32: What causes unnecessary re-renders in React?
**Answer**: Parent re-render causes all children to re-render by default, even with same props. State updates trigger re-renders. Context value changes re-render all consumers. Inline object/array creation in render creates new references. Inline functions passed as props. Redux state changes. Subscriptions triggering setState. Solutions include React.memo, useMemo, useCallback, proper state structure, splitting contexts, and careful prop design.

### Q33: Explain code splitting and lazy loading
**Answer**: Code splitting breaks bundle into chunks loaded on demand. Reduces initial load time. React.lazy wraps dynamic import for component-level splitting. Suspense provides fallback while loading. Route-based splitting most common. Component-based for heavy components. Library-based for large dependencies. Benefits include faster initial load, smaller bundles, better user experience. Vite and Webpack handle splitting automatically. Balance between too many chunks and too large chunks.

### Q34: What is bundle size optimization?
**Answer**: Bundle size affects load time and performance. Techniques include tree shaking to remove unused code, minification, compression with gzip or Brotli, lazy loading routes, dynamic imports, avoiding large dependencies, using smaller alternatives, analyzing with webpack-bundle-analyzer, and removing unused CSS. Modern bundlers like Vite optimize automatically. Aim for under 200KB initial bundle. Monitor with Lighthouse or bundle analyzer tools.

### Q35: Explain debouncing and throttling
**Answer**: Debouncing delays function execution until after time elapsed since last call. Useful for search inputs, window resize, or keystroke events. Throttling limits function execution to once per time period. Useful for scroll events, mouse movement, or button clicks. Debounce for when you want to wait for action to complete, throttle when you want regular intervals. Both prevent excessive function calls. Can implement manually or use libraries like lodash.


### Q36: What is virtualization and when to use it?
**Answer**: Virtualization renders only visible items in large lists, rest rendered as scroll. Libraries like react-window or react-virtualized implement this. Dramatically improves performance for thousands of rows. Use when rendering large datasets, infinite scrolls, or data grids. Trade-off is complexity and loss of browser's native scrolling features. Not needed for small lists under 100 items. Calculates viewport and renders only what's visible plus buffer.

### Q37: Explain the importance of key prop in lists
**Answer**: Keys help React identify which items changed, added, or removed. Improves reconciliation performance. Should be stable, predictable, and unique among siblings. Don't use array index if list can reorder - causes bugs and performance issues. Use unique IDs from data. Keys not passed as props, only used by React internally. Wrong keys cause components to unmount and remount unnecessarily. Critical for dynamic lists.

### Q38: What is React.StrictMode?
**Answer**: StrictMode helps find potential problems during development. Doesn't render visible UI. Enables checks like detecting unsafe lifecycles, legacy API usage, unexpected side effects. Intentionally double-invokes some functions to detect side effects. Only runs in development mode. Doesn't affect production build. Helps prepare for future React features. Wrap entire app or specific subtrees. Useful for catching bugs early.

### Q39: How to optimize Context API performance?
**Answer**: Split contexts to prevent unnecessary re-renders. Memoize context value with useMemo. Use multiple contexts for different concerns. Implement context selectors to subscribe to specific values. Consider state management library if context performance becomes issue. Keep context close to consumers. Use composition to pass static content. Combine with React.memo on consumers. Don't put everything in one context. Balance between prop drilling and context overuse.

### Q40: What is batching in React?
**Answer**: Batching groups multiple state updates into single re-render for performance. React automatically batches updates in event handlers. React 18 extended automatic batching to promises, setTimeout, and native event handlers. Improves performance by reducing renders. Can opt out with flushSync if needed. Batching is why you can't read state immediately after setState. Makes React predictable and efficient. Reduces layout thrashing in browser.

---

## JavaScript Fundamentals

### Q41: Explain closures and their importance in React
**Answer**: Closure is function that has access to outer function's variables even after outer function returned. React hooks rely heavily on closures to maintain state between renders. Common pitfall: stale closures when using old state/props in callbacks. Solutions include dependency arrays, functional setState updates, or useRef. Understanding closures essential for hooks, event handlers, and callbacks. Every render creates new closure over current props/state.

### Q42: What is the event loop?
**Answer**: Event loop handles asynchronous JavaScript. Call stack executes functions. When async operation starts, callback goes to task queue. Event loop checks if call stack empty, then moves callback from queue to stack. Microtasks like promises have higher priority than macrotasks like setTimeout. Understanding event loop crucial for async code, performance, and avoiding blocking main thread. React's render cycle works with event loop for batching and concurrent features.

### Q43: Explain promises and async/await
**Answer**: Promises represent eventual completion or failure of async operation. Three states: pending, fulfilled, rejected. Chain with then/catch or use async/await for cleaner syntax. Async functions return promises. Await pauses execution until promise resolves. Error handling with try/catch. Better than callback hell. React commonly uses promises for data fetching. useEffect cleanup can cancel promises. Modern alternative to callbacks. Part of ES6/ES2017.

### Q44: What is the difference between let, const, and var?
**Answer**: Var is function-scoped, hoisted, and can be redeclared. Let is block-scoped, hoisted without initialization, can't be redeclared. Const is block-scoped, must be initialized, can't be reassigned but objects are mutable. Prefer const by default, let when reassignment needed, avoid var. Block scoping prevents bugs. Const doesn't make objects immutable, only binding. Modern JavaScript uses let/const. Understanding scoping crucial for closures and React hooks.

### Q45: Explain array and object destructuring
**Answer**: Destructuring extracts values from arrays or objects into variables. Array destructuring uses position, object uses property names. Can provide default values. Useful in React for hooks, props, and state. Makes code cleaner and more readable. Can destructure in function parameters. Rest operator collects remaining properties. Nested destructuring for complex objects. Common in modern JavaScript and essential React pattern.

### Q46: What are arrow functions and how do they differ?
**Answer**: Arrow functions have concise syntax, lexical this binding, no arguments object, can't be used as constructors. Lexical this is crucial in React for event handlers - no need to bind. Great for callbacks and functional programming. Implicit return for single expressions. Not hoisted like function declarations. Use regular functions when you need this context or arguments. Arrow functions cleaner for most React code.

### Q47: Explain spread and rest operators
**Answer**: Spread expands iterables into individual elements. Use for copying arrays/objects, merging, passing array elements as arguments. Rest collects arguments into array. Use in function parameters or destructuring. Same syntax, different context. Spread is shallow copy. Common in React for immutable updates, combining props, or copying state. ES6 feature essential for modern JavaScript.

### Q48: What is the this keyword in JavaScript?
**Answer**: This refers to object executing current code. Value depends on how function called. In methods, this is the object. In functions, this is global object or undefined in strict mode. Arrow functions inherit this from enclosing scope. In React class components, must bind this for event handlers. Functional components avoid this keyword entirely. Common source of bugs. Understanding this crucial for class components.

### Q49: Explain prototypal inheritance
**Answer**: JavaScript uses prototypal inheritance, not classical. Objects inherit from other objects. Every object has internal prototype reference. Prototype chain used for property lookup. Constructor functions and classes are syntactic sugar over prototypes. Understanding prototypes helps understand how JavaScript works under the hood. React class components use classes which use prototypes. Modern React prefers composition over inheritance.

### Q50: What are higher-order functions?
**Answer**: Functions that take functions as arguments or return functions. Examples include map, filter, reduce, forEach. Enable functional programming patterns. Common in React for HOCs, hooks, and utilities. Make code more reusable and composable. Key concept for understanding React patterns. Use for data transformation, validation, or decorating functions.

---

## TypeScript

### Q51: What is TypeScript and why use it with React?
**Answer**: TypeScript is typed superset of JavaScript. Adds static typing, interfaces, and better tooling. Catches errors at compile time, provides better autocomplete, makes refactoring safer, serves as documentation, and improves team collaboration. In React, type props, state, events, hooks, and context. Trade-off is learning curve and setup complexity. Modern React development increasingly uses TypeScript. Helps in large codebases.

### Q52: Explain interfaces vs types in TypeScript
**Answer**: Both define object shapes. Interfaces can be extended, reopened for declaration merging. Types can use unions, intersections, primitives. Interfaces better for public API, objects, classes. Types better for unions, tuples, complex types. Can use interchangeably for objects. Prefer interfaces for React props to allow extension. Types for union types or utility types. Style choice for most cases.

### Q53: What are generics in TypeScript?
**Answer**: Generics create reusable components that work with multiple types. Provide type safety without sacrificing flexibility. Use angle brackets for type parameters. Common in React for generic components, hooks, or utilities. Examples include typed useState, generic list components, or data fetchers. Make code more reusable while maintaining type safety. Essential for library code.

### Q54: Explain utility types in TypeScript
**Answer**: Built-in type transformations. Partial makes all properties optional. Required makes all required. Pick selects properties. Omit excludes properties. Readonly makes immutable. Record creates object type. ReturnType gets return type. Many others available. Useful for deriving types, modifying existing types, or constraining types. Reduce code duplication. Essential for advanced TypeScript usage.

### Q55: How to type React components?
**Answer**: Functional components use React.FC or explicit return type. Props interfaces define component inputs. Generic props for reusable components. Type children, events, refs. Class components use React.Component with generic props and state types. Type custom hooks return values. Use discriminated unions for conditional props. Proper typing prevents bugs and improves developer experience. Makes refactoring safer.

---

## DOM & Browser APIs

### Q56: Explain the DOM and how React interacts with it
**Answer**: DOM is tree structure representing HTML document. JavaScript can manipulate it via DOM API. React creates virtual representation, calculates changes, then updates real DOM minimally. Direct DOM manipulation expensive, React optimizes this. React refs provide escape hatch for direct access when needed. Understanding DOM crucial for performance optimization and using refs correctly. Browser renders DOM to visual page.

### Q57: What is the difference between innerHTML and textContent?
**Answer**: InnerHTML parses HTML tags, can execute scripts, slower, security risk. TextContent treats everything as text, faster, safe from XSS. Use textContent for setting text, innerHTML when you need HTML. React escapes values by default for security. Avoid dangerouslySetInnerHTML unless sanitized. Understanding difference important for security and performance.

### Q58: Explain localStorage vs sessionStorage
**Answer**: Both part of Web Storage API. LocalStorage persists after browser closes, shared across tabs, 5-10MB limit. SessionStorage clears when tab closes, separate per tab. Use localStorage for long-term data like preferences. SessionStorage for temporary data like form state. Synchronous APIs. String storage only, need JSON for objects. No expiration, must manually clear. Alternative to cookies for client-side storage.

### Q59: What is event bubbling and capturing?
**Answer**: Event propagation has three phases: capturing from root to target, target phase, bubbling from target to root. Most events bubble up DOM tree. Use stopPropagation to prevent bubbling. AddEventListener third parameter controls phase. React uses event delegation on root for performance. Understanding bubbling important for event handling and preventing unwanted triggers. Related to event delegation pattern.

### Q60: Explain requestAnimationFrame
**Answer**: Browser API for smooth animations, syncs with display refresh rate, typically 60fps. Pauses when tab not visible, saving CPU. Better than setTimeout for animations. Receives timestamp parameter. Returns ID for cancellation. React internally uses for some updates. Use for game loops, physics simulations, or smooth animations. Batches updates to next repaint.

### Q61: What is the Canvas API?
**Answer**: Canvas provides drawing surface for graphics via JavaScript. Good for games, visualizations, image manipulation. 2D and WebGL contexts available. Immediate mode graphics, not DOM-based. Good performance for many objects. Drawbacks include no built-in interactivity, accessibility challenges. React can integrate with useRef and useEffect. Alternative to SVG for different use cases.

### Q62: Explain IntersectionObserver
**Answer**: API to observe when elements enter/exit viewport or intersect with ancestor. Asynchronous, efficient. Use for lazy loading images, infinite scroll, analytics, animations on scroll. Better than scroll listeners for performance. Options for root, threshold, margin. Callback receives entries array. Polyfill for older browsers. Modern way to handle scroll-based features.

### Q63: What is ResizeObserver?
**Answer**: Observes element size changes. Fires when element resized. More reliable than window resize events. Use for responsive components, charts, or dynamic layouts. Callback receives entries with contentRect. Unobserve when done. Part of modern DOM APIs. Useful in React with useEffect for cleanup.

### Q64: Explain MutationObserver
**Answer**: Observes DOM mutations like added/removed nodes or attribute changes. Asynchronous callback. Configure what to observe: childList, attributes, characterData, subtree. Use for third-party library integration or complex DOM monitoring. Performance better than deprecated mutation events. Disconnect when done. Useful in React for integrating with non-React code.

### Q65: What is the Fetch API?
**Answer**: Modern API for HTTP requests, promise-based, cleaner than XMLHttpRequest. Doesn't reject on HTTP errors, check response.ok. Supports request/response objects, streaming, CORS. Use for API calls in React. Combine with async/await. AbortController for cancellation. Built into modern browsers. Alternative to axios for simple cases.

---

## Event Handling


### Q66: What are synthetic events in React?
**Answer**: React's cross-browser wrapper around native browser events. Same interface across browsers. Pooled for performance in older React versions. Access native event via nativeEvent. Some differences from native events. Don't need to worry about browser inconsistencies. Event delegation handled by React. Understanding synthetic events important for event handling in React.

### Q67: Explain event delegation in React
**Answer**: React attaches single event listener to root rather than each element. Events bubble to root where React handles them. Improves performance with many elements. Automatically handled, usually don't need to worry. Understanding helps with event handling bugs. Changed in React 17 to attach to root node instead of document.

### Q68: How to pass parameters to event handlers?
**Answer**: Use arrow function inline, bind in constructor, or create wrapper function with useCallback. Each has trade-offs. Arrow functions create new function each render unless memoized. Binding in constructor once. UseCallback for memoization. Can also use data attributes. Choose based on performance needs and complexity.

### Q69: What is preventDefault and stopPropagation?
**Answer**: PreventDefault stops default browser behavior like form submission or link navigation. StopPropagation prevents event from bubbling up DOM tree. Use preventDefault for forms, links, context menus. StopPropagation when you don't want parent handlers to fire. Don't confuse with return false which does both. Understanding both important for proper event handling.

### Q70: Explain passive event listeners
**Answer**: Passive listeners can't call preventDefault, allowing browser to optimize scroll performance. Set via addEventListener third parameter. Important for touch and wheel events. Improves scroll performance on mobile. React supports via specific event names. Modern browsers default some events to passive. Understanding helps with scroll performance issues.

---

## Async Programming

### Q71: What are race conditions and how to avoid them?
**Answer**: Race condition occurs when timing affects outcome. Common in async code when multiple operations depend on order. In React, cleanup functions prevent race conditions in useEffect. Cancel old requests when new ones start. Use loading states to prevent multiple simultaneous operations. AbortController for cancelling fetch requests. Proper state management prevents races. Understanding crucial for async operations.

### Q72: Explain Promise.all vs Promise.race
**Answer**: Promise.all waits for all promises to resolve, rejects if any rejects. Returns array of results. Use when need all results. Promise.race resolves/rejects with first settled promise. Use for timeout patterns or fastest response. Promise.allSettled waits for all but doesn't short-circuit on rejection. Choose based on requirements.

### Q73: What is the AbortController?
**Answer**: API to abort fetch requests and other async operations. Create controller, pass signal to fetch, call abort to cancel. Useful in React useEffect cleanup to cancel pending requests. Prevents memory leaks and race conditions. Throws AbortError when cancelled. Essential for proper cleanup in components.

### Q74: Explain debouncing API calls
**Answer**: Delay API call until user stops typing. Prevents excessive requests. Use setTimeout and clear on each keystroke. Libraries like lodash provide debounce. In React, can implement with useEffect and cleanup. Important for search inputs, autocomplete. Improves performance and reduces server load. Balance between responsiveness and efficiency.

### Q75: What are Web Workers?
**Answer**: Run JavaScript in background thread, separate from main thread. Can't access DOM. Communicate via postMessage. Use for heavy computations, data processing, or complex calculations. Prevents blocking UI. Transfer data between threads. Useful in React for expensive operations. Not needed for most apps. Modern way to use multiple CPU cores.

---

## Design Patterns

### Q76: Explain the Container/Presentational pattern
**Answer**: Separate logic from presentation. Container components handle data and logic, pass props to presentational components. Presentational components focus on UI, receive props, no business logic. Makes components more reusable and testable. Clear separation of concerns. Container can be smart component, presentational dumb. Hooks blur this distinction but pattern still useful.

### Q77: What are Higher-Order Components?
**Answer**: Function that takes component and returns enhanced component. Share logic between components. Examples include withRouter, withAuth. Can inject props, modify behavior, or wrap with additional UI. Alternative to render props and hooks. Hooks generally preferred now. Still useful for some cases. Name should start with "with". Understanding helps with older codebases.


### Q78: What is the Render Props pattern?
**Answer**: Component that uses function prop to share code. Function receives data and returns React element. More flexible than HOCs. Component controls what to render. Examples include React Router's Route. Hooks largely replaced this pattern. Still useful for specific cases. Can be verbose. Name "render prop" from common prop name but can be any function prop.

### Q79: Explain Compound Components pattern
**Answer**: Components designed to work together, sharing implicit state. Parent manages state, children access via context or cloning. Examples include Select/Option, Tabs/Tab. Flexible API, good developer experience. Used by UI libraries like Radix. Provides flexible composition. Implementation uses Context or React.cloneElement. Makes related components easy to use together.

### Q80: What is Dependency Injection in React?
**Answer**: Passing dependencies to components rather than hardcoding them. Makes components more testable and flexible. Can inject via props, context, or HOCs. Useful for services, API clients, or configuration. Improves testability by allowing mock injection. Context API natural form of DI in React. Balance between flexibility and complexity.

### Q81: Explain the Observer pattern in React
**Answer**: Subjects maintain list of observers, notify them of state changes. React state management follows observer pattern - components observe state, re-render on changes. Context and Redux implement observer pattern. Hooks like useState internally use observers. Understanding helps grasp React's reactivity model. Pub-sub is related pattern.

### Q82: What is the Factory pattern and its use?
**Answer**: Function that creates objects/components based on input. Hide creation logic. In React, create components dynamically based on type. Useful for form builders, dynamic UIs, or plugin systems. Provides abstraction layer. Makes code more maintainable. Can combine with configuration objects. Common in component libraries.

### Q83: Explain the Singleton pattern
**Answer**: Ensures class has only one instance. Global point of access. In React, avoid true singletons as they prevent isolation. Module exports act like singletons. Redux store is singleton. Context providers manage singleton state. Be cautious with singletons in React due to testing and SSR concerns. Modules provide singleton-like behavior.

### Q84: What is Composition vs Inheritance?
**Answer**: React favors composition over inheritance. Build complex components from simple ones rather than extending classes. Composition more flexible, easier to understand. Use props.children, render props, or HOCs for composition. Inheritance creates tight coupling. React components should rarely use extends beyond React.Component. Composition enables better reusability.

### Q85: Explain the Provider pattern
**Answer**: Component that provides values to descendants via Context. Wraps part of tree, children access via Consumer or useContext. Manages shared state or dependencies. Examples include Redux Provider, Theme Provider. Enables dependency injection. Avoids prop drilling. Can nest multiple providers. Core pattern in React ecosystem.

---

## Build Tools & Bundlers

### Q86: What is Vite and how does it differ from Webpack?
**Answer**: Vite is modern build tool using native ES modules during development. Instant server start, faster HMR than Webpack. Uses Rollup for production builds. Webpack bundles everything, slower for large projects. Vite pre-bundles dependencies with esbuild. Webpack more mature, broader plugin ecosystem. Vite simpler configuration. Choose based on project needs and team familiarity.

### Q87: Explain tree shaking
**Answer**: Elimination of dead code during bundling. Works with ES6 modules. Removes unused exports. Reduces bundle size significantly. Requires static imports, not dynamic. Side-effect-free code treeshakes better. Configure via package.json sideEffects field. Modern bundlers do this automatically. Understanding helps optimize bundle size.

### Q88: What is Hot Module Replacement?
**Answer**: Updates modules in running application without full reload. Preserves application state. Faster development feedback loop. Works with Webpack, Vite. React Fast Refresh builds on HMR for React components. Can lose state if not properly configured. Essential for modern development experience. Different from live reload which refreshes page.

### Q89: Explain code splitting strategies
**Answer**: Break bundle into chunks loaded on demand. Route-based splitting most common. Component-based for heavy components. Library splitting for large dependencies. Dynamic imports enable splitting. React.lazy for components. Balance between too many chunks and too few. Analyze bundle to identify split points. Improves initial load time.

### Q90: What are polyfills and when to use them?
**Answer**: Code that provides modern functionality in older browsers. Adds missing browser features. Examples include Promise, fetch, Array methods. Can increase bundle size. Use browserslist to target browsers. Tools like core-js provide polyfills. Only include needed polyfills. Modern bundlers can add automatically. Trade-off between compatibility and size.

---

## Testing

### Q91: What is unit testing in React?
**Answer**: Test individual components or functions in isolation. Mock dependencies and props. Use Jest as test runner. React Testing Library for component testing. Test behavior, not implementation. Cover edge cases and error states. Fast execution. Foundation of testing pyramid. Should be majority of tests.

### Q92: Explain integration testing
**Answer**: Test how components work together. More realistic than unit tests. Test user flows and interactions. Mock external dependencies like APIs. Slower than unit tests but catch more bugs. Use React Testing Library. Test from user perspective. Balance with unit and E2E tests.

### Q93: What is E2E testing?
**Answer**: Test entire application flow from user perspective. Use tools like Playwright, Cypress. Run in real browser. Test critical paths. Slowest tests but highest confidence. Catch integration issues. Expensive to maintain. Should be small portion of test suite. Complement unit and integration tests.

### Q94: Explain React Testing Library philosophy
**Answer**: Test components as users would use them. Query by accessibility roles, labels, text. Avoid testing implementation details. Makes tests resilient to refactoring. Encourages accessible code. Prefer user-centric queries. Different from Enzyme which tests implementation. Opinionated but leads to better tests.

### Q95: What is snapshot testing?
**Answer**: Capture component output and compare to previous snapshot. Catches unintended changes. Good for static components. Can create false positives with dynamic content. Review snapshots carefully during updates. Complement with behavior tests. Jest provides snapshot testing. Don't overuse. Best for UI consistency checks.

---

## Web Performance

### Q96: Explain Critical Rendering Path
**Answer**: Steps browser takes to render page: HTML parsing, CSS parsing, render tree construction, layout, and paint. Optimizing CRP improves perceived performance. Minimize render-blocking resources. Inline critical CSS. Defer non-critical JavaScript. Use async/defer attributes. Understanding helps optimize initial load. Affects metrics like FCP and LCP.

### Q97: What are Web Vitals?
**Answer**: User-centric performance metrics. Core Web Vitals include LCP (loading), FID (interactivity), CLS (visual stability). LCP should be under 2.5s, FID under 100ms, CLS under 0.1. Affects Google rankings. Measure with Lighthouse, PageSpeed Insights. Optimize for better user experience. React optimizations help these metrics.

### Q98: Explain lazy loading images
**Answer**: Load images only when needed, typically when entering viewport. Reduces initial page weight. Use loading="lazy" attribute or Intersection Observer. React libraries like react-lazy-load-image-component help. Improves performance on image-heavy pages. Placeholder or blur-up techniques for better UX. Balance between performance and user experience.

### Q99: What is progressive enhancement?
**Answer**: Build basic functionality first, enhance for capable browsers. Opposite of graceful degradation. Core content works without JavaScript. Add interactivity progressively. Improves accessibility and reliability. SEO benefits. React applications can use server-side rendering for core content. Balance between progressive enhancement and modern features.

### Q100: Explain caching strategies
**Answer**: Browser caching reduces repeated requests. Cache-Control headers control caching. Service Workers enable advanced caching. Versioned assets enable long-term caching. CDNs provide edge caching. LocalStorage for application data. IndexedDB for large datasets. Balance between fresh content and performance. Cache busting with hashes in filenames.

---

## Security

### Q101: What is XSS and how to prevent it?
**Answer**: Cross-Site Scripting injects malicious scripts. React escapes values by default, preventing most XSS. Avoid dangerouslySetInnerHTML unless sanitizing with DOMPurify. Validate and sanitize user inputs. Use Content Security Policy headers. Escape data from external sources. Never trust user input. Critical security concern for web applications.

### Q102: Explain CSRF and prevention
**Answer**: Cross-Site Request Forgery tricks users into unwanted actions. Prevention includes CSRF tokens, SameSite cookies, checking Origin/Referer headers, and requiring re-authentication for sensitive actions. React apps need backend implementation. Token stored in hidden form field or custom header. Affects authenticated endpoints.

### Q103: What is Content Security Policy?
**Answer**: HTTP header controlling resource loading. Prevents XSS and injection attacks. Whitelist allowed sources for scripts, styles, images. React apps need careful CSP configuration. Inline scripts require nonces or hashes. Restrict eval usage. Test thoroughly before deploying. Modern security best practice.

### Q104: Explain authentication vs authorization
**Answer**: Authentication verifies identity (who you are). Authorization determines permissions (what you can do). Authentication happens first. Use JWT, sessions, or OAuth for authentication. Role-based or permission-based authorization. React handles UI, backend enforces security. Never trust client-side checks alone. Both critical for secure applications.

### Q105: What are secure dependencies?
**Answer**: Regularly update dependencies to patch vulnerabilities. Use npm audit to check for issues. Verify package legitimacy. Check download counts and maintenance. Use lock files. Avoid packages with no tests or documentation. Consider package weight and dependencies. Security updates critical. Automated tools like Dependabot help.

---

## Advanced React

### Q106: Explain React 18 Concurrent features
**Answer**: Concurrent rendering allows React to interrupt rendering. StartTransition marks updates as non-urgent. Automatic batching in all scenarios. Suspense for data fetching. useTransition and useDeferredValue hooks. Improves responsiveness. Backward compatible. Opt-in features. Enables future optimizations. Changes how React schedules updates.

### Q107: What is Suspense and how does it work?
**Answer**: Suspense handles asynchronous operations declaratively. Show fallback while waiting for code or data. Works with React.lazy for code splitting. React 18 adds data fetching support. Throw promise to trigger Suspense. Can nest Suspense boundaries. Improves loading state management. Part of Concurrent React. Simplifies async component logic.

### Q108: Explain Server Components
**Answer**: React Server Components render on server, send to client. Zero bundle size for server components. Direct database access possible. Improved performance. Client components handle interactivity. Can mix server and client components. Different from SSR. Still experimental. Requires special bundler support. Future of React architecture.

### Q109: What is hydration in SSR?
**Answer**: Process of attaching event handlers to server-rendered HTML. Makes page interactive. React checks server HTML matches client render. Hydration mismatches cause warnings. Selective hydration in React 18. Critical for SSR performance. Different from client-side rendering. Improves perceived performance.

### Q110: Explain React Fiber architecture
**Answer**: React's reconciliation engine rewrite in React 16. Enables incremental rendering. Breaks work into chunks. Can pause and resume work. Priority scheduling for updates. Foundation for Concurrent features. Improved error handling with error boundaries. Better performance for complex UIs. Understanding helps grasp React internals.

### Q111: What are Portals and when to use them?
**Answer**: Render children into DOM node outside parent hierarchy. Use for modals, tooltips, overlays. Breaks out of parent styles and overflow. Events still bubble through React tree. Created with ReactDOM.createPortal. Common in UI libraries. Solves z-index and positioning issues. Essential for overlay components.

### Q112: Explain Error Boundaries
**Answer**: Components that catch JavaScript errors in child tree. Log errors and show fallback UI. Only work in class components. Can't catch errors in event handlers, async code, or own errors. Use componentDidCatch lifecycle. getDerivedStateFromError for render phase errors. Should be used strategically, not everywhere. Prevents entire app crashes.

### Q113: What is React DevTools and its features?
**Answer**: Browser extension for debugging React applications. Inspect component tree, props, and state. Profile performance with flamegraph. Track component updates. Find performance bottlenecks. Debug hooks. Support for Suspense and Concurrent features. Essential development tool. Helps understand React behavior and optimize applications.

### Q114: Explain Profiler API
**Answer**: Measures rendering performance. Wrap components to track render times. Callback receives timing information. Helps identify expensive renders. Use in development only. React DevTools provides visual profiler. Can measure specific subtrees. Essential for performance optimization. Programmatic alternative to DevTools profiler.

### Q115: What is Strict Mode and its checks?
**Answer**: Development mode component highlighting problems. Detects unsafe lifecycles, legacy API usage, unexpected side effects. Double-invokes some functions to find bugs. Doesn't affect production. Helps prepare for future React. Warns about findDOMNode usage. Checks for legacy context API. Wrap app or specific parts.

### Q116: Explain Forward Refs
**Answer**: Pass ref through component to child. Use React.forwardRef wrapper. Enables ref forwarding to DOM elements or class instances. Useful for reusable component libraries. Combine with useImperativeHandle for custom ref API. Common in UI libraries. Maintains encapsulation while allowing ref access.

### Q117: What is useId hook?
**Answer**: Generates unique IDs stable across server and client. Useful for accessibility attributes. Prevents hydration mismatches. Available in React 18. Better than Math.random for SSR. Use for form labels and ARIA attributes. Part of React's SSR improvements.

### Q118: Explain React.startTransition
**Answer**: Marks state updates as transitions. Keeps UI responsive during expensive renders. Different from setTimeout because React-aware. Can interrupt transition renders for urgent updates. Improves perceived performance. Part of Concurrent React. Use for non-urgent updates like filtering or searching.

### Q119: What is useSyncExternalStore?
**Answer**: Subscribe to external stores. Handles concurrent rendering correctly. Use for state management libraries, browser APIs, or any external subscription. Replaces older patterns prone to tearing. Part of React 18. Enables libraries to support concurrent features. Advanced hook for library authors.

### Q120: Explain automatic batching in React 18
**Answer**: Groups multiple state updates into single re-render. Extended to promises, setTimeout, and native event handlers in React 18. Previously only in React event handlers. Improves performance automatically. Can opt out with flushSync. Backward compatible. Makes React more consistent. Reduces unnecessary renders.

---

## Bonus Questions

### Q121: What is the difference between library and framework?
**Answer**: Library provides specific functionality, you call it. Framework provides structure, calls your code. React is library for UI, doesn't dictate routing, state management, or build tools. Angular is framework with everything included. Libraries more flexible, frameworks more opinionated. React ecosystem combines libraries. Choice affects architecture decisions.

### Q122: Explain responsive design principles
**Answer**: Design adapts to different screen sizes. Mobile-first approach recommended. Use relative units, flexible grids, media queries. CSS Grid and Flexbox enable responsive layouts. Breakpoints for different devices. Touch-friendly for mobile. Progressive enhancement. Test on actual devices. Consider performance on mobile networks.

### Q123: What is accessibility and why it matters?
**Answer**: Make applications usable by everyone including people with disabilities. Legal requirement in many jurisdictions. Semantic HTML, ARIA labels, keyboard navigation, screen reader support. Benefits all users. SEO improvements. React supports accessibility but requires attention. Use tools like axe, lighthouse. Test with screen readers.

### Q124: Explain Progressive Web Apps
**Answer**: Web apps that work offline, installable, feel native. Use service workers for caching. Manifest file for installation. Push notifications. Responsive design. HTTPS required. Improves engagement and performance. React can build PWAs. Balance between web and native features.

### Q125: What is micro-frontends architecture?
**Answer**: Split frontend into independent applications. Each team owns feature. Independent deployment. Technology agnostic. Challenges include shared state, styling, performance. Solutions include Module Federation, iframes, or web components. Suitable for large organizations. Increases complexity. React supports via Module Federation.

---

## 🎯 Final Tips for Interviews

### Before the Interview
1. Review your project thoroughly - know every feature
2. Understand why you made each technical decision
3. Be ready to discuss trade-offs and alternatives
4. Prepare examples of challenges you solved
5. Know the basics of all technologies you listed

### During the Interview
1. Think out loud - show your problem-solving process
2. Ask clarifying questions before answering
3. Admit when you don't know something
4. Relate answers to your actual project experience
5. Discuss trade-offs and alternatives
6. Be honest about limitations and what you'd improve

### Common Follow-up Questions
- Why did you choose React over Angular/Vue?
- How would you improve this application?
- What was the biggest challenge you faced?
- How did you ensure code quality?
- What would you do differently if starting over?
- How did you handle performance issues?
- What testing strategy did you use?
- How did you manage state complexity?

### Red Flags to Avoid
- Not knowing your own project
- Unable to explain technical decisions
- Claiming everything is perfect
- Copying code without understanding
- Not considering trade-offs
- Ignoring performance implications
- Dismissing alternative approaches

---

## 📚 Recommended Learning Resources

### Official Documentation
- React Documentation
- TypeScript Handbook
- MDN Web Docs
- web.dev by Google

### Books
- "Learning React" by Alex Banks & Eve Porcello
- "You Don't Know JS" by Kyle Simpson
- "JavaScript: The Good Parts" by Douglas Crockford

### Courses
- Frontend Masters
- Epic React by Kent C. Dodds
- React documentation interactive tutorials

### Practice
- LeetCode for algorithms
- Frontend Mentor for projects
- Build real applications
- Contribute to open source

---

**Good luck with your interviews! Remember: understanding concepts deeply is more important than memorizing answers. Use your project as a foundation to demonstrate real-world application of these concepts.**

---

© 2024 Interview Preparation Guide
