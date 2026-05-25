# Food Delivery Management System

A full-stack, responsive food ordering application and separate order management control desk dashboard. Built with **Next.js (App Router)**, **Tailwind CSS**, and **MongoDB (Mongoose)**.

Both the user website and admin panel are built with a premium, clear, light theme utilizing soft off-white/slate backgrounds, charcoal typography, sunset orange highlights, and fresh emerald accents.

---

## Project Structure

```text
G:\Codezela\food delivery\
├── website/             # Client Food Ordering Site (Runs on port 3000)
│   ├── src/app/         # Next.js App Router Page Layouts & API Routes
│   ├── src/components/  # Frosted Glass Header, Footer components
│   ├── src/context/     # Shopping Cart Context State Management
│   ├── src/lib/         # Cached MongoDB connection file
│   └── src/models/      # Mongoose schemas (Order, Admin)
│
└── admin/               # Order Control Dashboard (Runs on port 3001)
    ├── src/app/         # Login Page, Dashboard grid, Auth API routes
    ├── src/lib/         # JWT Security Signers, DB utilities
    └── seed.js          # Independent Database Seeding Script
```

---

## Technology Stack

* **Frontend Framework**: Next.js 15 (React 19)
* **Backend Database Adapter**: Mongoose (MongoDB Client)
* **Styling framework**: Tailwind CSS (v4)
* **Security & Auth**: JSON Web Tokens (JWT) & HTTP-Only Secure Cookies, crypt-hashed passwords via bcryptjs
* **Vector Icons**: Lucide React

---

## Getting Started

### 1. Database Configuration
Both apps use `.env.local` files to read database credentials. Ensure you have the database credentials configured:
- Create or check [**`website/.env.local`**](file:///G:/Codezela/food%20delivery/website/.env.local) and [**`admin/.env.local`**](file:///G:/Codezela/food%20delivery/admin/.env.local).
- Make sure `MONGODB_URI` contains your MongoDB Atlas connection string:
  ```env
  MONGODB_URI=mongodb+srv://savinda:sdlove01@cluster0.9ucw66b.mongodb.net/food_delivery?appName=Cluster0
  ```

### 2. Run Database Seeding
To verify database connections and load mock data, run the seed script:
```powershell
cd "G:\Codezela\food delivery\admin"
node seed.js
```
This script will:
* Check your MongoDB Atlas connection.
* Automatically seed the default admin account:
  * **Username**: `admin`
  * **Password**: `admin123`
* Create a test customer order so your dashboard starts with sample details.

---

## Running the Applications Locally

You can spin up both development servers concurrently on different ports:

### A. Run Client Ordering Website
Open a terminal tab:
```powershell
cd "G:\Codezela\food delivery\website"
npm run dev
```
* Access the customer website at: **[http://localhost:3000](http://localhost:3000)**
* Available routes:
  * `/` - Interactive Home page with Hero slide
  * `/about` - Core kitchen values and sanitation checklist
  * `/menu` - Organic foods grid with quick Add-to-Cart actions
  * `/cart` - Dynamic orders tray calculation and checkout forms
  * `/contact` - Direct support info and validated customer inquiry form

### B. Run Admin Control Panel
Open a second terminal tab:
```powershell
cd "G:\Codezela\food delivery\admin"
npm run dev -- -p 3001
```
* Access the control desk at: **[http://localhost:3001](http://localhost:3001)**
* Available routes:
  * `/login` - Secure administrator access login card
  * `/dashboard` - Protected dashboard containing order status toggles, real-time KPI metrics, search filtering, and deletion options.

---

## Security Verification (JWT Cookies)
All dashboard operations are secured behind Server Component redirects. The server checks for the presence of the `admin_token` cookie. If not present or if verification fails, the server rejects traffic and routes the user back to the login form immediately.
