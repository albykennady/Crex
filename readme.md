CREX
Repo: https://github.com/albykennady/Crex | Generated: 2024-05-24

Overview
CREx is an internal static-web application for designing and ordering custom merchandise, built for members of the Experion organization. Users register and log in via Firebase Authentication, compose designs on product mockups using a Fabric.js canvas editor, save preview images to Firebase Storage, manage a cart backed by Storage and Realtime Database, check out orders, and submit feedback. It is a multi-page static HTML/CSS/JS front end with no SPA framework, using Firebase as its serverless backend. A small optional Express.js demo API provides an in-memory vendor catalog for local experimentation. No public live URL is documented in the repository.

Tech Stack
Frontend — Plain HTML/CSS/JS (browser ES modules and classic scripts); Bootstrap 5.0.0-beta1; Fabric.js 4.5.0; html2canvas 1.3.3 and 0.4.1; SweetAlert2 11; Montserrat font family
Backend — Firebase BaaS (Auth, Realtime Database, Firestore, Storage, Analytics) via JS SDK compat 8.6.1 and modular 10.12.2/10.12.3; optional Node.js/Express 4.19.2 demo API; root package also declares Playwright 1.45.1, @google-cloud/storage 7.11.3, cors-anywhere 0.4.4, and body-parser 1.20.2 (unused in current source)
Database — Firebase Realtime Database and Cloud Firestore
Infrastructure — Static file serving inferred for local development; Firebase backends (Google-hosted); no CI/CD or hosting configuration 
Auth — Firebase Authentication email/password; application-level username stored in browser localStorage

Key Features
Registration — Submit the register form to create a Firebase Auth account, write a profile to Realtime Database, and create a user folder stub in Firebase Storage
Login / Logout — Enter username and password to look up the email in Realtime Database, sign in via Firebase Auth, and store the username in localStorage; logout clears localStorage
Password reset — Click “Forgot password” to trigger Firebase sendPasswordResetEmail
Logo gallery — Load standard design logos from the Firestore images collection on design-tool page load
Onam logos — Load seasonal logos from the Firestore onam collection on specific design pages
Canvas editing — Manipulate Fabric.js objects on a product mockup (move, delete, change background color) in the design tool
Save design to cart — Click “Add to Cart” to capture the mockup container with html2canvas, convert to a blob, and upload previews to Firebase Storage under CartFolder and Users/{username}
Cart view — Open the cart page to list captured cart images, infer product types from Storage folder names, and display unit prices fetched from Realtime Database
Checkout — Click Checkout to write an order record to Realtime Database, delete the cart Storage objects, and redirect to the feedback page
Feedback — Submit a rating and comment, which pushes a timestamped entry to Realtime Database under crex/feedback/{username}
My Projects — View saved personal designs listed from the Users/{username} path in Firebase Storage
Vendor browsing — Demo page that calls the local Express API on port 3000 to filter an in-memory vendor list
Architecture
Pattern — Static-site monolith front end + BaaS (Firebase) with an optional orthogonal Express demo API; all primary business logic runs in the browser, trading duplication for simplicity

System diagram

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

Request lifecycle
User lands on the homepage or navigates to login/register
Registers or logs in via Firebase Auth; username is resolved through Realtime Database and cached in localStorage
Opens a design tool page; Firestore images or onam logos load into a left gallery
Selects a logo and manipulates it on the Fabric.js canvas over a product mockup
Clicks “Add to Cart”; html2canvas captures the mockup and uploads blobs to Firebase Storage
Navigates to the cart page; client lists CartFolder/cart/ items and fetches prices from crex/product/{type}
Clicks Checkout; client writes the order to orders/{orderId} in Realtime Database and deletes cart Storage objects
Redirects to feedback page; submits a rating/comment pushed to crex/feedback/{username}

Data Model
Realtime Database Firestore +------------------+ +------------------+ | crex/users/{u} | | images | | - email | | - dataUrl | | - password | +------------------+ +------------------+ +------------------+ | crex/product/{t} | | onam | | - price | | - dataUrl | +------------------+ +------------------+ | crex/feedback/{u}| | - rating | | - comment | | - timestamp | +------------------+ | orders/{id} | | - username | | - orderItems | | - quantity | | - orderDate | +------------------+

Firebase Storage +------------------+ | Users/{username}/| | CartFolder/{type}/| | CartFolder/cart/ | +------------------+

Key entities
crex/users/{username}: { email, password }
crex/product/{productType}: { price }
orders/{orderId}: { username, orderItems, quantity, orderDate }
crex/feedback/{username}: pushed nodes with rating, comment, ISO timestamp
Firestore images and onam: documents containing a dataUrl string
Storage: user folders, product-type folders, and a cart folder for checkout thumbnails
Conventions
Order IDs use order_ + timestamp; Storage filenames use random integer suffixes
Timestamps are ISO strings for feedback entries
No soft deletes; cart Storage items are permanently removed on checkout

API & Integrations
Base path: http://localhost:3000 (local demo only). No authentication required.

| Method | Path | Auth | Description | |--------|------|------|-------------| | GET | /vendors | None | List all in-memory vendors | | GET | /vendors/:id | None | Get a single vendor by numeric ID | | GET | /vendors/:id/tshirts | None | Get t-shirt array for a vendor | | POST | /vendors | None | Create a new vendor | | POST | /vendors/:id/tshirts | None | Add a t-shirt to a vendor | | PUT | /vendors/:id | None | Update a vendor | | DELETE | /vendors/:id | None | Remove a vendor |

External integrations:

| Service | Purpose | Env var | |---------|---------|---------| | Firebase (project crex-f9f68) | Auth, Realtime Database, Storage, Analytics | N/A — config is hardcoded inline | | Firebase (project product-40143) | Firestore logo assets (images, onam) | N/A — config is hardcoded inline | | gstatic / jsdelivr / cdnjs CDNs | Firebase SDKs, Bootstrap, Fabric.js, html2canvas, SweetAlert2 | N/A |

Environment Variables
No environment variables detected in the codebase.

How to Rebuild
Phase 1 — Project scaffold [ ] Create static HTML entry pages for homepage, login, register, cart, feedback, my projects, and each product design tool, sharing a two-tier header/footer and Montserrat typography [ ] Initialize a root package manifest with the declared Node dependencies (express, playwright, @google-cloud/storage, body-parser, cors-anywhere) and a separate vendor-server manifest with express and cors [ ] Provision two Firebase projects—one for Auth/Realtime Database/Storage (crex-f9f68) and one for Firestore logo assets (product-40143)—and embed the generated web SDK configs into the client scripts [ ] Add CDN references for Bootstrap 5.0.0-beta1 CSS, Fabric.js 4.5.0, html2canvas 1.3.3, SweetAlert2 11, and both Firebase SDK variants (compat 8.6.1 and modular 10.12.2) [ ] Create stylesheet and script folders for page-specific CSS and ES modules/classic scripts

Phase 2 — Core features [ ] Build the registration flow using Firebase Auth createUserWithEmailAndPassword, then mirror {email, password} into Realtime Database under crex/users/{username} and create a Storage folder stub under Users/{username}/ [ ] Build the login flow to query the username from Realtime Database, call signInWithEmailAndPassword, persist the username to localStorage, and add logout handlers that clear localStorage across all pages [ ] Build the design tool UI with a Bootstrap card layout: a left logo grid fed by Firestore images and onam collections, a center Fabric.js canvas layered on product mockups, and a right-side control panel for background color changes, object deletion, and Add-to-Cart [ ] Implement the Add-to-Cart capture: use html2canvas to snapshot the mockup container, convert to blob, and upload preview images to three Storage paths (CartFolder/{Product}/, CartFolder/cart/, and Users/{username}/), then redirect to the cart page [ ] Build the cart page to aggregate items from CartFolder/cart/, infer product types by probing sibling Storage folders, and fetch unit prices from Realtime Database crex/product/{productType} for display and quantity controls

Phase 3 — Integrations & polish [ ] Implement checkout: generate an order_ + timestamp ID, write {username, orderItems, quantity, orderDate} to Realtime Database orders/{orderId}, delete the cart Storage objects, and redirect to the feedback page [ ] Build the feedback form to push {rating, comment, ISO timestamp} nodes under Realtime Database crex/feedback/{username} [ ] Build the My Projects view to list saved designs from the Users/{username} Storage folder [ ] Implement the optional vendor catalog demo as an in-memory Express service on port 3000 with CORS, exposing REST endpoints for vendors and their t-shirts [ ] Apply the visual theme: header gradient linear-gradient(45deg, #B3011C, #E60124) with white text, #tshirt-div white background, logo cards with #ddd borders, and red Add-to-Cart buttons styled with border-radius: 10px and padding: 16px 32px
