# NTC Equipment & Resource Booking System

## Overview

The **NTC Equipment & Resource Booking System** is a full-stack web application designed to digitize the management, availability tracking, and reservation of shared equipment and resources within an organization such as Nepal Telecom.

The system provides a centralized platform where staff members can view available equipment, submit booking requests, and track their reservations. Administrators can manage equipment, categories, users, and reservations.

A key feature of the system is the prevention of **double-booking** by validating reservation time periods before a booking is confirmed.

---

## Project Objectives

The main objectives of this project are:

* Digitize the management of shared equipment and resources.
* Provide a centralized equipment reservation system.
* Allow staff to check equipment availability.
* Allow staff to submit equipment booking requests.
* Prevent double-booking through time conflict validation.
* Manage the complete equipment lifecycle.
* Provide separate Staff and Admin access.
* Apply full-stack web development concepts using the MERN stack.
* Gain practical experience in database design, REST APIs, authentication, authorization, and frontend development.

---

## Technology Stack

This project is developed using the **MERN Stack**.

### Frontend

* React.js
* Tailwind CSS
* Axios
* React Router

### Backend

* Node.js
* Express.js

### Database

* MongoDB
* Mongoose

### Authentication & Security

* JSON Web Token (JWT)
* bcryptjs
* Environment Variables using dotenv

---

## System Architecture

```text
┌─────────────────────────────┐
│      React Frontend         │
│                             │
│  Staff Dashboard            │
│  Admin Dashboard            │
└──────────────┬──────────────┘
               │
               │ HTTP Requests / REST API
               │
               ▼
┌─────────────────────────────┐
│   Node.js + Express.js      │
│                             │
│   Authentication            │
│   Equipment Management      │
│   Reservation Management    │
│   Booking Validation        │
└──────────────┬──────────────┘
               │
               │ Mongoose
               │
               ▼
┌─────────────────────────────┐
│          MongoDB            │
│                             │
│ Users                       │
│ Equipment                   │
│ Categories                  │
│ Reservations                │
└─────────────────────────────┘
```

---

# Project Features

## 1. User Authentication

The system will provide secure authentication for users.

Features include:

* User registration
* User login
* JWT authentication
* Password hashing using bcrypt
* Protected routes
* Logout functionality

---

## 2. User Roles

The system contains two primary user roles.

### Staff

Staff users can:

* Login to the system
* View available equipment
* Search for equipment
* Filter equipment by category
* Check equipment availability
* Submit booking requests
* View their reservations
* Cancel reservations when permitted
* Track reservation status

### Admin

Admin users can:

* Manage equipment
* Add new equipment
* Update equipment information
* Remove equipment
* Manage equipment categories
* View all reservations
* Approve or reject booking requests
* Mark equipment as checked out
* Mark equipment as returned
* Manage users
* View dashboard statistics

---

# Equipment Management

Each equipment item will contain information such as:

```text
Equipment Name
Category
Serial Number
Description
Location
Status
Created Date
```

Examples of equipment may include:

* Optical Fiber Fusion Splicer
* OTDR Testing Meter
* Field Laptop
* Spectrum Analyzer
* Service Vehicle
* Network Testing Equipment

---

# Equipment Status

Equipment can have the following statuses:

* Available
* Reserved
* Checked-Out
* Under Maintenance
* Unavailable

The exact status will be updated according to equipment availability and reservation activity.

---

# Reservation Management

A staff member can submit a reservation containing:

```text
Equipment
Start Date and Time
End Date and Time
Purpose
Reservation Status
```

The reservation lifecycle is:

```text
Available
    ↓
Booking Requested
    ↓
Approved / Reserved
    ↓
Checked-Out
    ↓
Returned
    ↓
Available
```

A reservation may also be:

```text
Rejected
Cancelled
```

---

# Double-Booking Prevention

One of the most important features of this project is preventing multiple users from booking the same equipment during overlapping time periods.

Before creating a reservation, the backend will check for an existing reservation.

A time conflict exists when:

```text
New Start Time < Existing End Time

AND

New End Time > Existing Start Time
```

Example:

```text
Existing Booking:

Equipment: OTDR Meter
Start: 10:00 AM
End:   2:00 PM


New Booking:

Start: 1:00 PM
End:   3:00 PM


Result:

❌ Booking Conflict
```

The system will reject the conflicting reservation.

---

# Database Models

## User Model

```text
User
├── _id
├── name
├── email
├── password
├── role
├── createdAt
└── updatedAt
```

Roles:

```text
staff
admin
```

---

## Category Model

```text
Category
├── _id
├── name
├── description
├── createdAt
└── updatedAt
```

---

## Equipment Model

```text
Equipment
├── _id
├── name
├── category
├── serialNumber
├── description
├── location
├── status
├── createdAt
└── updatedAt
```

---

## Reservation Model

```text
Reservation
├── _id
├── user
├── equipment
├── startTime
├── endTime
├── purpose
├── status
├── approvedBy
├── createdAt
└── updatedAt
```

---

# Project Folder Structure

```text
ntc-equipment-booking/
│
├── client/
│   │
│   ├── public/
│   │
│   ├── src/
│   │   │
│   │   ├── components/
│   │   ├── pages/
│   │   ├── layouts/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── utils/
│   │   ├── App.jsx
│   │   └── main.jsx
│   │
│   └── package.json
│
├── server/
│   │
│   ├── config/
│   │   └── db.js
│   │
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── equipmentController.js
│   │   ├── categoryController.js
│   │   └── reservationController.js
│   │
│   ├── middleware/
│   │   ├── authMiddleware.js
│   │   └── errorMiddleware.js
│   │
│   ├── models/
│   │   ├── User.js
│   │   ├── Equipment.js
│   │   ├── Category.js
│   │   └── Reservation.js
│   │
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── equipmentRoutes.js
│   │   ├── categoryRoutes.js
│   │   └── reservationRoutes.js
│   │
│   ├── .env
│   ├── .gitignore
│   ├── package.json
│   └── server.js
│
├── .gitignore
├── README.md
└── package.json
```

---

# Backend API Structure

## Authentication APIs

```text
POST   /api/auth/register
POST   /api/auth/login
GET    /api/auth/profile
```

---

## Equipment APIs

```text
GET    /api/equipment
GET    /api/equipment/:id
POST   /api/equipment
PUT    /api/equipment/:id
DELETE /api/equipment/:id
```

---

## Category APIs

```text
GET    /api/categories
POST   /api/categories
PUT    /api/categories/:id
DELETE /api/categories/:id
```

---

## Reservation APIs

```text
GET    /api/reservations
GET    /api/reservations/my-reservations
POST   /api/reservations
PUT    /api/reservations/:id
DELETE /api/reservations/:id
```

Additional admin actions may include:

```text
PUT /api/reservations/:id/approve
PUT /api/reservations/:id/reject
PUT /api/reservations/:id/checkout
PUT /api/reservations/:id/return
```

---

# Environment Variables

The backend uses a `.env` file.

Example:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
```

**Important:** Never upload the `.env` file to GitHub.

Add the following to `.gitignore`:

```text
node_modules
.env
```

---

# Installation

## Clone or Create the Project

```bash
mkdir ntc-equipment-booking
cd ntc-equipment-booking
```

---

## Backend Setup

Navigate to the server folder:

```bash
cd server
```

Install dependencies:

```bash
npm install
```

For development:

```bash
npm run dev
```

The backend server will run on:

```text
http://localhost:5000
```

---

## Frontend Setup

Navigate to the client folder:

```bash
cd client
```

Install dependencies:

```bash
npm install
```

Run the React application:

```bash
npm run dev
```

---

# Development Roadmap

## Phase 1: Project Setup

* [ ] Set up Node.js environment
* [ ] Create project folder
* [ ] Create Express server
* [ ] Connect MongoDB
* [ ] Configure environment variables
* [ ] Set up Git repository

## Phase 2: Database Design

* [ ] Create User model
* [ ] Create Category model
* [ ] Create Equipment model
* [ ] Create Reservation model
* [ ] Define model relationships

## Phase 3: Authentication

* [ ] Create registration API
* [ ] Create login API
* [ ] Hash passwords
* [ ] Generate JWT tokens
* [ ] Create authentication middleware
* [ ] Create role-based authorization

## Phase 4: Equipment Management

* [ ] Create equipment API
* [ ] Add equipment
* [ ] Get equipment
* [ ] Update equipment
* [ ] Delete equipment
* [ ] Add search functionality
* [ ] Add category filtering

## Phase 5: Reservation System

* [ ] Create reservation API
* [ ] Check equipment availability
* [ ] Implement double-booking prevention
* [ ] Create reservation status system
* [ ] Allow reservation cancellation
* [ ] Track reservation history

## Phase 6: Frontend Development

* [ ] Create React project
* [ ] Configure Tailwind CSS
* [ ] Create login page
* [ ] Create registration page
* [ ] Create staff dashboard
* [ ] Create admin dashboard
* [ ] Create equipment pages
* [ ] Create reservation pages

## Phase 7: Integration

* [ ] Connect React frontend to Express API
* [ ] Configure Axios
* [ ] Add authentication tokens
* [ ] Protect frontend routes
* [ ] Handle API errors
* [ ] Add loading states

## Phase 8: Testing

* [ ] Test user registration
* [ ] Test login
* [ ] Test protected routes
* [ ] Test equipment CRUD operations
* [ ] Test reservation creation
* [ ] Test double-booking prevention
* [ ] Test admin permissions
* [ ] Test equipment check-out and return

## Phase 9: Deployment

* [ ] Prepare production environment
* [ ] Deploy backend
* [ ] Deploy frontend
* [ ] Configure production MongoDB
* [ ] Test deployed application

---

# Current Development Progress

### Completed

* [x] Development environment setup
* [x] Node.js setup
* [x] Express.js server setup
* [x] MongoDB connection
* [x] Mongoose configuration
* [x] User model
* [x] bcryptjs installation
* [x] jsonwebtoken installation
* [x] User registration API

### Currently Working On

* [ ] Login API
* [ ] JWT Authentication

### Upcoming

* [ ] Authentication middleware
* [ ] Equipment model
* [ ] Category model
* [ ] Reservation model
* [ ] Equipment management API
* [ ] Double-booking validation
* [ ] React frontend
* [ ] Staff dashboard
* [ ] Admin dashboard

---

# Future Improvements

Possible future improvements include:

* Email notifications
* Booking reminders
* Equipment maintenance scheduling
* Equipment usage reports
* Dashboard analytics
* QR code-based equipment identification
* QR code check-out/check-in
* File attachments for maintenance records
* Advanced search and filtering
* Audit logs
* Notification system
* Mobile-responsive interface

---

# Learning Goals

This project is being developed as a learning-oriented full-stack application.

During development, the following concepts will be learned and applied:

* Node.js fundamentals
* Express.js
* RESTful API development
* MongoDB
* Mongoose
* Database schema design
* CRUD operations
* Authentication
* JWT
* Password hashing
* Middleware
* Role-based authorization
* React.js
* React components
* React hooks
* State management
* API integration
* Tailwind CSS
* Error handling
* Testing
* Deployment

---

# Project Status

🚧 **Project Under Development**

Current Stack:

```text
MongoDB
   +
Express.js
   +
React.js
   +
Node.js
```

---

# Author

Developed as a full-stack internship project for an internal equipment and resource booking system.

---

# License

This project is developed for educational and internship purposes.
