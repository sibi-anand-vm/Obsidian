`useMemo` is a React Hook that helps **optimize performance** by **memoizing** (remembering) the result of a **function calculation**—so it's only **recalculated when dependencies change**.

```jsx
import { useMemo, useState } from "react"

const items = ["Apple", 'Banana', "Orange", "Mango", "Grapes"]

export default function UseMemoExample() {
  const [search, setSearch] = useState("")
  const [counter, setCounter] = useState(0)

  const filterItems = useMemo(() => {
    console.log("Filtering...")
    return items.filter((item) => item.includes(search))
  }, [search])

  return (
    <div>
      <h1>UseMemo Example</h1>
      <input onChange={(e) => setSearch(e.target.value)} />
      <h3>Filtered Items:</h3>
      <ul>
        {filterItems.map(item => <li>{item}</li>)}
      </ul>
      <h3>Count: {counter}</h3>
      <button onClick={() => setCounter(state => state + 1)}>
        Increment Count
      </button>
    </div>
  )
}
```

It demonstrates how to **optimize performance using `useMemo`** by memoizing the result of filtering a list, avoiding unnecessary recalculations when unrelated state (like `counter`) changes.