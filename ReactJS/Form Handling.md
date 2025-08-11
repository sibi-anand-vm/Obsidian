
## 🔧 What is Form Handling in React?

Form handling in React involves capturing user input through form elements like `<input>`, `<textarea>`, and `<select>`, and processing the data via controlled components.

---

## 🧠 Why Use State in Forms?

- Keep form inputs in sync with component state
- Perform real-time validations
- Conditionally render elements based on input
- Capture all user inputs for submission

---

## 🔄 Controlled Components

A controlled component is a form element whose value is controlled by React state.

```jsx
import { useState } from "react";

function MyForm(){
    const [inputs, setInputs] = useState({});

    const handleSubmit = (e) => {
        e.preventDefault();
        console.log("Form submitted:", inputs);
    };

    const handleChange = (e) => {
        let name = e.target.name;
        let value = e.target.value;
        setInputs((prev) => ({
            ...prev,
            [name]: value // ✅ dynamic key update
        }));
    };

    return (
        <form onSubmit={handleSubmit}>
            <label>
                Name: <input type="text" name="name" onChange={handleChange} />
            </label><br/>
            <label>
                Nickname: <input type="text" name="nickname" onChange={handleChange} />
            </label><br/>
            <label>
                Age: <input type="text" name="age" onChange={handleChange} />
            </label><br/>
            <label>
                Mail: <input type="text" name="mail" onChange={handleChange} />
            </label><br/>
            <label>
                Phone: <input type="text" name="phone" onChange={handleChange} />
            </label><br/>
            <input type="submit" value="Submit form" />
        </form>
    );
}
export default MyForm;