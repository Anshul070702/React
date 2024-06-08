# `UseState` Hook

- This hook lets us add state to a functional component
- It returns an array with 2 elements
- The first element is current value of the state, and the second value is the state setter function
- In classes, state is always an object but in useState hook, state doesnot have to be object, it can be any type.
- A state variable can be `String`, `Number`, `Boolean`, `Object`, `Array`, `function`, `null`, `undefined`

  > const [state, setState] = useState(intitalValue)
  > Here, the `initialValue` is the value you want to start with, and `state` is the current state value that can be used in your component. The `setState` function can be used to update the state, triggering a re-render of your component.

```
import {useState} from 'react'

const HookCounter = () => {
  const[count, setCount] = useState(0)
  const handleClick = () => {
    setCount(count + 1)
  }
  return (
    <div>
      <button
      onClick{handleClick}
      > Count {count}
      </button>
    </div>
  )
}
```

## `useState` with previous state

setCount(count + 1 ) => **not** a right way to change value

```
import {useState} from 'react'

const HookCounter = () => {
  const[count, setCount] = useState(0)
  const handleClick = () => {
    setCount(prevCount => prevCount + 1)
  }
  return (
    <div>
      <button
      onClick{handleClick}
      > Count {count}
      </button>
    </div>
  )
}
```

## using Object inside `useState`

```
const [state, setState] = useState({ count: 4, theme: 'blue'})
const count = state.count
const theme = state.theme
const handleClick = () => {
  setState(prevState => {
    // useState doesnot automatically merge and update the object, so while using objects, previous state must be spread before in order to merge with the updated state
    return {...prevState, count: prevstate.count + 1}
  })
}
return(
  <div>
  <button
  onClick = {handleClick}
  >
  </button>
  </div>
)
```

## using Array inside `useState`

```
import {useState} from 'react'
const HookCounter = () => {
  const[items, setItems] = useState([])
  const addItem = () => {
    setItems([
      ...items, // first items of array will be copied using spread, then new item will be appended
      {
        // appending the new items
        id: items.length,
        value: Math.floor(Math.random() * 10) + 1,
      },
    ]);
  };
  return (
    <div>
      <button onClick={addItem}> Add an item </button>
      <ul>
      {items.map(item=>(
        <li key = {item.id}>{item.value}</li>
      ))}
      </ul>
    </div>
  )
}
```

## passing state in `useState`

- useState(4) => The initial value will be assigned everytime the fuction is called or the state is changed
- useState(() => { return 4 }) => The initial value will be assigned only on the initial render.
