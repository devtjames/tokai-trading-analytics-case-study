# Tokai – Trading Data Sync & Analytics System

## Overview

Tokai is an automated backend system that synchronizes live trading data from the Myfxbook API, stores it safely, and presents accurate performance analytics across multiple trading accounts.

Tokai is not a trading bot and not a manual import tool.  
It acts as a reliable data backbone for monitoring trading performance over time.

The system is designed to run unattended, handle API constraints, and keep financial data consistent even when syncs are repeated.

---

## Problem Statement

Third-party trading platforms like Myfxbook introduce real operational challenges:

- API sessions expire frequently
- Trade history is limited to a rolling window
- Financial values can change after trade closure
- Duplicate records can occur during repeated syncs
- Financial data must remain accurate at all times

Tokai exists to control these issues and provide a stable and auditable data layer.

---

## Screenshots

### Home
![1  HOMEPAGE](https://github.com/user-attachments/assets/2927e906-7c36-44d1-8bdb-1a47916d4649)


### Admin Login
![2  ADMIN LOGIN](https://github.com/user-attachments/assets/fd75d8e3-91df-42fa-8518-a02b733f63e2)


### Dashboard
![3  ADMIN DASHBOARD](https://github.com/user-attachments/assets/f8e61921-fce8-481d-b518-0738d992804b)


### Trade Sync History & Analysis
![4  ADMIN SYNC TRADING ANALYSIS HISTORY](https://github.com/user-attachments/assets/42d61a84-7abe-4dc7-b565-2f9a7ad046cf)


### Mobile Dashboard View
![5  ADMIN MOBILE DASHBOARD](https://github.com/user-attachments/assets/3afa2ee3-9330-485e-aba1-327e2f25d675)



---

## Core Features

- Automated Myfxbook API synchronization
- Cron-based and manual sync execution
- Fresh authentication on every sync
- Idempotent trade history processing
- Duplicate-safe inserts and controlled updates
- Accurate balance, profit, and gain tracking
- Masked trading account identifiers
- Monthly and historical performance views
- Admin interface for monitoring and manual sync control

---

## Tech Stack

- **Backend:** PHP  
- **Database:** MySQL  
- **Frontend:** HTML, TailwindCSS, JavaScript  
- **Server:** Apache (XAMPP for local development)  
- **Version Control:** Git and GitHub  

---

## My Role

I handled the full development of the project, including:

- System setup and overall structure  
- Backend logic and data synchronization  
- Database design and data integrity rules  
- UI integration with backend data  
- Deployment and ongoing maintenance  

---

## System Architecture

Tokai is structured around four main layers:

1. External Data Source (Myfxbook API)
2. Sync Engine (cron and manual triggers)
3. Database Layer (normalized financial records)
4. Presentation Layer (dashboards and analytics)

Detailed architecture is documented here:

- `architecture.md`

---

## Data Synchronization Strategy

### Account Synchronization

For each account retrieved from Myfxbook:

- Existing accounts are updated
- New accounts are created once
- Account identity remains stable over time

This prevents duplicates while keeping balances current.

---

### Trade History Synchronization

Trade history synchronization is the core of the system.

- Myfxbook returns only recent trades
- Trades may reappear across multiple syncs
- Profit values may update after closure

Tokai handles this by:

- Identifying trades using `accountId + openTime`
- Enforcing database-level uniqueness
- Inserting new trades
- Updating existing trades safely
- Ignoring duplicates without errors

Repeated syncs always produce the same correct result.

---

## Data Integrity

Tokai is built with idempotency as a first-class principle.

Running the same sync multiple times will never corrupt data.  
This allows the system to run hourly, daily, or on-demand without risk.

---

## Time & Date Handling

- API timestamps are converted to MySQL `DATETIME`
- Exact trade times are preserved
- Dates are normalized for aggregation and charts

This enables accurate historical and monthly analytics.

---

## Admin Capabilities

The admin interface allows:

- Manual synchronization triggers
- Sync monitoring
- Data inspection for accounts and trades

This supports both automation and operational control.

---

## Localization

The default interface language is **pt-BR (Portuguese – Brazil)**.

---

## Development Notes

- The production source code is private.  
- This repository exists to document the system design, technical decisions, and overall approach.  
- Screenshots, architecture notes, and decisions reflect the real production system.  

For code samples, see my other public repositories.

---

## Documentation

- `architecture.md` – system structure and data flow  
- `decisions.md` – technical decisions and trade-offs  

---

## Live System

https://tokaielite.com/

---

## Contact

If you want to discuss this project or review the code privately, feel free to reach out.
