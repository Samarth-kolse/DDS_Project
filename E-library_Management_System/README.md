# 📚 E-Library Management System

## 📌 Overview
A command-line digital library management system to manage book inventory, borrowing, and returning.
Built as a Data Structures project using linked lists for inventory and stacks for undo operations.
Supports search, sorting, file storage, and double confirmation before deleting books.

---

## 🛠 Features
Add new books to the library

View all available books

Search books by ID, Author or Title.

Borrow and return books

Undo last borrow/return action


---

## 📂 Data Structures Used
Language: C++ 

Data Structures Used: Linked List, Stack


---
📌 How It Works

Admin adds books to the library inventory.

Users search or browse available books.

Borrowing or returning updates the linked list and pushes the action to the stack.

The undo feature pops from the stack and restores the previous state.


---
## 🚀 How to Run

```bash
#Clone the repository
git clone https://github.com/your-username/e-library-management.git
cd e-library-management/src

#Compile the C++ program
g++ elibrary.cpp -o elibrary

#Run the executable
./elibrary
