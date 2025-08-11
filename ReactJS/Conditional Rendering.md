### 🔁 Conditional Rendering with Props

You can show/hide components based on certain prop values.

#### Example (Functional):


```jsx
import ShipDetail from './ShipDetail'; 
function Titanic() 
{  
const detail = {     color: "Black",     size: "200m",     speed: 40   };    return ( 
<>     
<h1>I am bigger than all ships</h1>    

{ detail.size !== undefined  ? <ShipDetail detail={detail} />  : null  }     </>   
);
}
export default Titanic;`
```

#### ✅ Shortcut:

Instead of ternary, use `&&`:

```{ detail.size && <ShipDetail detail={detail} /> }```