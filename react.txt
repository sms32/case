import React, { useState } from 'react';

function App() {
  const [tasks, setTasks] = useState(["Meeting", "Assignment"]);
  const [inputValue, setInputValue] = useState("");

  const addTask = () => {
    if (inputValue.trim()) {
      setTasks([...tasks, inputValue]);
      setInputValue("");
    }
  };

  return (
    <div style={{ display: 'flex', flexDirection: 'column', alignItems: 'center', fontFamily: 'Arial, sans-serif' }}>
      <h2 style={{ color: '#333' }}>Task Manager</h2>
      <div style={{ marginBottom: '20px' }}>
        <input 
          type="text" 
          placeholder="Enter new task"
          value={inputValue}
          onChange={(e) => setInputValue(e.target.value)}
          style={{ padding: '8px', fontSize: '14px' }}
        />
        <button 
          onClick={addTask} 
          style={{ padding: '8px 12px', fontSize: '14px', cursor: 'pointer' }}
        >
          Add Task
        </button>
      </div>
      <ul style={{ listStyleType: 'none', padding: 0, width: '200px', textAlign: 'left' }}>
        {tasks.map((task, index) => (
          <li key={index}>{task}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;
