# Expense Tracker (ReactJS)
## Date:24-05-2025

## AIM
To develop a simple Expense Tracker application using React that allows users to manage their personal finances by adding, viewing, and deleting income and expense transactions, while dynamically calculating the current balance, total income, and total expenses.

## ALGORITHM
### STEP 1: Initialize the Project
Create a new React app using:

npx create-react-app expense-tracker
or

npm create vite@latest expense-tracker --template react

Open the project in a code editor like VS Code.

### Step 2: Setup State
Define a state variable to store transactions:

Example: const [transactions, setTransactions] = useState([])

Define state variables for the form inputs:

const [text, setText] = useState("")

const [amount, setAmount] = useState("")

### Step 3: Add a New Transaction
Create a form with two inputs:

Text input for description

Number input for amount

On form submit:

Validate input

Create a new transaction object

Add the object to the transactions array using setTransactions.

### Step 4: Display Transaction List

Use map() to render each transaction in a list.

Conditionally style each item based on amount > 0 (income) or amount < 0 (expense).

Add a delete button next to each transaction.

### Step 5: Calculate and Display Summary

Use reduce() to calculate:

Total Balance: sum of all amounts

Total Income: sum of all positive amounts

Total Expenses: sum of all negative amounts

Display these values at the top of the UI.

### Step 6: Delete a Transaction

When delete is clicked:

Use filter() to remove the transaction from the array by id.

Update the state using setTransactions.

### Step 7: Style the Application

Use basic CSS to style:

Balance summary

Income/expense totals

Form inputs

Transaction list (with color coding)

## PROGRAM
```
import React, { useState } from "react";

export default function ExpenseTracker() {
  const [transactions, setTransactions] = useState([]);
  const [description, setDescription] = useState("");
  const [amount, setAmount] = useState("");

  const handleAddTransaction = (e) => {
    e.preventDefault();
    if (!description || !amount) return;
    const newTransaction = {
      id: Date.now(),
      description,
      amount: parseFloat(amount),
    };
    setTransactions([newTransaction, ...transactions]);
    setDescription("");
    setAmount("");
  };

  const handleDeleteTransaction = (id) => {
    setTransactions(transactions.filter((tx) => tx.id !== id));
  };

  const income = transactions
    .filter((tx) => tx.amount > 0)
    .reduce((acc, tx) => acc + tx.amount, 0);

  const expense = transactions
    .filter((tx) => tx.amount < 0)
    .reduce((acc, tx) => acc + tx.amount, 0);

  const balance = income + expense;

  return (
    <div className="max-w-md mx-auto p-4 bg-white shadow-lg rounded-xl mt-8">
      <h1 className="text-2xl font-bold text-center mb-4">Expense Tracker</h1>
      <div className="mb-4">
        <h2 className="text-xl font-semibold">Balance: ₹{balance.toFixed(2)}</h2>
        <div className="flex justify-between mt-2">
          <div className="text-green-600 font-medium">
            Income: ₹{income.toFixed(2)}
          </div>
          <div className="text-red-600 font-medium">
            Expense: ₹{Math.abs(expense).toFixed(2)}
          </div>
        </div>
      </div>
      <form onSubmit={handleAddTransaction} className="mb-4">
        <input
          type="text"
          placeholder="Description"
          value={description}
          onChange={(e) => setDescription(e.target.value)}
          className="w-full border p-2 rounded mb-2"
        />
        <input
          type="number"
          placeholder="Amount (positive or negative)"
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
          className="w-full border p-2 rounded mb-2"
        />
        <button type="submit" className="w-full bg-blue-500 text-white p-2 rounded">
          Add Transaction
        </button>
      </form>
      <ul>
        {transactions.map((tx) => (
          <li
            key={tx.id}
            className={`flex justify-between items-center mb-2 p-2 border-l-4 rounded ${
              tx.amount > 0 ? "border-green-500 bg-green-50" : "border-red-500 bg-red-50"
            }`}
          >
            <span>{tx.description}: ₹{tx.amount.toFixed(2)}</span>
            <button
              onClick={() => handleDeleteTransaction(tx.id)}
              className="text-sm text-red-600"
            >
              ✕
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

## OUTPUT

![image](https://github.com/user-attachments/assets/b14047d7-49bd-4e5b-ace0-5be26edff9f2)

## RESULT
A fully functional React-based Expense Tracker application was successfully developed. 
