# GreenLegacy - Full Website (Razorpay + Netlify Functions + Firebase)

## Overview
This project is a full demo-ready website for **GreenLegacy** with:
- Frontend: static site (single-page) using HTML/CSS/JS
- Payment integration: **Razorpay** using serverless functions (for Netlify)
- Serverless functions: create order & verify payment (Node.js for Netlify Functions)
- Advanced Tree Tracker: uses **Firebase Firestore** (server writes on verified payment)

**Important:** You must provide your own credentials and deploy functions to Netlify (or other Node server).

## Quick features
- Donor fills form → frontend requests `/.netlify/functions/createOrder` → server creates Razorpay order → Razorpay Checkout opens → on success frontend calls `/.netlify/functions/verifyPayment` → server verifies signature and writes tree record to Firestore using Firebase Admin SDK → donor receives certificate & Tree ID.
- Tree tracking reads data from Firestore (public read assumed; adjust rules).

## Project structure
```
greenlegacy_full/
├─ frontend/
│  └─ index.html
│  └─ assets/ (images)
│  └─ css/styles.css
│  └─ js/app.js
├─ netlify/
│  └─ functions/
│     ├─ createOrder.js
│     └─ verifyPayment.js
├─ package.json
└─ README.md
```

## Required configuration (before deploying)
1. **Razorpay**: Create an account and get `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`.
2. **Netlify**: Deploy this folder and set environment variables in Netlify:
   - RAZORPAY_KEY_ID
   - RAZORPAY_KEY_SECRET
   - FIREBASE_SERVICE_ACCOUNT (JSON string)
   - FIREBASE_PROJECT_ID
3. **Firebase**:
   - Create a Firebase project.
   - Create a service account JSON (Admin SDK) and copy the JSON content into `FIREBASE_SERVICE_ACCOUNT` env var (stringified).
   - Create a Firestore database and appropriate security rules.

## Local testing (without deploying serverless functions)
- You can run functions locally using Netlify CLI (`netlify dev`) after installing dependencies.

## Notes
- This project is configured for Netlify Functions (Node.js). You can adapt server files to Express or other platforms as needed.
- For production, ensure you secure your Firebase rules and verify Razorpay payments server-side.

