# 🚗 Smart_Parking_Lot

---

## Overview
A **C++ project** to manage parking lot entry/exit using:
- Linked lists for active parked cars
- Dynamic memory allocation for parking slots
- Overflow handling when the lot is full
  
---

## 🛠 Features
🚘 Park a car in the lowest available slot.<br>
🟢 Remove a car and free the slot for future use.<br>
📋 Display all currently parked cars with their slot numbers.<br>
❌ Prevents parking if lot is full.<br>
✅ Uses Linked List to store car details dynamically.<br>
⚡ Uses Vector + Algorithm Library to manage available slots.

---

## 📌 Tech Used
- Language: C++
- Data Structure: Linked List
- Memory: Dynamic allocation

---
## ⚙️ How It Works

### 1.Parking a Car:

- System checks if parking is full.<br>
- Finds the lowest available slot (using vector + sort).<br>
- Creates a new Car node in the linked list and adds it at the front.<br>
- Displays confirmation with slot number.

### 2.Removing a Car:

- Searches linked list by car number.<br>
- Removes the node (car details) from the list.<br>
- Returns the freed slot back to the available slots vector.<br>
- Displays confirmation message.

### 3.Displaying Cars:

- Traverses the linked list starting from the head.<br>
- Prints all cars with their slot number → car number mapping.<br>
- If empty, shows "No cars parked".

---

## ▶️ Run Instructions
```bash
g++ main.cpp -o parking
./parking# 🚗 Smart_Parking_Lot

---

## Overview
A **C++ project** to manage parking lot entry/exit using:
- Linked lists for active parked cars
- Dynamic memory allocation for parking slots
- Overflow handling when the lot is full
  
---

## 🛠 Features
🚘 Park a car in the lowest available slot.<br>
🟢 Remove a car and free the slot for future use.<br>
📋 Display all currently parked cars with their slot numbers.<br>
❌ Prevents parking if lot is full.<br>
✅ Uses Linked List to store car details dynamically.<br>
⚡ Uses Vector + Algorithm Library to manage available slots.

---

## 📌 Tech Used
- Language: C++
- Data Structure: Linked List
- Memory: Dynamic allocation

---
## ⚙️ How It Works

### 1.Parking a Car:

- System checks if parking is full.<br>
- Finds the lowest available slot (using vector + sort).<br>
- Creates a new Car node in the linked list and adds it at the front.<br>
- Displays confirmation with slot number.

### 2.Removing a Car:

- Searches linked list by car number.<br>
- Removes the node (car details) from the list.<br>
- Returns the freed slot back to the available slots vector.<br>
- Displays confirmation message.

### 3.Displaying Cars:

- Traverses the linked list starting from the head.<br>
- Prints all cars with their slot number → car number mapping.<br>
- If empty, shows "No cars parked".

---

## ▶️ Run Instructions
```bash
g++ main.cpp -o parking
./parking
