//This is the express code should run on thr computer loacallay to cconnect with frontend 

const express = require('express');
const bodyParser = require('body-parser');
const path = require('path');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());
app.use(express.static('public')); // For serving static files

// Serve the HTML file
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Calculate endpoint
app.post('/calculate', (req, res) => {
    try {
        const { num1, num2 } = req.body;
        
        // Convert strings to numbers and calculate sum
        const result = parseInt(num1) + parseInt(num2);
        
        // Send result back to client
        res.json({ result });
    } catch (error) {
        res.status(400).json({ error: 'Invalid input' });
    }
});

// Start server
app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});

