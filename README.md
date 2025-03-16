# **💰 Money Tracker App**  
A simple **expense and income tracking** application built with **HTML, CSS, Node.js (Express.js), and MongoDB**.

---

## **📌 Overview**  
This project allows users to **track their expenses and income**, view transaction history, and manage their **personal finances effectively**. 

### **✨ Features**  
✔️ **Add Income & Expenses**  
✔️ **View Transaction History**  
✔️ **Data Stored in MongoDB**  
✔️ **Simple & Responsive UI**  
✔️ **Delete or Edit Transactions**  
✔️ **Monthly Expense Summary**  

---

## **🛠 Tech Stack**  
- 🌐 **Frontend:** HTML, CSS  
- 🖥 **Backend:** Node.js, Express.js  
- 🛢 **Database:** MongoDB (Mongoose ORM)  
- 🔐 **Security:** dotenv for config management  

---

## **🚀 Installation & Setup**  

### **1️⃣ Clone the Repository**  
```bash
git clone https://github.com/your-username/money-tracker-app.git
cd money-tracker-app
```

### **2️⃣ Install Dependencies**  
```bash
npm install
```

### **3️⃣ Set Up MongoDB**  
Ensure **MongoDB is installed** or use **MongoDB Atlas**.  
Create a **`.env` file** and add your MongoDB connection string:  
```
MONGO_URI=mongodb://localhost:27017/moneyTracker
PORT=3000
```

### **4️⃣ Start the Server**  
```bash
node server.js
```
- Open **`http://localhost:3000`** in your browser.

---

## **📂 File Structure**  
```
/money-tracker-app
  ├── /public       # Frontend (HTML, CSS)
  ├── /views        # EJS Templates (if using templating)
  ├── /routes       # Express Routes
  ├── /models       # Mongoose Models
  ├── server.js     # Main Server File
  ├── .env          # Environment Variables
  ├── package.json  # Project Dependencies
```

---

## **🔗 API Endpoints**  

| Method | Endpoint       | Description             |
|--------|--------------|-------------------------|
| POST   | `/transaction` | Add Income/Expense    |
| GET    | `/transactions` | Fetch all Transactions |
| DELETE | `/transaction/:id` | Delete a Transaction |

---

## **💻 Code Snippets**  

### **Transaction Model (`models/Transaction.js`)**
```javascript
const mongoose = require("mongoose");

const transactionSchema = new mongoose.Schema({
  type: { type: String, enum: ["income", "expense"], required: true },
  amount: { type: Number, required: true },
  category: String,
  date: { type: Date, default: Date.now },
});

module.exports = mongoose.model("Transaction", transactionSchema);
```

### **Server Setup (`server.js`)**
```javascript
const express = require("express");
const mongoose = require("mongoose");
const dotenv = require("dotenv");
const Transaction = require("./models/Transaction");

dotenv.config();
const app = express();
app.use(express.json());

mongoose.connect(process.env.MONGO_URI, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log("MongoDB Connected"));

app.post("/transaction", async (req, res) => {
  try {
    const transaction = new Transaction(req.body);
    await transaction.save();
    res.status(201).send("Transaction Added");
  } catch (error) {
    res.status(400).send(error.message);
  }
});

app.listen(process.env.PORT, () => console.log(`Server running on port ${process.env.PORT}`));
```

---

## **📈 Future Enhancements 🚀**  
🔹 **User Authentication** (JWT)  
🔹 **Categorized Expense Reports**  
🔹 **Graphical Data Representation**  
🔹 **Export Transactions as CSV/PDF**  

---

## **👤 Contributors**  
**Bishal Jaysawal** - [GitHub Profile](https://github.com/Bishaljay)  
