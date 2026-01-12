# 💰 Expense Tracker (Vue 3)

A simple **Expense Tracker** built with **Vue 3 (Composition API)** that allows users to add income and expenses, calculate totals automatically, and persist data using **localStorage**. Toast notifications provide instant user feedback.

---

## ✨ Features

- ➕ Add income and expense transactions  
- ➖ Delete transactions  
- 📊 Automatic calculation of:
  - Total Income
  - Total Expense
  - Balance  
- 💾 Persistent data using `localStorage`  
- 🔔 Toast notifications (success, error, info)  
- ⚡ Built with Vue 3 `<script setup>`

---

## 🛠️ Tech Stack

- **Vue 3**
- **Composition API**
- **vue-toastification**
- **Browser localStorage**

---

## 📂 Project Structure


---

## 🚀 Installation & Setup

### 1️⃣ Install dependencies

```bash
npm install vue-toastification



🧠 How It Works
🔹 State Management

Transactions are stored in a reactive items array

Form inputs are handled using a reactive form object

🔹 Persistence

Transactions are saved to localStorage

On page load, stored data is restored automatically



🧮 Computed Properties

| Property  | Description                |
| --------- | -------------------------- |
| `income`  | Sum of all positive values |
| `expense` | Sum of all negative values |
| `balance` | Income + Expense           |




🗑️ Delete Transaction

Each transaction includes a delete button:

Removes the transaction

Updates localStorage

Displays a toast notification



🔔 Toast Notifications

❌ Error when fields are empty

✅ Success when transaction is added

ℹ️ Info when transaction is deleted

🧪 Validation Rules

Both Text and Amount are required

Amount must be a number

Positive value = Income

Negative value = Expense

📌 Notes

Simple object-based transaction storage

Data persists after page refresh

Ideal for beginners and small projects