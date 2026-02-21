# Project 3: Secure Feedback & Analytics Portal
(Security-Focused System)

## Problem Statement

Organizations require a secure and structured way to collect feedback from users or employees while ensuring data protection and role-based access.

The objective is to build a Secure Feedback & Analytics Portal that emphasizes authentication, authorization, and clean backend architecture.

This project is designed to showcase security fundamentals and production-style PHP design.

---

## Core Requirements

### Frontend (HTML / CSS / JavaScript)

#### Feedback Submission Form
- Text input
- Rating selection
- Dropdown fields
- Client-side validation before submission

#### Feedback Listing
- Tabular display of feedback
- Sorting functionality
- Filtering capability

---

### Backend (PHP + MySQL)

#### Database Schema
- `users`
- `feedback`

#### Authentication
- Hashed passwords using:
  - `password_hash()`
  - `password_verify()`

#### Role-Based Access Control
- User → Submit feedback
- Admin → View feedback and analytics

---

## Security & Architecture

- CSRF tokens for all form submissions
- Prepared statements only
- Input sanitization
- Output escaping
- Modular PHP structure following MVC-style separation:
  - Models
  - Controllers
  - Views

---

## Scalability & Future Extension

- Pagination-ready feedback listing
- Placeholder analytics dashboard for:
  - Trends
  - Rating distributions

---

## Deliverables

- `index.html` — Feedback form and listings
- `style.css` — Responsive UI
- `feedback.js` — Validation and rendering
- `auth.php` — Authentication logic
- `feedback.php` — Feedback handling logic
- `admin.php` — Admin functionality
- `db.sql` — Database schema
