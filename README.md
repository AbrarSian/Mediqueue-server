# MediQueue – Tutor Booking System (Server API)

### **MediQueue Platform | CAT_02 Project**
* **Project Name:** MediQueue – Tutor Booking System (Backend API)
* **Author:** [AbrarSian](https://github.com/AbrarSian)
* **Server GitHub Repository:** [https://github.com/AbrarSian/Mediqueue-server](https://github.com/AbrarSian/Mediqueue-server)
* **Client GitHub Repository:** [https://github.com/AbrarSian/Mediqueue-client](https://github.com/AbrarSian/Mediqueue-client)
* **API Health Check:** `GET /`

---

## 📄 Project Description
The **MediQueue Server** is a high-performance RESTful API backend engineered with Node.js, Express.js, and MongoDB. It manages tutor directories, coordinates session scheduling with automated slot tracking, provides case-insensitive search and date range filtering, and secures protected endpoints using JWT authentication.

---

## 🚀 Key Features

1. **Intelligent Regex Search Engine:**
   - Multi-field case-insensitive search using MongoDB `$regex` across tutor names, subjects, locations, institutions, and teaching modes.
2. **Date Range Filtering:**
   - Precise filtering of upcoming tutoring sessions using `$gte` and `$lte` operators against session start dates.
3. **Atomic Slot Management:**
   - Automatically decrements available tutor slots (`$inc: { totalSlots: -1 }`) upon successful student booking.
   - Restores slots (`$inc: { totalSlots: 1 }`) if a student or tutor cancels a session.
4. **JWT Security Middleware:**
   - Protects private tutor operations (creation, editing, deletion) and personal booking dashboards with bearer token verification.
5. **Full CRUD for Tutors & Bookings:**
   - Complete endpoints for listing, creating, reading, updating, and cancelling tutor profiles and student bookings.
6. **Vercel Serverless & CORS Ready:**
   - Optimized with preflight handler and `vercel.json` configuration for seamless serverless deployment.

---

## 🛠️ Tech Stack

* **Runtime:** Node.js (v18+)
* **Framework:** Express.js 5
* **Database Driver:** MongoDB Native Driver (`mongodb` v7)
* **Security & Auth:** `jose-cjs` / `jsonwebtoken`
* **CORS & Utilities:** `cors`, `dotenv`, `uuid`
* **Deployment:** Vercel Serverless Functions / Node.js Host

---

## 🗺️ API Endpoints

### Health Check
* `GET /` — API health status and timestamp.

### 1. Tutors Endpoints
* `POST /tutors` — Create a new tutor listing *(Private - Requires JWT)*
* `GET /tutors` — Fetch tutors with query parameters:
  * `?search=<keyword>` — Case-insensitive `$regex` search
  * `?startDate=<YYYY-MM-DD>&endDate=<YYYY-MM-DD>` — Date range filter (`$gte` & `$lte`)
  * `?limit=<number>` — Result limit (e.g., 6 for home page featured list)
* `GET /tutors/:id` — Retrieve single tutor details
* `GET /tutors/user/:email` — Retrieve all tutors created by a user *(Private)*
* `PATCH /tutors/:id` — Update tutor details *(Private)*
* `DELETE /tutors/:id` — Delete a tutor listing *(Private)*

### 2. Bookings Endpoints
* `POST /bookings` — Create a session booking (checks slots & auto-decrements totalSlots) *(Private)*
* `GET /bookings` — Retrieve all bookings *(Private)*
* `GET /bookings/:email` — Retrieve bookings made by student email *(Private)*
* `PATCH /bookings/:id` — Cancel a booking and restore slot back to tutor *(Private)*

### 3. Users Endpoints
* `PATCH /users/:id` — Update user profile display name and avatar *(Private)*

---

## ⚙️ Getting Started (Local Setup)

### 1. Clone the repository
```bash
git clone https://github.com/AbrarSian/Mediqueue-server.git
cd Mediqueue-server
```

### 2. Install dependencies
```bash
npm install
```

### 3. Environment variables
Create a `.env` file in the root folder:
```env
PORT=5000
MONGODB_URI=your_mongodb_connection_uri
CLIENT_URL=http://localhost:3000
JWT_SECRET=your_jwt_secret_key
```

### 4. Run the server
```bash
node index.js
```
The server will start listening on `http://localhost:5000`.
