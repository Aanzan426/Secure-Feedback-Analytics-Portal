# 📄 **Database Design Documentation**

## Secure Feedback & Analytics Portal

---

# 1️⃣ WHAT (What is this system?)

This system is a:

> **Secure, structured, and scalable feedback management system**

It enables:

* Users to submit feedback
* Admins to manage, analyze, and act on feedback
* Secure handling of sensitive data

---

## Core Capabilities

* Authentication & user management
* Feedback submission and classification
* Role-based access control
* Secure session handling
* Audit logging
* Tagging and categorization
* Analytics-ready data structure

---

# 2️⃣ WHY (Why are we building this?)

## Problem Statement

Traditional feedback systems suffer from:

### 🔻 Lack of structure

* Feedback stored as plain text
* No categorization or metadata

### 🔻 Lack of security

* No encryption
* Vulnerable to SQL injection, XSS, CSRF

### 🔻 Lack of usability

* No filtering
* No analytics
* No prioritization

---

## Solution

This system solves those problems by:

* Structuring feedback into relational tables
* Securing data using best practices
* Making feedback actionable through metadata

---

## Strategic Value

This project demonstrates:

* Backend system design
* Database normalization
* Security engineering
* Real-world architecture thinking

---

# 3️⃣ WHO (Who uses this system?)

## Actors

### 👤 User

* Registers and logs in
* Submits feedback
* Views own submissions (optional)

---

### 🛡 Admin

* Views all feedback
* Filters and analyzes data
* Updates status and priority
* Monitors system activity

---

### ⚙ System

* Validates input
* Manages sessions
* Logs actions
* Enforces security rules

---

# 4️⃣ WHERE (Where is data stored and used?)

## Data Storage

* MySQL relational database
* Structured tables with relationships

---

## Data Flow

```text
User Input → Backend Validation → Secure Processing → Database Storage → Admin Retrieval → Analysis
```

---

## Usage Points

* Frontend forms (input)
* Backend controllers (processing)
* Database (storage)
* Admin dashboard (output)

---

# 5️⃣ WHEN (When does each part operate?)

| Component          | Trigger                |
| ------------------ | ---------------------- |
| User creation      | Registration           |
| Authentication     | Login                  |
| Session creation   | Successful login       |
| Feedback insertion | Form submission        |
| Encryption         | Before DB insert       |
| Logging            | On every admin action  |
| Analytics          | Admin dashboard access |

---

# 6️⃣ HOW (How does the system work?)

## 🔁 End-to-End Flow

### Step 1: User Authentication

* Credentials verified using hashed passwords
* Session created and stored

---

### Step 2: Feedback Submission

1. User fills form
2. Input validated (client + server)
3. Data sanitized
4. (Optional) encrypted
5. Stored in database

---

### Step 3: Storage Design

Feedback is stored with:

* user linkage
* category classification
* metadata (status, priority)

---

### Step 4: Admin Access

* Admin retrieves feedback
* Filters using indexed columns
* Updates status or priority

---

### Step 5: Logging

Every critical action:

* stored in `feedback_logs`
* linked to user + feedback

---

# 7️⃣ HOW MUCH (Scale, performance, impact)

## Performance Considerations

* Indexed columns:

  * user_id
  * category_id
  * status
* Composite index for filtering

---

## Scalability

Supports:

* thousands of users
* large feedback datasets
* real-time filtering

---

## Security Coverage

* SQL injection prevention
* XSS mitigation
* CSRF protection
* password hashing
* session control

---

 # 🚀 POSSIBLE IMPROVEMENTS

---

## 🔹 Short-Term

* Add pagination support
* Add search queries
* Add sorting logic

---

## 🔹 Mid-Level

* Replace ENUM with lookup tables
* Add API layer
* Add rate limiting

---

## 🔹 Advanced

* AES encryption for feedback_text
* RSA key exchange
* key management system

---

## 🔹 Elite (AI Integration)

* sentiment analysis
* feedback clustering
* anomaly detection

---

---

# 22nd March, 2026 - Day 1

---

# 🔹 TABLE: `users`

## Purpose

Stores user identity and authentication data.

---

## Columns

| Column        | Type      | Purpose                 |
| ------------- | --------- | ----------------------- |
| user_id       | INT       | Unique identifier       |
| username      | VARCHAR   | Display name            |
| email         | VARCHAR   | Login identity          |
| password_hash | VARCHAR   | Secure password storage |
| role          | ENUM      | Access control          |
| created_at    | TIMESTAMP | Account creation time   |
| last_login    | DATETIME  | Activity tracking       |

---

## Why this table?

* Enables authentication
* Supports role-based access
* Tracks user activity

---

# 🔹 TABLE: `categories`

## Purpose

Defines feedback classification types.

---

## Columns

| Column        | Type    | Purpose     |
| ------------- | ------- | ----------- |
| category_id   | INT     | Unique ID   |
| category_name | VARCHAR | Type label  |
| description   | TEXT    | Explanation |

---

## Why?

Avoids:

* multiple tables
* hardcoded logic

---

# 🔹 TABLE: `feedback`

## Purpose

Stores all feedback entries.

---

## Columns

| Column        | Type      | Purpose            |
| ------------- | --------- | ------------------ |
| feedback_id   | INT       | Unique identifier  |
| user_id       | INT       | Who submitted      |
| category_id   | INT       | Type of feedback   |
| rating        | TINYINT   | Quantitative input |
| feedback_text | TEXT      | Main content       |
| is_encrypted  | BOOLEAN   | Security flag      |
| status        | ENUM      | Workflow state     |
| priority      | ENUM      | Importance level   |
| created_at    | TIMESTAMP | Creation time      |
| updated_at    | TIMESTAMP | Last update        |

---

## Why?

This is the **core data table**.

---

## Key Design Decisions

* Single table for all feedback
* Classification via category
* Workflow via status + priority

---

# 🔹 TABLE: `sessions`

## Purpose

Tracks active user sessions securely.

---

## Columns

| Column     | Type      | Purpose              |
| ---------- | --------- | -------------------- |
| session_id | VARCHAR   | Unique session token |
| user_id    | INT       | Linked user          |
| ip_address | VARCHAR   | Security tracking    |
| user_agent | TEXT      | Device/browser info  |
| created_at | TIMESTAMP | Session start        |
| expires_at | DATETIME  | Expiry               |

---

## Why?

* Prevent session hijacking
* Enable session expiration
* Audit user activity

---

# 🔹 TABLE: `feedback_logs`

## Purpose

Maintains audit trail of actions.

---

## Columns

| Column       | Type      | Purpose              |
| ------------ | --------- | -------------------- |
| log_id       | INT       | Unique ID            |
| feedback_id  | INT       | Related feedback     |
| action       | VARCHAR   | Action performed     |
| performed_by | INT       | Admin/user ID        |
| timestamp    | TIMESTAMP | When action happened |

---

## Why?

* Traceability
* Accountability
* Security monitoring

---

# 🔹 TABLE: `feedback_tags`

## Purpose

Allows flexible tagging of feedback.

---

## Columns

| Column      | Type    | Purpose         |
| ----------- | ------- | --------------- |
| tag_id      | INT     | Unique ID       |
| feedback_id | INT     | Linked feedback |
| tag_name    | VARCHAR | Label           |

---

## Why?

* Dynamic classification
* Better analytics
* Search/filter enhancement

---

# 🔍 INDEXING STRATEGY

## Why indexing?

To optimize:

* search
* filtering
* admin dashboard queries

---

## Indexed Fields

* email (login)
* user_id (joins)
* category_id (filtering)
* status (dashboard)
* composite index (multi-filter queries)

---

---

#___ - Day 2
