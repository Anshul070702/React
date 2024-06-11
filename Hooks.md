Hooks are feature which allows us to use React features without having to write a class.

## Why Hooks?

React mainly used class components, which can be exhausting at times as you always had to switch between classes, higher-order components, and render props. With React hooks, you can now do all these without switching, using functional components.

**&rarr;** Avoid the whole confusion of _this_ keyword.

**&rarr;** Allow to resuse stateful logic.

**&rarr;** Organize the logic inside a component into reusable isolated units

## Rules of Hooks

- Only call Hooks at the top level

> _don't call hooks inside loops, conditions, or nested functions_

- Only call Hooks from React functions

> _call them from within React functional components and not just any regular JavaScript function_

## State Hooks

_State_ lets a component “remember” information like user input.

> For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.

To add state to a component, use one of these Hooks:

- **`useState`** declares a state variable that you can update directly.

- **`useReducer`** declares a state variable with the update logic inside a reducer function.

```
function ImageGallery() {
const [index, setIndex] = useState(0);
// ...
}
```

## Effect Hooks

_Effects_ let a component connect to and synchronize with external systems. This includes dealing with network, browser DOM, animations, widgets written using a different UI library, and other non-React code.

- **`useEffect`** connects a component to an external system.

```
function ChatRoom({ roomId }) {
useEffect(() => {
const connection = createConnection(roomId);
connection.connect();
return () => connection.disconnect();
}, [roomId]);
// ...
}
```

**If you’re not interacting with an external system, you might not need an Effect.**

## Context Hooks

_Context_ lets a component receive information from distant parents without passing it as props.

> For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

- **`useContext`** reads and subscribes to a context.

```
function Button() {
const theme = useContext(ThemeContext);
// ...
}

```

## Ref Hooks

_Refs_ let a component hold some information that isn’t used for rendering, like a DOM node or a timeout ID.

They are useful when you need to work with non-React systems, such as the built-in browser APIs.

**Unlike with state, updating a ref does not re-render your component.**

- **`useRef`** declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.

```
function Form() {
  const inputRef = useRef(null);
  // ...
}
```

## Performance Hooks

A common way to optimize re-rendering performance is to skip unnecessary work.

> or example, you can tell React to reuse a cached calculation or to skip a re-render if the data has not changed since the previous render.

To skip calculations and unnecessary re-rendering, use one of these Hooks:

- **`useMemo`** lets you cache the result of an expensive calculation.
- **`useCallback`** lets you cache a function definition before passing it down to an optimized component.

```
function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```
