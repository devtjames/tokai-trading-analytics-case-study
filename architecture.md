# Tokai Architecture

## Overview

Tokai is designed as a backend-first system with strict separation of responsibilities.  
Each layer has a single purpose and clear boundaries.

The architecture favors correctness, repeatability, and long-term data safety.

---

## High-Level Components

Tokai is composed of four main layers:

1. External Data Source
2. Sync Engine
3. Database Layer
4. Presentation Layer

---

## 1. External Data Source

**Myfxbook API**

Provides access to:

- Trading accounts
- Balances
- Deposits
- Profits
- Trade history (limited rolling window)

Constraints handled by Tokai:

- Session expiration
- Limited trade history
- Changing financial values

---

## 2. Sync Engine

The sync engine is the core backend process.

### Execution Modes

- Automated cron execution
- Manual execution via admin panel

### Responsibilities

- Authenticate with Myfxbook
- Fetch accounts and trade data
- Validate incoming data
- Normalize timestamps and values
- Synchronize records safely

Each sync run starts with a fresh API login and ends with session disposal.

---

## 3. Database Layer

The database is the single source of truth.

### Core Tables

- `accounts`
- `account_history`
- `trades`

### Guarantees

- Unique constraints prevent duplicates
- Controlled updates protect historical records
- Time-based accuracy is enforced

Trade uniqueness is based on:

- `accountId`
- `openTime`

This allows safe repeated syncs without corruption.

---

## 4. Presentation Layer

The frontend never reads directly from the API.

It only displays normalized database data:

- Masked account numbers
- Balances and profits
- Historical performance
- Monthly aggregation

Charts and dashboards reflect stored truth, not transient API responses.

---

## Data Flow Summary

1. Sync is triggered (cron or manual)
2. Fresh authentication is created
3. Accounts are synced
4. Trade history is synced
5. Data is stored or updated safely
6. Frontend reads normalized records

---

## Design Focus

- Backend reliability
- Financial data correctness
- Safe automation
- Clear separation of concerns
