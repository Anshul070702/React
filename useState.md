UseState Hook
This hook provides 
```
import {useState} from 'react'

const HookCounter = () => {
  const[count, setCount] = useState(0)

  return (
    <div>
      <button
      onClick{() => setCount(count + 1)}
      > Count {count}
      </button>
    </div>
  )
}

```

- using Objects inside State

```
const [state, setState] = useState({ count: 4, theme: 'blue'})
const count = state.count
const theme = state.theme

const handleClick = () => {
  setState(prevState => {
    // since everything is overwritten when values are updated, so while using objects, previous state must be spread.
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

- passing state in useState
  - useState(4) => this will run everytime the fuction is called or the state is changed
  - useState(() => {
    return 4
    }) => this runs only one time
