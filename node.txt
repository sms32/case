const express = require('express');
const app = express();
const port = 3000;

// Middleware to parse JSON bodies
app.use(express.json());

let todoList = []; // Array to store to-do items
let idCounter = 1; // Simple ID counter for to-do items

// CREATE: Add a new to-do item
app.post('/api/todos', (req, res) => {
    const { task } = req.body;
    if (!task) {
        return res.status(400).json({ error: 'Task is required' });
    }

    const newTodo = {
        id: idCounter++,
        task,
        completed: false,
    };
    todoList.push(newTodo);
    res.status(201).json(newTodo);
});

// READ: Get all to-do items
app.get('/api/todos', (req, res) => {
    res.json(todoList);
});

// UPDATE: Update a to-do item by ID
app.put('/api/todos/:id', (req, res) => {
    const { task, completed } = req.body;
    const todo = todoList.find((t) => t.id === parseInt(req.params.id));

    if (!todo) {
        return res.status(404).json({ error: 'To-do item not found' });
    }

    if (task !== undefined) {
        todo.task = task;
    }
    if (completed !== undefined) {
        todo.completed = completed;
    }

    res.json(todo);
});

// DELETE: Delete a to-do item by ID
app.delete('/api/todos/:id', (req, res) => {
    const index = todoList.findIndex((t) => t.id === parseInt(req.params.id));

    if (index === -1) {
        return res.status(404).json({ error: 'To-do item not found' });
    }

    const deletedTodo = todoList.splice(index, 1);
    res.json(deletedTodo[0]);
});

// Start the server
app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
