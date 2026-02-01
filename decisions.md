# Technical Decisions

## Why Fresh Authentication Per Sync

Myfxbook API sessions expire without warning.

Reusing sessions causes:
- Silent sync failures
- Partial updates
- Stale financial data

Tokai authenticates on every sync to guarantee correctness and predictability.

---

## Why Idempotent Sync Logic

Financial systems must tolerate retries.

Tokai is designed so that:
- Running the same sync twice produces the same result
- Duplicate records are never created
- Updated values are applied safely

This supports cron execution without manual supervision.

---

## Why Database-Level Uniqueness

Application-level checks alone are not sufficient.

Uniqueness is enforced at the database level to:
- Prevent race conditions
- Protect against logic errors
- Guarantee historical accuracy

The database acts as the final authority.

---

## Why Limited API Data Is Still Safe

Myfxbook returns only recent trades.

Tokai compensates by:
- Updating existing trades
- Preserving older historical records
- Preventing duplicates across rolling windows

This allows long-term analytics using short-window API data.

---

## Why Frontend Never Talks to the API

The frontend only consumes normalized database data.

This avoids:
- Inconsistent values
- API dependency for UI rendering
- Performance issues during sync operations

The backend controls all external communication.

---

## Why This Is a Case Study Repository

This repository focuses on:
- Architecture
- Data handling strategy
- Backend reasoning

The production source code remains private, while system behavior and decisions are documented clearly.

This mirrors real-world systems where reliability matters more than tutorials.
