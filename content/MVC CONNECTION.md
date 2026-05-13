mongoose-crud-app/
│
├── server.js
├── package.json
├── .env
│
├── config/
│   └── db.js
│
├── models/
│   └── User.js
│
├── routes/
│   └── userRoutes.js
│
└── controllers/
    └── userController.js


PACKAGE.JSON
{
  "name": "mongoose-crud-app",
  "version": "1.0.0",
  "description": "CRUD with MongoDB & Mongoose",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "dotenv": "^16.0.0",
    "express": "^4.18.2",
    "mongoose": "^7.0.0"
  }
}

# 2. .env

MONGO_URI=mongodb://127.0.0.1:27017/mydatabase  
PORT=3000

# 3. config/db.js

const mongoose = require('mongoose');  
  
const connectDB = async () => {  
    try {  
        await mongoose.connect(process.env.MONGO_URI);  
        console.log("MongoDB Connected");  
    } catch (error) {  
        console.error(error.message);  
        process.exit(1);  
    }  
};  
  
module.exports = connectDB;

---

#  4. models/User.js

const mongoose = require('mongoose');  
  
const userSchema = new mongoose.Schema({  
    name: {  
        type: String,  
        required: true  
    },  
    email: {  
        type: String,  
        required: true,  
        unique: true  
    },  
    age: {  
        type: Number  
    }  
}, { timestamps: true });  
  
module.exports = mongoose.model('User', userSchema);

---

#  5. controllers/userController.js

const User = require('../models/User');  
  
// CREATE  
exports.createUser = async (req, res) => {  
    try {  
        const user = new User(req.body);  
        const savedUser = await user.save();  
        res.json(savedUser);  
    } catch (error) {  
        res.status(500).json({ error: error.message });  
    }  
};  
  
// READ ALL  
exports.getUsers = async (req, res) => {  
    try {  
        const users = await User.find();  
        res.json(users);  
    } catch (error) {  
        res.status(500).json({ error: error.message });  
    }  
};  
  
// READ ONE  
exports.getUserById = async (req, res) => {  
    try {  
        const user = await User.findById(req.params.id);  
        res.json(user);  
    } catch (error) {  
        res.status(500).json({ error: error.message });  
    }  
};  
  
// UPDATE  
exports.updateUser = async (req, res) => {  
    try {  
        const updatedUser = await User.findByIdAndUpdate(  
            req.params.id,  
            req.body,  
            { new: true }  
        );  
        res.json(updatedUser);  
    } catch (error) {  
        res.status(500).json({ error: error.message });  
    }  
};  
  
// DELETE  
exports.deleteUser = async (req, res) => {  
    try {  
        await User.findByIdAndDelete(req.params.id);  
        res.json({ message: "User deleted successfully" });  
    } catch (error) {  
        res.status(500).json({ error: error.message });  
    }  
};

---

#  6. routes/userRoutes.js

const express = require('express');  
const router = express.Router();  
const userController = require('../controllers/userController');  
  
router.post('/', userController.createUser);  
router.get('/', userController.getUsers);  
router.get('/:id', userController.getUserById);  
router.put('/:id', userController.updateUser);  
router.delete('/:id', userController.deleteUser);  
  
module.exports = router;

---

#  7. server.js

require('dotenv').config();  
const express = require('express');  
const connectDB = require('./config/db');  
  
const app = express();  
  
// Middleware  
app.use(express.json());  
  
// DB Connection  
connectDB();  
  
// Routes  
app.use('/api/users', require('./routes/userRoutes'));  
  
// Server  
const PORT = process.env.PORT || 3000;  
  
app.listen(PORT, () => {  
    console.log(`Server running on port ${PORT}`);  
});

---

# 8. Run the Project

### Install dependencies

npm install

### Start MongoDB

mongod

### Run server

npm start

# API Endpoints

|Method|URL|
|---|---|
|POST|`/api/users`|
|GET|`/api/users`|
|GET|`/api/users/:id`|
|PUT|`/api/users/:id`|
|DELETE|`/api/users/:id`|