# React User Table with CRUD and Edit Support

This React app implements a basic CRUD system using functional components and hooks. It displays a list of users in a table, allows new user addition, deletion, and inline editing.

## Features
- Fetch users from an API on initial load
- Display users in a styled table
- Add new user with a form
- Inline editing support
- Delete user functionality
- Toast notifications

## Technologies Used
- React (Hooks: `useState`, `useEffect`)
- Tailwind CSS (for styling)
- React Toastify (for notifications)

---

## Code Walkthrough

### State Definitions
```js
const [users, setUsers] = useState([...]);
```
Initial state holds hardcoded users. Later, it fetches more from API.

```js
const [editIndex, setEditIndex] = useState(null);
```
Tracks which user (by index) is currently being edited.

```js
const [editdata, setEditData] = useState({ name: '', DOB: '', email: '' });
```
Holds the data for the row being edited.

```js
const [form, setForm] = useState({ name: '', DOB: '', email: '' });
```
Holds the data for the new user form.

### Fetch Users
```js
useEffect(() => {
  const fetchUsers = async () => { ... }
  fetchUsers();
}, []);
```
Fetches users from a public API once during the initial render. Maps data to expected format.

### Add User
```js
const handleSubmit = (e) => {
  e.preventDefault();
  if (!form.name || !form.DOB || !form.email) return;
  setUsers((prev) => [...prev, form]);
  toast("User added Successfully");
  setForm({ name: '', DOB: '', email: '' });
};
```
Adds a user if all fields are filled. Updates state and resets form.

### Delete User
```js
const removeUser = (index) => {
  setUsers((prev) => prev.filter((_, i) => i !== index));
  toast.dark("User deleted Successfully");
};
```
Filters out user at `index` from the array.

### Edit User
```js
const handleEdit = (index) => {
  setEditIndex(index);
  setEditData(users[index]);
};
```
Enables edit mode for the selected row.

```js
const handleSave = (index) => {
  let updatedUsers = [...users];
  updatedUsers[index] = editdata;
  setUsers(updatedUsers);
  toast.warning("User data edited Successfully");
  setEditIndex(null);
};
```
Saves changes and exits edit mode.

```js
const handleCancel = () => {
  setEditIndex(null);
};
```
Cancels editing.

```js
const handleEditformChange = (e) => {
  const { name, value } = e.target;
  setEditData((prev) => ({ ...prev, [name]: value }));
};
```
Updates edit form fields.

### JSX Table
- Uses conditional rendering:
  - If `editIndex === index`, show inputs
  - Else, show plain data

### Add Form (Last Row)
- Uses `form` state
- Adds user to table

---

# FullCode
```jsx
import './App.css';
import { useEffect, useState } from 'react';
import { ToastContainer, toast } from 'react-toastify';

function App() {
  // State for users data
  const [users, setUsers] = useState([
    { name: 'John Smith', DOB: '1990-05-15', email: 'john.smith@example.com' },
    { name: 'Emily Johnson', DOB: '1985-11-22', email: 'emily.j@example.com' },
  ]);

  // Track index of user being edited
  const [editIndex, setEditIndex] = useState(null);

  // Store temporary user data during edit
  const [editdata, setEditData] = useState({ name: '', DOB: '', email: '' });

  // Form input state for adding new user
  const [form, setForm] = useState({ name: '', DOB: '', email: '' });

  // Fetch dummy users from external API and append to existing users
  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        const data = await response.json();

        // Map API data to desired structure
        const mappeduser = data.map((u) => ({
          name: u.name,
          DOB: u.username, // NOTE: Using 'username' as dummy DOB
          email: u.email
        }));

        setUsers((prev) => [...prev, ...mappeduser]);
      } catch (err) {
        console.log(err);
      }
    };
    fetchUsers();
  }, []);

  // Delete user
  const removeUser = (index) => {
    setUsers((prev) => prev.filter((_, i) => i !== index));
    toast.dark("User deleted Successfully");
  };

  // Handle new user form submission
  const handleSubmit = (e) => {
    e.preventDefault();
    if (!form.name || !form.DOB || !form.email) return;
    setUsers((prev) => [...prev, form]);
    toast("User added Successfully");
    setForm({ name: '', DOB: '', email: '' });
  };

  // Track changes in form for new user
  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm((prev) => ({ ...prev, [name]: value }));
  };

  // Enable edit mode for a user
  const handleEdit = (index) => {
    setEditIndex(index);
    setEditData(users[index]);
  };

  // Save updated user data
  const handleSave = (index) => {
    const updatedUsers = [...users];
    updatedUsers[index] = editdata;
    setUsers(updatedUsers);
    toast.warning("User data edited Successfully");
    setEditIndex(null);
  };

  // Cancel edit mode
  const handleCancel = () => {
    setEditIndex(null);
  };

  // Track changes during edit mode
  const handleEditformChange = (e) => {
    const { name, value } = e.target;
    setEditData((prev) => ({ ...prev, [name]: value }));
  };

  return (
    <div className="overflow-x-auto p-4">
      <ToastContainer />
      <table className="min-w-full divide-y-2 divide-gray-200 dark:divide-gray-700 border">
        <thead className="bg-gray-100 dark:bg-gray-800">
          <tr className="*:font-medium *:text-gray-900 dark:*:text-white">
            <th className="px-3 py-2 whitespace-nowrap">Name</th>
            <th className="px-3 py-2 whitespace-nowrap">DoB</th>
            <th className="px-3 py-2 whitespace-nowrap">Email</th>
            <th className="px-3 py-2 whitespace-nowrap">Action</th>
          </tr>
        </thead>

        <tbody className="divide-y divide-gray-200 dark:divide-gray-700">
          {users.map((user, index) => (
            editIndex !== index ? (
              <tr key={index}>
                <td className="px-3 py-2 whitespace-nowrap">{user.name}</td>
                <td className="px-3 py-2 whitespace-nowrap">{user.DOB}</td>
                <td className="px-3 py-2 whitespace-nowrap">{user.email}</td>
                <td>
                  <button
                    onClick={() => handleEdit(index)}
                    className="text-white bg-green-700 hover:bg-green-800 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2"
                  >Update</button>
                  <button
                    onClick={() => removeUser(index)}
                    className="text-white bg-red-700 hover:bg-red-800 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2"
                  >Delete</button>
                </td>
              </tr>
            ) : (
              <tr key={index}>
                <td className="px-3 py-2 whitespace-nowrap">
                  <input
                    type="text"
                    name="name"
                    value={editdata.name}
                    onChange={handleEditformChange}
                    className="border px-2 py-1 w-full"
                  />
                </td>
                <td className="px-3 py-2 whitespace-nowrap">
                  <input
                    type="text"
                    name="DOB"
                    value={editdata.DOB}
                    onChange={handleEditformChange}
                    className="border px-2 py-1 w-full"
                  />
                </td>
                <td className="px-3 py-2 whitespace-nowrap">
                  <input
                    type="text"
                    name="email"
                    value={editdata.email}
                    onChange={handleEditformChange}
                    className="border px-2 py-1 w-full"
                  />
                </td>
                <td>
                  <button
                    onClick={() => handleSave(index)}
                    className="text-white bg-green-700 hover:bg-green-800 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2"
                  >Save</button>
                  <button
                    onClick={handleCancel}
                    className="text-white bg-red-700 hover:bg-red-800 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2"
                  >Cancel</button>
                </td>
              </tr>
            )
          ))}

          {/* Add new user row */}
          <tr className="*:font-medium *:text-gray-900 dark:*:text-white">
            <td className="px-3 py-2 whitespace-nowrap">
              <input
                type="text"
                name="name"
                value={form.name}
                onChange={handleChange}
                className="border px-2 py-1 w-full"
                placeholder="Name"
              />
            </td>
            <td className="px-3 py-2 whitespace-nowrap">
              <input
                type="date"
                name="DOB"
                value={form.DOB}
                onChange={handleChange}
                className="border px-2 py-1 w-full"
              />
            </td>
            <td className="px-3 py-2 whitespace-nowrap">
              <input
                type="text"
                name="email"
                value={form.email}
                onChange={handleChange}
                className="border px-2 py-1 w-full"
                placeholder="Email"
              />
            </td>
            <td className="px-3 py-2 whitespace-nowrap">
              <button
                onClick={handleSubmit}
                className="px-4 py-1 text-sm font-semibold rounded-full text-green-700 bg-green-300 hover:bg-green-500 hover:text-white transition w-full"
              >Add User</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  );
}

export default App;
```