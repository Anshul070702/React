## The problem with passing Props

Passing props is a great way to explicitly pipe data thorough UI tree to the components that use it.
When we need to pass prop deeply through the tree, or if many components need the same props then it can lead to problems especially in larger applications or deeply nested component trees.
Here are some common issues associated with passing props:

* **Prop drilling** occurs when you have to pass props through several layers of components that do not need to use the props themselves but are merely intermediate layers.
 This can make the code harder to read and maintain, as well as more error-prone.

```
const Grandparent = () => {
  const [state, setState] = useState("some data");
  return <Parent state={state} />;
};
const Parent = ({ state }) => {
  return <Child state={state} />;
};
const Child = ({ state }) => {
  return <div>{state}</div>;
};
```
![alt text](https://github.com/Anshul070702/React/blob/main/propDrilling.png)

## REACT CONTEXT API
* Context in React is used for sharing data between components in a component tree. It allows you to pass data through the component tree without having to pass down props manually at every level.
* In other words, context provides a way to make certain data accessible to many components in your application, regardless of how deeply nested they are in the component tree. 
* The React Context API is a feature in React that allows you to pass context.

![alt text](https://github.com/Anshul070702/React/blob/main/contextAPI.png)

