# Supermarket Management System (SMS)

A console-based Supermarket Management System built in C++ as a Programming Fundamentals course project at FAST–NUCES, Karachi. The system integrates inventory management, checkout and billing, customer loyalty tracking, supplier restocking, and sales reporting around a single, consistent set of data records.

## Overview

Most small-scale supermarket software treats billing, inventory, and reporting as separate, loosely connected processes — leading to delayed stockout detection, undifferentiated staff access, manual reporting, and reactive supplier restocking. This project addresses those gaps directly by building every module (checkout, inventory, loyalty, suppliers, reports) against the same underlying product, customer, transaction, and supplier records.

See [`docs/proposal.md`](docs/proposal.md) (or the submitted proposal document) for the full problem statement and design rationale.

## Features

- **Role-based access** — Admin, Manager, and Cashier roles with permission-gated operations
- **Inventory management** — add/update/remove/search products, category and supplier association, batch-level expiry tracking
- **Real-time low-stock alerts** — configurable thresholds checked at startup and at checkout
- **Checkout & billing** — cart-based checkout with itemized receipts (price, quantity, discount, tax)
- **Customer & loyalty management** — cumulative spend tracking with automatic point/tier issuance
- **Discounts & promotions** — percentage/fixed discounts and promotional codes
- **Returns & refunds** — transaction-linked returns with inventory and loyalty reversal
- **Reporting** — on-request daily/weekly/monthly sales reports, top-selling and slow-moving items
- **Supplier & purchase orders** — automatic purchase-order drafts on reorder threshold breach
- **Audit logging** — append-only log of privileged actions with timestamp and user attribution
- **File-based persistence** — all records survive across sessions

## Tech Stack

| Component | Choice |
|---|---|
| Language | C++ (C++17 or later) |
| Data structures | STL — `vector`, `map`/`unordered_map`, `queue` |
| Persistence | File I/O via `fstream` (structured text/binary records) |
| Build | GCC/g++, Makefile |
| Version control | Git / GitHub |
| OS support | Cross-platform (Windows, Linux, macOS) |

## Project Structure

```
supermarket-management-system/
├── src/
│   ├── main.cpp                # Entry point — menu loop, role-based dispatch
│   ├── models/
│   │   ├── Product.cpp / .h
│   │   ├── Customer.cpp / .h
│   │   ├── Transaction.cpp / .h
│   │   ├── Supplier.cpp / .h
│   │   └── User.cpp / .h       # Base class; Admin, Manager, Cashier derive from this
│   ├── inventory/
│   │   ├── InventoryManager.cpp / .h
│   │   └── ExpiryMonitor.cpp / .h
│   ├── billing/
│   │   ├── Checkout.cpp / .h
│   │   └── ReturnsManager.cpp / .h
│   ├── loyalty/
│   │   └── LoyaltyLedger.cpp / .h
│   ├── suppliers/
│   │   └── PurchaseOrderManager.cpp / .h
│   ├── reports/
│   │   └── ReportGenerator.cpp / .h
│   ├── auth/
│   │   └── AuthManager.cpp / .h
│   └── storage/
│       └── FileHandler.cpp / .h   # Read/write for all persisted records
├── data/                        # Persisted data files (products.txt, customers.txt, etc.)
├── docs/
│   └── proposal.md              # Project proposal / design document
├── tests/                       # Manual test cases and sample data files
├── Makefile
├── .gitignore
└── README.md
```

> The structure above reflects the intended modular design (each subsystem as its own class/component); files are added incrementally as development proceeds.

## Getting Started

### Prerequisites

- A C++ compiler supporting C++17 (GCC 9+ recommended)
- `make` (optional, for the provided Makefile)
- Git

### Clone the repository

```bash
git clone https://github.com/<your-username>/supermarket-management-system.git
cd supermarket-management-system
```

### Build

Using the Makefile:

```bash
make
```

Or directly with g++:

```bash
g++ -std=c++17 -Wall -o sms src/main.cpp src/models/*.cpp src/inventory/*.cpp src/billing/*.cpp src/loyalty/*.cpp src/suppliers/*.cpp src/reports/*.cpp src/auth/*.cpp src/storage/*.cpp
```

### Run

```bash
./sms
```

On first run, the system initializes empty data files under `data/`. Sample seed data for testing can be placed in `tests/sample-data/`.

## Usage

The application runs as a menu-driven console interface. After logging in, the menu shown depends on the authenticated role:

- **Admin** — full access: user management, pricing, suppliers, reports, audit log
- **Manager** — inventory, purchase orders, discounts, reports, refund approval
- **Cashier** — checkout, returns (within limit), stock lookup

## Development Workflow

- Create a feature branch per module: `git checkout -b feature/inventory-module`
- Keep commits scoped to one logical change
- Open a pull request into `main` for review before merging
- Update this README and `docs/proposal.md` if the design changes

## Team

| Name | Roll Number | Role |
|---|---|---|
| _TBD_ | _TBD_ | _TBD_ |
| _TBD_ | _TBD_ | _TBD_ |

## Course Context

- **Course**: Programming Fundamentals, FAST–NUCES Karachi
- **Submission deadline**: September 20, 2026

## License

This project is developed for academic purposes as part of a university course assignment.
