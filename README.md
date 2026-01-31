# 📦 Industrial Bakery Simulation

**Final Project – Algorithms and Data Structures (2023–2024, Politecnico di Milano)**  
**Grade: 30/30 – Maximum score achieved**

---

## 📖 Overview

This project implements a **discrete-time simulation** of an industrial bakery order management system.  

The goal is to efficiently manage:

- Recipes
- Ingredient inventory
- Customer orders
- Periodic deliveries  

The simulation advances **one time unit after each processed command** and terminates at the end of the input stream.

---

## 🧁 System Model

The bakery system manages:

- **Ingredients** – identified by name and stored in a warehouse  
- **Recipes** – each composed of multiple ingredients with required quantities  
- **Ingredient batches** – each defined by quantity and expiration time  
- **Customer orders** – may be immediately processed or queued if ingredients are insufficient  
- **Delivery truck** – arrives periodically with limited capacity  

**Important rule:** ingredient consumption always prioritizes batches with the earliest expiration date.

---

## ⏱️ Order Handling

1. Orders are **accepted** if the recipe exists; otherwise, they are **rejected**.  
2. If ingredients are insufficient, orders are placed in a **pending queue**.  
3. Pending orders are re-evaluated **after each restock**, in **FIFO order**.  
4. Prepared orders are stored until picked up by the courier.  
5. At delivery time:
   - Orders are selected in **chronological order**, respecting truck capacity.  
   - Selected orders are loaded by **descending weight**, with ties broken by arrival time.

---

## 🧠 Data Structures Used

The implementation emphasizes **efficient data access and updates**:

- **Hash Tables**
  - Recipes lookup (`hash_table`)
  - Ingredient warehouse (`hashmag`)  
- **Min-Heaps**
  - Used per ingredient to manage batches ordered by expiration date  
- **Linked Lists**
  - Recipe ingredient lists
  - Pending orders queue
  - Ready orders list  
- **Dynamic Arrays**
  - Heap resizing for ingredient batches  

Custom hash functions (**FNV-based**) are used to ensure uniform distribution.

---

## ⚙️ Commands Supported

- `aggiungi_ricetta` – Add a new recipe  
- `rimuovi_ricetta` – Remove a recipe if no pending or ready orders exist  
- `rifornimento` – Restock the warehouse with ingredient batches  
- `ordine` – Place a customer order  

> The program prints status messages and delivery outputs exactly as specified.

---

## 🛠️ Implementation Details

- **Language:** C  
- **Memory:** manually managed (`malloc`, `realloc`, `free`)  
- Designed for **efficiency**, **correctness**, and **strict adherence** to the specification  
- Handles **large input sizes** and **arbitrary numbers** of orders, recipes, and ingredients

---

## ✅ Output

At each courier arrival, the program prints:

- **Loaded orders**: `(time, recipe name, quantity)` in loading order  
- **Or**: `camioncino vuoto` if no orders are shipped

---

## 🎯 Purpose

This project demonstrates practical application of:

- **Hashing**  
- **Priority queues (heaps)**  
- **Linked data structures**  
- **Simulation logic**  
- **Careful time and state management**

> All requirements of the official specification are fully implemented.
