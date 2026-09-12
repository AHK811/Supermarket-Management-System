<div align="center">

<img src="download.png" alt="FAST–NUCES" width="180">

# 🛒 Supermarket Management System

### A Modular Console-Based Retail Management System in C++

**Programming Fundamentals — FAST–NUCES Karachi**

<br>

[![C++](https://img.shields.io/badge/C%2B%2B-17%2B-00599C?style=for-the-badge\&logo=cplusplus\&logoColor=white)](https://isocpp.org/)
[![GCC](https://img.shields.io/badge/GCC-9%2B-5C2D91?style=for-the-badge\&logo=gnu\&logoColor=white)](https://gcc.gnu.org/)
[![Git](https://img.shields.io/badge/Git-Version%20Control-F05032?style=for-the-badge\&logo=git\&logoColor=white)](https://git-scm.com/)
[![FAST–NUCES](https://img.shields.io/badge/FAST–NUCES-Karachi-111111?style=for-the-badge)](https://www.nu.edu.pk/)
[![Status](https://img.shields.io/badge/Status-In%20Development-F4A261?style=for-the-badge)]()

<br>

**Inventory • Billing • Loyalty • Suppliers • Reporting • Access Control**

<br>

[📋 Proposal](docs/proposal.md)  ·  [📁 Source Code](src/)  ·  [📖 Documentation](docs/)

</div>

 

## 📌 About the Project

The **Supermarket Management System (SMS)** is a modular, console-based retail management application developed in **C++17** as a Programming Fundamentals course project at **FAST–NUCES, Karachi**.

The system is designed around a central principle:

> **Every major supermarket operation should work with the same consistent set of records.**

Instead of treating billing, inventory, customers, suppliers, and reporting as isolated systems, SMS connects them through shared product, customer, transaction, supplier, and user records.

This allows an action in one subsystem to immediately affect the others.

For example:

```text
Customer Checkout
       │
       ├──► Transaction Record
       │
       ├──► Inventory Updated
       │
       ├──► Loyalty Points Updated
       │
       ├──► Sales Report Updated
       │
       └──► Low-Stock Check
                    │
                    └──► Purchase Order Draft
```

The result is a small but complete retail-management ecosystem implemented using fundamental C++ programming concepts.

 

## 🎯 Problem Statement

Small-scale supermarket operations often rely on disconnected processes for:

* Inventory management
* Customer billing
* Stock monitoring
* Supplier restocking
* Loyalty programs
* Sales reporting
* Returns and refunds
* Employee access control

This separation creates several practical problems:

| Problem                                | Consequence                    |
|----------------------------------------|--------------------------------|
| Manual inventory tracking              | Incorrect stock counts         |
| Delayed stockout detection             | Products become unavailable    |
| Separate billing and inventory records | Data inconsistency             |
| No role-based access                   | Unauthorized operations        |
| Manual customer tracking               | Loyalty information is lost    |
| Reactive supplier ordering             | Restocking happens too late    |
| Manual reporting                       | Slow decision-making           |
| Poor transaction history               | Difficult refunds and auditing |

**SMS addresses these problems by connecting the entire workflow through a common data model.**

📄 **Full problem statement, objectives, scope, and design rationale:**
**[Read the Project Proposal →](docs/Proposal.md)**

 

# ✨ Key Features

<table>
<tr>
<td width="50%">

### 🔐 Role-Based Access

Three operational roles with different permissions:

* 👑 Admin
* 📦 Manager
* 💳 Cashier

Sensitive operations are restricted according to the authenticated user's role.

</td>

<td width="50%">

### 📦 Inventory Management

Complete product lifecycle management:

* Add products
* Update products
* Remove products
* Search products
* Categories
* Supplier association
* Batch tracking
* Expiry monitoring

</td>
</tr>

<tr>
<td>

### 🧾 Checkout & Billing

Cart-based checkout with:

* Product lookup
* Quantity validation
* Discounts
* Tax calculation
* Itemized receipts
* Transaction records
* Automatic inventory deduction

</td>

<td>

### ⭐ Customer Loyalty

Customer accounts maintain:

* Purchase history
* Cumulative spending
* Loyalty points
* Loyalty tiers
* Automatic point issuance
* Return-based point reversal

</td>
</tr>

<tr>
<td>

### 🏷️ Discounts & Promotions

Flexible promotional system supporting:

* Percentage discounts
* Fixed-value discounts
* Promotional codes
* Transaction-level calculations

</td>

<td>

### 🔄 Returns & Refunds

Transaction-linked returns provide:

* Original transaction verification
* Inventory restoration
* Refund calculation
* Loyalty reversal
* Role-based refund approval

</td>
</tr>

<tr>
<td>

### 🚨 Low-Stock Monitoring

The system continuously checks configurable stock thresholds.

When inventory falls below the reorder level:

```text
Low Stock
   ↓
Alert
   ↓
Reorder Threshold
   ↓
Purchase Order Draft
```

</td>

<td>

### 📊 Sales Reporting

Generate reports for:

* Daily sales
* Weekly sales
* Monthly sales
* Top-selling products
* Slow-moving products
* Revenue analysis

</td>
</tr>

<tr>
<td>

### 🚚 Supplier Management

Supplier records are connected to inventory and purchasing.

The system can create purchase-order drafts when products reach their reorder threshold.

</td>

<td>

### 📝 Audit Logging

Privileged operations are recorded with:

* User identity
* Action
* Timestamp
* Relevant operation details

Logs are maintained as append-only records.

</td>
</tr>
</table>

 

# 🧠 System Architecture

SMS follows a modular architecture where each subsystem has a focused responsibility.

```text
                         ┌──────────────────────┐
                         │       main.cpp       │
                         │   Application Layer  │
                         └──────────┬───────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    │               │               │
                    ▼               ▼               ▼
              ┌──────────┐   ┌───────────┐   ┌──────────┐
              │   Auth   │   │ Inventory │   │ Billing  │
              └──────────��   └───────────┘   └──────────┘
                    │               │               │
                    │               ▼               ▼
                    │         ┌───────────┐   ┌───────────┐
                    │         │ Suppliers │   │  Loyalty  │
                    │         └───────────┘   └───────────┘
                    │               │               │
                    └───────────────┼───────────────┘
                                    ▼
                           ┌─────────────────┐
                           │    Reporting    │
                           └────────┬────────┘
                                    │
                                    ▼
                           ┌─────────────────┐
                           │ File Persistence│
                           │    fstream      │
                           └─────────────────┘
```

### Core Data Flow

```text
                    ┌──────────────┐
                    │   Product    │
                    └──────┬───────┘
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
        ┌─────────┐   ┌──────────┐   ┌──────────┐
        │Inventory│   │ Checkout │   │ Supplier │
        └────┬────┘   └─────┬────┘   └────┬─────┘
             │              │             │
             │              ▼             │
             │        ┌────────────┐       │
             └───────►│Transaction │◄──────┘
                      └─────┬──────┘
                            │
                 ┌──────────┼──────────┐
                 ▼          ▼          ▼
             ┌────────┐ ┌────────┐ ┌─────────┐
             │Loyalty │ │Reports │ │ Audit   │
             └────────┘ └────────┘ └─────────┘
```

 

# 🗂️ Project Structure

```text
supermarket-management-system/
│
├── assets/
│   └── fast-nuces-logo.png
│
├── src/
│   ├── main.cpp
│   │
│   ├── models/
│   │   ├── Product.cpp
│   │   ├── Product.h
│   │   ├── Customer.cpp
│   │   ├── Customer.h
│   │   ├── Transaction.cpp
│   │   ├── Transaction.h
│   │   ├── Supplier.cpp
│   │   ├── Supplier.h
│   │   ├── User.cpp
│   │   └── User.h
│   │
│   ├── inventory/
│   │   ├── InventoryManager.cpp
│   │   ├── InventoryManager.h
│   │   ├── ExpiryMonitor.cpp
│   │   └── ExpiryMonitor.h
│   │
│   ├── billing/
│   │   ├── Checkout.cpp
│   │   ├── Checkout.h
│   │   ├── ReturnsManager.cpp
│   │   └── ReturnsManager.h
│   │
│   ├── loyalty/
│   │   ├── LoyaltyLedger.cpp
│   │   └── LoyaltyLedger.h
│   │
│   ├── suppliers/
│   │   ├── PurchaseOrderManager.cpp
│   │   └── PurchaseOrderManager.h
│   │
│   ├── reports/
│   │   ├── ReportGenerator.cpp
│   │   └── ReportGenerator.h
│   │
│   ├── auth/
│   │   ├── AuthManager.cpp
│   │   └── AuthManager.h
│   │
│   └── storage/
│       ├── FileHandler.cpp
│       └── FileHandler.h
│
├── data/
│   ├── products.txt
│   ├── customers.txt
│   ├── transactions.txt
│   ├── suppliers.txt
│   ├── users.txt
│   └── audit.log
│
├── docs/
│   └── proposal.md
│
├── tests/
│   └── sample-data/
│
├── Makefile
├── .gitignore
└── README.md
```

 

# 👥 User Roles

SMS implements permission-based access through three primary roles.

| Role           | Access                                                                     |
|----------------|----------------------------------------------------------------------------|
| 👑 **Admin**   | Full system access, users, pricing, suppliers, reports, audit logs         |
| 📦 **Manager** | Inventory, suppliers, purchase orders, discounts, reports, refund approval |
| 💳 **Cashier** | Checkout, permitted returns, stock lookup                                  |

### Permission Flow

```text
                 ┌─────────────┐
                 │    Login    │
                 └──────┬──────┘
                        │
                        ▼
                ┌───────────────┐
                │ Authentication│
                └───────┬───────┘
                        │
              ┌─────────┼─────────┐
              ▼         ▼         ▼
           ADMIN     MANAGER    CASHIER
              │         │         │
              ▼         ▼         ▼
           Full      Managed    Limited
           Access     Access     Access
```

 

# 🧾 Checkout Workflow

A typical supermarket transaction follows this flow:

```text
┌───────────────┐
│ Select Product│
└───────┬───────┘
        ▼
┌───────────────┐
│ Check Stock   │
└───────┬───────┘
        ▼
┌───────────────┐
│ Add to Cart   │
└───────┬───────┘
        ▼
┌───────────────┐
│ Apply Discount│
└───────┬───────┘
        ▼
┌───────────────┐
│ Calculate Tax │
└───────┬───────┘
        ▼
┌───────────────┐
│ Generate Bill │
└───────┬───────┘
        ▼
┌────────────────┐
│ Save Transaction│
└───────┬────────┘
        ▼
┌────────────────┐
│ Update Inventory│
└───────┬────────┘
        ▼
┌────────────────┐
│ Update Loyalty │
└───────┬────────┘
        ▼
┌─────────────────┐
│ Check Low Stock │
└─────────────────┘
```

 

# 💾 Data Persistence

The application uses C++ file I/O through `fstream` for persistent storage.

Data remains available after the program is closed.

```text
Application
     │
     ▼
┌──────────────┐
│ FileHandler  │
└──────┬───────┘
       │
       ├──► products.txt
       ├──► customers.txt
       ├──► transactions.txt
       ├──► suppliers.txt
       ├──► users.txt
       └──► audit.log
```

This demonstrates fundamental file-handling concepts while keeping the project lightweight and dependency-free.

 

# 🛠️ Technology Stack

| Technology              | Purpose                        |
|-------------------------|--------------------------------|
| **C++17+**              | Core programming language      |
| **STL**                 | Data structures and algorithms |
| `vector`                | Dynamic collections            |
| `map` / `unordered_map` | Fast record lookup             |
| `queue`                 | Queue-based workflows          |
| `fstream`               | Persistent file storage        |
| **GCC / g++**           | Compilation                    |
| **Make**                | Build automation               |
| **Git**                 | Version control                |
| **GitHub**              | Repository and collaboration   |


# 📊 Functional Modules

```text
                       SUPERMARKET MANAGEMENT SYSTEM
                                    │
       ┌────────────────────────────┼────────────────────────────┐
       │                            │                            │
       ▼                            ▼                            ▼
   AUTHENTICATION              INVENTORY                    BILLING
       │                            │                            │
       │                       ┌────┴────┐                 ┌─────┴─────┐
       │                       │         │                 │           │
       ▼                       ▼         ▼                 ▼           ▼
    Admin                  Products   Expiry            Checkout    Returns
    Manager                    │       Monitor               │           │
    Cashier                    │                            │           │
                               ▼                            ▼           ▼
                          Low Stock                   Transactions   Refunds
                               │                            │
                               ▼                            ▼
                         PURCHASE ORDERS              LOYALTY
                               │                            │
                               └──────────────┬─────────────┘
                                              ▼
                                           REPORTS
                                              │
                                              ▼
                                      PERSISTENT STORAGE
```

 

# 📈 Reporting

The reporting subsystem provides information derived from transaction records rather than requiring separate manual data entry.

### Supported Reports

* Daily sales
* Weekly sales
* Monthly sales
* Top-selling products
* Slow-moving products
* Revenue summaries

This keeps reporting connected to the same transaction data used by checkout.

 

# 🔄 Returns & Inventory Integrity

Returns are linked to the original transaction rather than being treated as independent operations.

```text
Original Transaction
        │
        ▼
Return Request
        │
        ▼
Transaction Verification
        │
        ├───────────────┐
        ▼               ▼
Inventory Restore   Loyalty Reversal
        │               │
        └───────┬───────┘
                ▼
          Refund Record
```

This prevents the inventory, financial, and loyalty systems from drifting apart.

 

# 🧪 Testing

Testing is organized under:

```text
tests/
└── sample-data/
```

Test scenarios include:

* Valid and invalid login
* Role restrictions
* Product creation
* Product updates
* Product deletion
* Stock validation
* Checkout
* Discount application
* Tax calculation
* Loyalty point issuance
* Returns
* Refunds
* Low-stock alerts
* Purchase-order generation
* Report generation
* File persistence


Feature branches should be merged into `main` through review.

### Recommended Commit Style

```text
feat: add product search
feat: implement checkout cart
fix: correct loyalty point calculation
fix: prevent negative inventory
docs: update project proposal
refactor: separate file persistence
test: add return transaction cases
```

 

# 📚 Course Context

| Field            | Details                         |
|------------------|----------------------------------|
| **University**   | FAST–NUCES                      |
| **Campus**       | Karachi                         |
| **Course**       | Programming Fundamentals        |
| **Language**     | C++                             |
| **Standard**     | C++17+                          |
| **Project Type** | Console-Based Management System |
| **Submission**   | September 20, 2026              |

The project is designed to demonstrate practical application of Programming Fundamentals concepts including:

* Variables and data types
* Conditional statements
* Loops
* Functions
* Arrays / STL containers
* Structures and classes
* Object-oriented programming
* Inheritance
* File handling
* Searching and sorting
* Modular programming
* Basic software architecture

 

# 📋 Project Proposal

The repository contains the project's formal proposal and design documentation.

📄 **[Read the Complete Project Proposal →](docs/Proposal.md)**

The proposal covers:

* Problem statement
* Motivation
* Objectives
* Proposed solution
* Functional requirements
* Non-functional requirements
* System modules
* User roles
* Data design
* Expected outcomes
* Project scope

> **The proposal and implementation are intended to remain synchronized as development progresses.**

 

# 👨‍💻 Team

| Name                  | Roll Number | Responsibility              |
|-----------------------|-------------|-----------------------------| 
|ABDUL HANNAN KASHIF    |  26K-3018   | Project Lead / Architecture |
|AZAAN MEHDI            |  26K-3000   | Sub leading  / Programming  |
|MUHAMMAD BILAL IMTIAZ  |  26K-3020   | Sub Leading  / Programming  |



# 📸 Demo

> Screenshots and demonstration material will be added as the implementation progresses.

Recommended demo coverage:

```text
Login
  ↓
Dashboard
  ↓
Inventory
  ↓
Checkout
  ↓
Receipt
  ↓
Inventory Update
  ↓
Loyalty Update
  ↓
Sales Report
```

 

# 🎓 Academic Purpose

This project is developed for academic purposes as part of the **Programming Fundamentals course at FAST–NUCES Karachi**.

It is intended to demonstrate how fundamental programming concepts can be combined to create a complete, interconnected software system rather than isolated programming exercises.

 

<div align="center">

## 🛒 Supermarket Management System

**Built with C++ • Designed at FAST–NUCES Karachi**

<br>

**Programming Fundamentals — 2026**

<br>

⭐ If this repository helped you understand the project, consider starring it.

</div>
