```javascript
import React, { useState } from "react";
import "./TodoApp.css";
import { RiDeleteBinLine } from "react-icons/ri";

const TodoApp = () => {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState("");

  const handleAddTodo = (e) => {
    console.log("inside add function");
    e.preventDefault();

    if (!input.trim()) return;

    const newTodo = {
      id: Date.now(),
      text: input,
      completed: false,
    };

    setTodos([newTodo, ...todos]);
    setInput("");
  };

  const toggleComplete = (id) => {
    setTodos(
      todos.map((todo) =>
        todo.id === id
          ? {
              ...todo,
              completed: !todo.completed,
            }
          : todo,
      ),
    );
  };

  const handleDelete = (id) => {
    setTodos(todos.filter((todo) => todo.id !== id));
  };

  return (
    <>
      <div>TodoApp</div>
      <div className="todo-container">
        <h1>To-Do List</h1>
        <form action="#" onSubmit={handleAddTodo}>
          <input
            type="text"
            placeholder="Enter a task"
            value={input}
            onChange={(e) => {
              console.log(input);
              setInput(e.target.value);
            }}
          />
          <button type="submit" onClick={handleAddTodo}>
            Add
          </button>
        </form>
        <ul className="todo-list">
          {todos.map((todo) => (
            <li key={todo.id} className={todo.completed ? "completed" : ""}>
              <span onClick={() => toggleComplete(todo.id)}>
                {todo.text} - {todo.completed.toString()}
              </span>
              <button onClick={() => handleDelete(todo.id)}>
                <RiDeleteBinLine />
              </button>
            </li>
          ))}
        </ul>
      </div>
    </>
  );
};

export default TodoApp;
```javascript
