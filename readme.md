# CREX 👕✨

Custom merchandise design platform built using Firebase, Fabric.js, and modern frontend workflows.

> Design. Customise. Preview. Order.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🚀 Overview

CREX is a creative merchandise customisation platform developed for internal organisation use.

Users can:
- Create custom apparel designs
- Add logos and graphics dynamically
- Preview products in real-time
- Save projects
- Manage cart & orders
- Submit feedback

The platform combines:
- Interactive frontend experiences
- Firebase backend services
- Canvas-based editing workflows
- Real-time cloud storage

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## ⚙️ Tech Stack

### Frontend
- HTML5
- CSS3
- JavaScript
- Bootstrap
- Fabric.js
- html2canvas

### Backend / Cloud
- Firebase Authentication
- Firebase Realtime Database
- Firebase Firestore
- Firebase Storage

### Additional
- Express.js (Vendor Demo API)
- SweetAlert2

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## ✨ Key Features

- 🔐 Firebase Authentication
- 🎨 Interactive Design Canvas
- 🖼 Dynamic Logo Management
- 🛒 Cart & Checkout Workflow
- ☁️ Cloud Image Storage
- 📦 Order Management
- 💬 Feedback System
- 📁 Saved Project Management

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# 🧠 System Architecture

```text
+------------------+     +-------------------------+
| Browser / HTML   |---->| Firebase Auth           |
| (Static pages)   |     +-------------------------+
| Fabric.js        |     +-------------------------+
| html2canvas      |---->| Firebase Storage        |
|                  |     | Users/{username}        |
|                  |     | CartFolder/...          |
|                  |     +-------------------------+
|                  |     +-------------------------+
|                  |---->| Firebase Realtime DB    |
|                  |     | crex/users              |
|                  |     | crex/product            |
|                  |     | crex/feedback           |
|                  |     | orders                  |
|                  |     +-------------------------+
|                  |     +-------------------------+
|                  |---->| Firebase Firestore      |
|                  |     | images / onam           |
|                  |     +-------------------------+
| Vendor Demo      |     +-------------------------+
| (optional page)  |---->| Express API :3000       |
+------------------+     +-------------------------+
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 📸 Project Preview

### Home Page
![Home Preview](./assets/home-preview.png)

### Design Tool
![Design Tool](./assets/design-tool.gif)

### Cart Workflow
![Cart Preview](./assets/cart-preview.png)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🔄 Application Flow

1. User registers/login using Firebase Auth
2. Product assets load dynamically from Firestore
3. User customises merchandise using Fabric.js canvas
4. html2canvas captures preview images
5. Assets uploaded to Firebase Storage
6. Cart & order data stored in Firebase DB
7. Checkout & feedback workflow executed

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🛠 Installation

```bash
git clone https://github.com/albykennady/Crex.git

cd Crex
```

Open `index.html` using Live Server or any static server.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 📂 Folder Structure

```bash
assets/
css/
js/
vendor-server/
firebase/
pages/
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🎯 Future Improvements

- AI-assisted design suggestions
- Payment gateway integration
- Responsive mobile-first redesign
- React migration
- Spring Boot backend migration
- Admin analytics dashboard

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 👨‍💻 Author

### Alby Kennedy

Software Engineer focused on:
- Full Stack Development
- Spring Boot
- React.js
- iOS Development
- Creative Frontend Engineering
- AI-integrated Applications

GitHub:
https://github.com/albykennady

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## ⭐ If you like this project

Give it a star and follow for upcoming full-stack and creative engineering projects.
