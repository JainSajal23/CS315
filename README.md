# 🛒 Departmental Store Database Application

**Course**: CS315  
**Institute**: Indian Institute of Technology Kanpur  
**Team Members**:
- Sajal Jain (210903) – [jsajal21@iitk.ac.in](mailto:jsajal21@iitk.ac.in)
- Siddhant Singhai (211028) – [ssinghai21@iitk.ac.in](mailto:ssinghai21@iitk.ac.in)
- Akshat Mehta (210092) – [akshatm21@iitk.ac.in](mailto:akshatm21@iitk.ac.in)
- Abhishek Choudhary (210037) – [cabhishek21@iitk.ac.in](mailto:cabhishek21@iitk.ac.in)
- Aryan Thada (210205) – [aryant21@iitk.ac.in](mailto:aryant21@iitk.ac.in)

---

## 📌 Abstract

This project implements a **multi-threaded Python-based database system** simulating realistic workloads of a departmental store. Built using the **`python-oracledb`** module and an Oracle backend, the application supports a full range of CRUD operations and offers robust error handling, deadlock detection, logging, and concurrency simulation.

---

## ⚙️ Architecture Overview

The system follows a **layered architecture** for maintainability and scalability:

### 🗂 Modules

- `db.py`: Database connection (standalone + pooled), session monitoring.
- `action.py`: Business logic including CRUD operations on CUSTOMERS, ORDERS, and ITEMS.
- `main.py`: Thread manager, workload dispatcher, metrics aggregator.
- `logger_tracer.py`: Logging and tracing setup for summary + detailed logs.
- `db.config`: Configuration file controlling connections, workload distribution, and logging settings.

---

## 🔄 Methodology

### ✅ Key Features

- **Thread-based concurrency** with weighted test cases.
- **Logging infrastructure** with separate monitor and trace files.
- **Transaction control** with `begin()`, `commit()`, `rollback()` for ACID compliance.
- **Real-time deadlock detection** and recovery using specific ORA error handling.
- **Workload simulation** over duration or fixed iterations.

### 🧩 Sample Workflows

- **Add New Customer**: Generates unique customer ID, inserts with validation.
- **Place Order**: Inserts order header and random items with pricing logic.
- **Delete Customer**: Cascaded delete with optimized query to avoid deadlock (via `EXISTS`).
- **Summarize Orders**: Computes bill amount using `SUM(PRICE * QTY)` and joins.

---

## 🧪 Testing and Results

- Successfully simulated concurrent transactions with up to 10 threads and 100 iterations.
- Deadlocks were mitigated using optimized subqueries (`EXISTS`).
- Logs and tabulated session outputs validated transaction integrity and thread-safe execution.

---

## 📊 Database Schema (ER Overview)

