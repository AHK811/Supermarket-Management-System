# Supermarket Management System --- Project Proposal

**National University of Computer & Emerging Sciences**\
**Karachi Campus**

## Supermarket Management System

### An Integrated Platform for Inventory, Sales, and Customer Management

**Project Proposal**\
**Course:** Programming Fundamentals\
**Program:** BS Software Engineering 1A

### Project Proposed By

-   Azaan Mehdi (26K-3000)
-   M Billal Imtiaz (26K-3020)
-   Abdul Hannan Kashif (26K-3018)

------------------------------------------------------------------------

## 1. Introduction

The Supermarket Management System is an application intended to
computerize and integrate the daily operations of every branch of retail
markets. Rather than treating billing, inventory control, customer
relationships, and reporting as separate manual processes, the system is
designed around a single, consistent set of data records (products,
customers, transactions, and suppliers). This removes the reconciliation
gaps that arise when the same underlying information, for example, how
much stock is left of a product is tracked in more than one place by
more than one person.

The target environment is a small to mid-sized supermarket, such as a
neighborhood store or a campus supermarket, staffed by a small team with
varying levels of technical familiarity. The system is therefore
designed for clarity and predictability of behavior over
configurability: a cashier should be able to complete a sale in a few
structured steps, while a manager or admin has access to additional
operations (pricing, discounts, supplier orders, and reports) that are
deliberately separated from routine checkout functions.

## 2. Existing System

Most small and mid-sized supermarkets today rely on one of three
approaches: fully manual record-keeping (registers and paper logs),
spreadsheet-based tracking kept by a single employee, or a basic
point-of-sale (POS) terminal that focuses primarily on the checkout
transaction. Across these approaches, a set of recurring characteristics
and limitations can be observed:

1.  **Transaction-centric design.** Commodity POS software is generally
    built around the scan-price-print receipt cycle. Inventory is
    usually decremented as a side effect of a sale rather than treated
    as a first-class, continuously monitored resource.
2.  **Periodic rather than continuous stock checks.** Stock levels are
    typically verified through manual shelf audits or end-of-day batch
    reconciliation, so a shortage is discovered after it has already
    affected a customer, not before.
3.  **Static, pre-defined reporting.** Where reporting exists, it is
    usually limited to a small set of fixed templates (e.g., a daily
    total), rather than reports generated on request against arbitrary
    date ranges, categories, or item rankings.
4.  **Loosely coupled loyalty schemes.** Customer loyalty or
    discount-card systems are often bolted on as a separate module or a
    third-party card processor, requiring manual reconciliation between
    the loyalty ledger and the billing ledger.
5.  **Coarse or absent access control.** Many small-scale systems give
    all staff members the same level of access, so price changes,
    discount applications, and transaction voids are not restricted to
    authorized roles, and there is no audit trail of who performed a
    sensitive action.
6.  **No automated expiry tracking.** Perishable-goods expiry is
    generally tracked, if at all, through manual shelf inspection, which
    detects spoilage only after it has already occurred.
7.  **Reactive supplier restocking.** Reordering from suppliers is
    usually initiated only once an employee notices a shortage, rather
    than being triggered automatically when stock crosses a defined
    threshold.
8.  **Unstructured returns handling.** Refunds and exchanges are often
    processed without a documented link back to the original
    transaction, which weakens traceability of daily cash and inventory
    totals.

## 3. Problem Statement

The limitations of the existing approach translate into concrete,
recurring problems that the proposed system is intended to resolve:

1.  **Delayed stockout awareness.** Because stock levels are not checked
    continuously, staff typically learn that a product is unavailable
    only when a customer tries to purchase it, resulting in a lost sale
    and degraded customer experience.
2.  **Fragmented loyalty tracking.** When reward points or spending
    thresholds are tracked outside the billing system, customers can be
    under-rewarded, double-counted, or omitted entirely due to manual
    reconciliation errors.
3.  **Manual, delayed reporting.** Without on-demand reporting, owners
    and managers must manually total receipts to gauge sales
    performance, which slows down decisions such as reordering or
    running a promotion.
4.  **Undifferentiated access control.** When every employee can modify
    prices, apply discounts, or delete transactions, the system carries
    an avoidable fraud and accountability risk, with no record of who
    performed a sensitive action.
5.  **Perishable goods waste.** Without automated expiry alerts, staff
    can remain unaware that a product is near or past its expiry date
    until the loss has already occurred.
6.  **Reactive supplier restocking.** Because reordering depends on a
    human noticing a shortage, normal supplier lead times translate into
    recurring, avoidable gaps on the shelf.
7.  **Unstructured returns handling.** Refunds that are not linked to
    the original sale reduce the traceability of daily cash totals and
    make it difficult to verify that a return is legitimate.

## 4. Proposed Solution

The proposed system addresses each of the problems above through a
dedicated mechanism, all operating against the same underlying product,
customer, transaction, and supplier records so that no data is
duplicated across modules:

1.  **Real-time inventory engine.** Every checkout, restock, or manual
    adjustment updates a shared stock record immediately. Each product
    carries a configurable low-stock threshold that, once crossed,
    raises an alert at system startup, during checkout, and on the
    manager's summary view, rather than waiting for a scheduled batch
    job.
2.  **Integrated loyalty ledger.** Every completed transaction updates
    the customer's cumulative spend and issues loyalty points or tier
    status as part of the same operation that records the sale, so there
    is a single customer record used whenever points or purchases are
    updated.
3.  **On-demand report generation.** Daily, weekly, and monthly sales
    reports, category breakdowns, and top-selling or slow-moving item
    lists are computed at request time directly from the transaction
    records, instead of requiring receipts to be re-entered or totaled
    by hand.
4.  **Role-based access control (RBAC).** Three roles---Admin, Manager
    and Cashier---are each assigned a fixed set of permissions (for
    example, only a Manager or Admin may edit prices or approve a refund
    above a set amount). Every privileged action is written to an
    append-only audit log with a timestamp and the acting user's
    identifier.
5.  **Expiry monitoring subsystem.** Each inventory batch stores an
    expiry date; a check run at startup and at defined intervals flags
    items that fall within a configurable near-expiry window, optionally
    suggesting a markdown price to reduce wastage.
6.  **Supplier and purchase-order module.** Each product is linked to a
    preferred supplier and a reorder threshold and quantity. When stock
    crosses the threshold, the system drafts a purchase order
    automatically for manager approval, instead of waiting for the
    shortage to be noticed manually.
7.  **Structured returns workflow.** A return references the original
    transaction identifier, confirms that the returned item and quantity
    were part of that transaction, reverses the associated loyalty-point
    effect proportionally, restores the inventory count, and is written
    to the audit log.

As this is a Programming Fundamentals course project, the system will be
implemented as a single-terminal, menu-driven console application built
around object-oriented design and file-based persistence (see Section
6). Each subsystem described above corresponds to a distinct class or
module, so that the design can later be extended to a multi-terminal,
database-backed, or graphical system without requiring a structural
rewrite.

## 5. Salient Features

### Authentication and Roles

-   Login for three roles: Admin, Manager and Cashier, with
    permission-gated access to sensitive operations.

### Inventory Management

-   Add, update, remove, and search products by ID, name, or category.
-   Supplier association and batch-level expiry tracking for perishable
    goods.

### Real-Time Stock Alerts

-   Configurable low-stock thresholds per product, checked at startup
    and at every checkout.

### Checkout and Billing

-   Cart-based checkout with itemized receipts showing unit price,
    quantity, discount, and tax.
-   Support for recording the payment mode used for each transaction.

### Customer and Loyalty Management

-   Customer profiles with cumulative spend and automatic point or tier
    issuance at configurable thresholds.

### Discount and Promotion Engine

-   Percentage and fixed-value discounts, promotional codes, and
    expiry-driven markdown suggestions.

### Returns and Refunds

-   Transaction-linked returns with automatic inventory restoration and
    loyalty-point reversal.

### Reporting and Analytics

-   On-request daily, weekly, and monthly sales reports.
-   Top-selling and slow-moving item rankings, and category-wise sales
    breakdowns.

### Supplier and Purchase-Order Management

-   Supplier directory with automatic purchase-order drafts once a
    reorder threshold is crossed.

### Audit Logging

-   Append-only log of privileged actions (price edits, discounts,
    refunds, user management) with timestamp and user attribution.

### Data Persistence and Reliability

-   Structured file-based storage with defined record formats for
    products, customers, transactions, and suppliers, so data persists
    across sessions.
-   Input validation and defensive error handling for invalid
    quantities, duplicate IDs, out-of-range prices, and malformed
    records.

### Stretch Goal

-   A simple text-based summary view (e.g., ASCII bar chart) of
    top-selling products for the requested period, time permitting.

## 6. Tools & Technologies

The following stack is proposed for the implementation:

### Programming Language

**C++** --- chosen for alignment with the Programming Fundamentals
course. Classes are used for Product, Customer, Transaction, User, and
Supplier; role hierarchy (Admin, Manager, Cashier) is implemented via
inheritance from a base User class; discount and pricing variations use
simple polymorphic strategies.

### Data Structures

**C++ Standard Template Library (STL):** `vector` for product and
transaction lists, `map` / `unordered_map` for constant-time product
lookup by ID, and `queue` for processing items during checkout.

### Persistence

File handling via `fstream`, with defined record formats for Products,
Customers, Transactions, Suppliers, and the Audit Log. Storage access is
isolated behind a small interface so that an upgrade to a lightweight
database (e.g., SQLite), if permitted, would not require changes to
business logic.

### Development Environment

GCC / g++ or Visual Studio; Git for version control to track incremental
progress across group members.

### Operating System

Cross-platform console application (Windows and Linux); no OS-specific
APIs, to keep the codebase portable.

### Testing Approach

Manual test cases per module, exercised against a small set of sample
data files, to validate inventory decrement logic, threshold triggers,
and report totals prior to submission.

> **Note:** The language choice above assumes standard course
> conventions; if the instructor specifies a different language, the
> same class structure, STL-equivalent containers, and file-based
> persistence pattern apply directly.

## 7. Expected Outcome

On completion, the system is expected to demonstrate a working,
menu-driven Supermarket Management System that keeps a single,
consistent record of inventory, customers, transactions, and suppliers;
enforces role-based access to sensitive operations; and generates sales
and stock information on request rather than through manual tallying.
The modular class structure is intended to allow the project to be
extended beyond the course submission---for example, toward a
database-backed or multi-terminal version---without a fundamental
redesign.
