# 🌱 Smart Irrigation Advisory System

> **An intelligent, data-driven irrigation advisory platform that helps farmers make better watering decisions using soil moisture, crop-stage requirements, and weather forecasts.**

[![React](https://img.shields.io/badge/Frontend-React.js-61DAFB?logo=react\&logoColor=white)](https://react.dev/)
[![Firebase](https://img.shields.io/badge/Backend-Firebase-FFCA28?logo=firebase\&logoColor=black)](https://firebase.google.com/)
[![Python](https://img.shields.io/badge/Backend-Python-3776AB?logo=python\&logoColor=white)](https://www.python.org/)
[![Firestore](https://img.shields.io/badge/Database-Firestore-FFCA28?logo=firebase\&logoColor=black)](https://firebase.google.com/docs/firestore)
[![Tailwind CSS](https://img.shields.io/badge/UI-Tailwind_CSS-06B6D4?logo=tailwindcss\&logoColor=white)](https://tailwindcss.com/)

---

## 📌 Project Overview

The **Smart Irrigation Advisory System** is a web-based agricultural technology solution designed to support farmers in making informed irrigation decisions.

The system combines:

* 🌱 Soil moisture readings
* 🌾 Crop type and growth stage
* 🌧️ Weather and rainfall forecast
* 💧 Crop water requirements
* 📊 Irrigation history and usage analytics

Based on these inputs, the system generates a simple recommendation such as **Irrigate Now** or **Wait**, along with the recommended irrigation amount and reason.

The goal is to reduce unnecessary water usage, avoid under-irrigation, and support more sustainable agricultural practices.

---

## 🎯 Problem Statement

Farmers may face difficulties deciding **when to irrigate and how much water to use**.

### Major challenges

* 💧 **Over-irrigation** can waste water and leach nutrients.
* 🌱 **Under-irrigation** can cause crop stress and affect productivity.
* 🌦️ Weather conditions can change irrigation requirements.
* 📋 Soil moisture, crop stage, and weather information may be handled separately.
* 📊 Farmers may not have a simple way to track irrigation usage.

### Our Approach

The system brings these factors together into a single advisory workflow.

**Soil Moisture + Crop Stage + Weather Forecast → Recommendation**

---

## 💡 Key Features

### 👨‍🌾 Farmer Module

* Farmer registration and login
* Create and manage fields
* Add crop and growth-stage information
* Enter soil-moisture readings
* View irrigation recommendations
* Record irrigation actions
* View irrigation history
* Monitor water-usage trends

### 👨‍💼 Admin Module

* Secure admin authentication
* Manage crop-stage rules
* Configure water requirements
* Configure moisture thresholds
* Maintain crop-related advisory information

### 🧠 Recommendation Engine

The recommendation engine evaluates:

* Current soil moisture
* Crop growth stage
* Required water per day
* Moisture threshold
* Rain probability
* Expected rainfall

It generates:

**Recommendation + Water Amount + Reason**

---

## 🔄 System Workflow

```text
        Farmer Login
             │
             ▼
       Select / Create Field
             │
             ▼
     Enter Soil Moisture
             │
             ▼
   Retrieve Crop-Stage Data
             │
             ▼
    Retrieve Weather Forecast
             │
             ▼
     Recommendation Engine
             │
       ┌─────┴─────┐
       ▼           ▼
   IRRIGATE       WAIT
       │           │
       └─────┬─────┘
             ▼
      Record Action
             │
             ▼
      Update Dashboard
```

---

## ⚙️ Technology Stack

| Layer          | Technologies                           |
| -------------- | -------------------------------------- |
| Frontend       | React.js, Vite                         |
| UI             | Tailwind CSS                           |
| Backend        | Firebase Cloud Functions, Python Flask |
| Database       | Firebase Firestore                     |
| Authentication | Firebase Authentication                |
| Charts         | Recharts                               |
| Weather API    | OpenWeatherMap                         |
| Deployment     | Firebase Hosting                       |
| Development    | JavaScript, Python                     |

The project uses Firebase Cloud Functions for server-side recommendation and weather logic rather than relying only on client-side operations.

---

## 🏗️ System Architecture

```text
┌─────────────────────────────┐
│        React Frontend       │
│      Vite + Tailwind CSS    │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│    Firebase Authentication  │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Firebase Backend       │
│       Cloud Functions       │
└───────┬─────────┬───────────┘
        │         │
        ▼         ▼
┌────────────┐ ┌──────────────┐
│ Firestore  │ │ OpenWeather  │
│  Database  │ │     API      │
└────────────┘ └──────────────┘
        │
        ▼
┌─────────────────────────────┐
│ Recommendation & Analytics  │
└─────────────────────────────┘
```

---

## 🧠 Recommendation Logic

The system uses a rule-based recommendation engine.

### Rule 1 — Moisture Above Threshold

If:

```text
Current Moisture >= Required Threshold
```

Then:

```text
Recommendation = WAIT
Irrigation Amount = 0 mm
```

### Rule 2 — Low Moisture + Sufficient Rain

If:

```text
Current Moisture < Threshold
AND
Rain Probability is sufficient
AND
Expected Rainfall covers the required amount
```

Then:

```text
Recommendation = WAIT
```

### Rule 3 — Low Moisture + Insufficient Rain

If:

```text
Current Moisture < Threshold
AND
Rainfall is insufficient
```

Then:

```text
Recommendation = IRRIGATE
```

The project documentation defines the engine as a unit-testable Cloud Function and calculates irrigation amount from the moisture deficit and daily crop requirement.

---

## 🗄️ Database Structure

The application uses **Firebase Firestore**.

### Main Collections

```text
users/{uid}
│
├── name
├── email
├── role
└── createdAt

fields/{fieldId}
│
├── userId
├── name
├── cropType
├── areaAcres
└── currentGrowthStage

cropStageRules/{ruleId}
│
├── cropType
├── growthStage
├── waterRequirementMmPerDay
└── moistureThresholdPercent
```

### Field Subcollections

```text
fields/{fieldId}/moistureReadings
fields/{fieldId}/weatherData
fields/{fieldId}/irrigationLogs
```

This structure keeps field history scoped to the individual field and supports irrigation tracking and analytics.

---

## 🔐 Authentication & Security

Security is implemented using:

* Firebase Authentication
* Email/password authentication
* Firebase custom role claims
* Firestore Security Rules
* Server-side role validation
* Cloud Function input validation

### User Roles

**Farmer**

* Manages own fields
* Records moisture readings
* Views recommendations
* Records irrigation actions
* Views personal dashboard

**Admin**

* Manages crop-stage rules
* Updates crop water requirements
* Maintains moisture thresholds

The project specifies that roles are enforced through Firebase custom claims, Firestore Security Rules, and Cloud Functions rather than relying only on the frontend.

---

## 📊 Dashboard & Analytics

The system provides:

* 💧 Water-usage trends
* 📈 Irrigation history
* 📋 Recommendation history
* 📊 Recommendation-vs-actual adherence
* 🌱 Field-level information

The analytics functions aggregate irrigation logs into chart-ready data for the dashboard.

---

## 🖥️ Application Screens

The application includes:

1. 🔐 Login / Registration
2. 👨‍🌾 Farmer Dashboard
3. 🌱 Field Details
4. 💧 Irrigation Recommendation
5. 📊 Water Usage Dashboard
6. 🌾 Crop Details
7. 📋 Irrigation History
8. 👨‍💼 Admin Crop Management

The documented frontend flow is designed around large, simple interactions and plain-language recommendations for farmers.

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
```

### 2. Navigate to the Project

```bash
cd smart-irrigation-advisory
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Configure Firebase

Create/configure your Firebase project and add the required Firebase configuration.

### 5. Configure Environment Variables

Add the required environment variables for:

```text
Firebase
OpenWeatherMap API
Backend configuration
```

### 6. Start the Development Server

```bash
npm run dev
```

### 7. Build for Production

```bash
npm run build
```

---

## 🌐 Live Demo

🔗 **Live Application:**
https://smart-irrigation-advisory.vercel.app/simulator

> Replace the URL above if your latest deployed application uses a different deployment address.

---

## 📁 Project Structure

```text
smart-irrigation-advisory/
│
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   └── ...
│
├── functions/
│   ├── ...
│   └── ...
│
├── public/
│
├── firebase.json
├── firestore.rules
├── package.json
├── README.md
└── ...
```

---

## 🔮 Future Scope

The project can be further enhanced with:

* 🎙️ Voice assistance for farmers
* 🌐 Regional-language support
* 🤖 AI-powered irrigation recommendations
* 📱 Dedicated mobile application
* 📡 Integration with real-time agricultural sensors
* 🚜 Automated irrigation-system integration

Voice assistance, multilingual support, AI-powered recommendations, and mobile integration are specifically identified as future improvements in the project presentation.

---

## 🏆 Project Highlights

### What this project demonstrates

* Full-stack web application development
* React-based frontend development
* Firebase backend integration
* Python backend logic
* REST/API integration
* Authentication and authorization
* Firestore database design
* Rule-based decision making
* Data visualization
* Cloud deployment
* Input validation and security

---

## 👥 Project

**Project:** Smart Irrigation Advisory System
**Team:** Quantum Coders
**Event:** Codegnan Hackathon
**Domain:** Agriculture & Technology

---

## 📚 Learning Outcomes

Through this project, we gained practical experience in:

* React.js and component-based development
* Firebase Authentication and Firestore
* Cloud Functions
* Python backend development
* API integration
* Database design
* Role-based access control
* Data visualization
* Deployment
* Building a real-world agriculture-focused application

---

## 📌 Conclusion

The **Smart Irrigation Advisory System** demonstrates how software, weather information, soil-moisture data, and crop-stage requirements can be combined to provide clear irrigation guidance.

The project focuses on helping farmers make informed irrigation decisions while supporting efficient water usage and sustainable agriculture.

---

## 🙏 Acknowledgement

**Developed as part of the Codegnan Hackathon by Team Quantum Coders.**

---

### ⭐ If you find this project useful, consider giving the repository a Star!

**Smart Water. Healthy Crops. Sustainable Future. 🌱💧**

