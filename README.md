# 🏥 Hospital, E-Commerce & Todos Backend

A foundational data modeling project demonstrating database schema design using Node.js, Express.js, and Mongoose. This repository defines the database architecture for three distinct modules: **Hospital Management**, **E-Commerce**, and **Todos**.

> [!IMPORTANT]
> This repository is currently focused purely on **Data Modeling**. It does not implement controllers, routes, middleware, authentication, or active REST API endpoints. It serves a simple static HTML file at the root, but the primary educational value lies in the Mongoose schema definitions found in the `models/` directory.

## 📌 Project Overview
This project serves as a starting point for building complex backend systems. By studying this repository, you will learn how to structure Mongoose schemas, define data types, and establish relationships between different entities in a NoSQL database.

## 📑 Table of Contents
- [📌 Project Overview](#-project-overview)
- [✨ Features](#-features)
- [📚 Backend Concepts Used in This Project](#-backend-concepts-used-in-this-project)
- [🛠️ Tech Stack](#️-tech-stack)
- [📦 Dependencies](#-dependencies)
- [📂 Project Structure](#-project-structure)
- [🔄 Request / Response Flow](#-request--response-flow)
- [🗄️ Database Documentation](#️-database-documentation)
- [🔗 Database Relationships](#-database-relationships)
- [🔐 Authentication & Authorization](#-authentication--authorization)
- [🛡️ Security](#️-security)
- [🌱 Environment Variables](#-environment-variables)
- [🧹 .gitignore Explanation](#-gitignore-explanation)
- [💻 Prerequisites](#-prerequisites)
- [🚀 Installation](#-installation)
- [▶️ How to Run the Project](#️-how-to-run-the-project)
- [📡 API Documentation](#-api-documentation)
- [🧪 Postman Testing Guide](#-postman-testing-guide)
- [🧠 Important Code Concepts](#-important-code-concepts)
- [❌ Error Handling](#-error-handling)
- [🐛 Troubleshooting](#-troubleshooting)
- [📚 Learning Roadmap](#-learning-roadmap)
- [🎯 Interview Questions](#-interview-questions)
- [🚀 Future Improvements](#-future-improvements)
- [☁️ Deployment](#️-deployment)
- [📋 Quick Reference](#-quick-reference)

## ✨ Features
This project currently implements Database Schema Definitions for three isolated domains:
- **🏥 Hospital Management**: Models for Hospitals, Doctors, Patients, and Medical Records.
- **🛒 E-Commerce**: Models for Users, Categories, Products, and Orders.
- **✅ Todos**: Models for Users, Todos, and Sub-Todos.

*Note: Features like Authentication, Search, Pagination, active CRUD operations, or Route Handlers are not currently implemented.*

## 📚 Backend Concepts Used in This Project
### What is a Schema?
A schema represents the structure of a particular document within a NoSQL database. It dictates the expected properties, data types, default values, and constraints (like `required` or `unique`) for the data.

### What is an ODM?
An Object Data Modeling (ODM) library (like Mongoose) manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB.

## 🛠️ Tech Stack
| Technology | Purpose | Where Used |
| :--- | :--- | :--- |
| **Node.js** | Runtime | Backend environment execution |
| **Express.js** | Web framework | Serving the static root page (`index.js`) |
| **Mongoose** | ODM | Schema definitions and constraints (`models/`) |

## 📦 Dependencies
### Production Dependencies
| Package | Purpose |
| :--- | :--- |
| `express` | Minimalist web framework used here for serving a static page. |
| `mongoose` | Elegant MongoDB object modeling providing a straight-forward, schema-based solution to model application data. |

*(There are no development dependencies currently configured in `package.json`)*

## 📂 Project Structure
```text
Hospital-Ecommerce-and-Todos-Backend/
│
├── models/                     → Contains all Mongoose schema definitions
│   ├── ecommerce/
│   │   ├── category.models.js
│   │   ├── order.models.js
│   │   ├── product.models.js
│   │   └── user.models.js
│   │
│   ├── hospital-management/
│   │   ├── doctor.models.js
│   │   ├── hospital.models.js
│   │   ├── medical_record.models.js
│   │   └── patient.models.js
│   │
│   └── todos/
│       ├── sub_todo.models.js
│       ├── todo.models.js
│       └── user.models.js
│
├── pages/                      → Contains static HTML pages
│   └── index.html
├── static/                     → Contains static assets
│   └── style.css
├── .gitignore                  → Specifies intentionally untracked files to ignore
├── index.js                    → Entry point serving the static HTML file
├── package-lock.json           → Automatically generated dependency tree
└── package.json                → Project metadata and scripts
```

## 🔄 Request / Response Flow
Because this repository focuses on data modeling, there is no active dynamic REST API request flow. The current architecture simply serves a static file:
```text
Frontend / Browser
       │
       ▼ HTTP GET /
       │
    Express.js Router
       │
       ▼ res.sendFile()
       │
    index.html (Response)
```

## 🗄️ Database Documentation

The database layer defines entities using Mongoose. Here is an overview of the schemas:

### 🛒 E-Commerce Module
| Model Name | Purpose | Important Fields | Relationships |
| :--- | :--- | :--- | :--- |
| **User** | Platform users/customers | `username`, `email`, `password` | None directly |
| **Category** | Product categorization | `name` | None directly |
| **Product** | Items available for sale | `name`, `price`, `stock`, `category` | Ref: `Category`, `User` (owner) |
| **Order** | User purchases | `orderPrice`, `address`, `status`, `orderItems` | Ref: `User` (customer), `Product` |

### 🏥 Hospital Management Module
| Model Name | Purpose | Important Fields | Relationships |
| :--- | :--- | :--- | :--- |
| **Hospital** | Healthcare facilities | `name`, `addressLine1`, `city`, `pincode` | None directly |
| **Doctor** | Medical professionals | `name`, `salary`, `qualification`, `experienceInYears` | Ref: `Hospital` (worksInHospitals) |
| **Patient** | Admitted individuals | `name`, `diagnosedWith`, `age`, `bloodGroup`, `gender` | Ref: `Hospital` (admittedIn) |
| **MedicalRecord**| History (Placeholder) | `timestamps` | None currently defined |

### ✅ Todos Module
| Model Name | Purpose | Important Fields | Relationships |
| :--- | :--- | :--- | :--- |
| **User** | App users | `username`, `email`, `password` | None directly |
| **Todo** | Main tasks | `content`, `complete` | Ref: `User` (createdBy), `SubTodo` |
| **SubTodo** | Sub-tasks | `content`, `complete` | Ref: `User` (createdBy) |

## 🔗 Database Relationships

Mongoose uses `ObjectId` and `ref` to establish relationships between schemas.

**E-Commerce Data Flow:**
```text
User (Customer) ──> Order ──> Product
User (Owner) ──> Product ──> Category
```

**Hospital Data Flow:**
```text
Hospital <── Doctor (Works In)
Hospital <── Patient (Admitted In)
```

**Todos Data Flow:**
```text
User ──> Todo ──> SubTodo
User ──> SubTodo
```

## 🔐 Authentication & Authorization
This project currently does not implement this feature.

## 🛡️ Security
This project currently does not implement active security middleware (like Helmet, CORS, or Rate Limiting).
**Security Best Practices (Future Reference):**
- Never commit `.env` or hardcode passwords.
- Hash passwords using libraries like `bcrypt` before saving to a database.
- Use JWT or secure sessions for authorization.

## 🌱 Environment Variables
This project currently does not use environment variables or a `.env` file. The server port is statically defined as `3010` in `index.js`.

## 🧹 .gitignore Explanation
The `.gitignore` file contains:
- `node_modules`: These are ignored because they take up significant disk space and can easily be regenerated on any machine by running `npm install`.

## 💻 Prerequisites
To run this project locally, you will need:
- [Node.js](https://nodejs.org/) (Verify installation: `node --version`)
- npm (Verify installation: `npm --version`)
- Git (Verify installation: `git --version`)

## 🚀 Installation

**Step 1 — Clone the repository**
```bash
git clone https://github.com/Mohammad-Asfin/Hospital-Ecommerce-and-Todos-Backend.git
```

**Step 2 — Enter the directory**
```bash
cd "hospital,  ecommerce and todos backend"
```

**Step 3 — Install dependencies**
```bash
npm install
```

## ▶️ How to Run the Project

**Start the Server**
Run the script defined in `package.json`:
```bash
npm start
```

**Verify the Server**
Open your browser and navigate to:
`http://localhost:3010`
You should see the static HTML page rendered.

## 📡 API Documentation
This project currently does not implement active REST API endpoints.

## 🧪 Postman Testing Guide
Since there are no active API routes configured in the Express app, Postman testing is not applicable at this stage.

## 🧠 Important Code Concepts
### Models & Schemas
- **What is it?** A blueprint for your data structure.
- **Why is it used?** To ensure consistency, validation, and to easily query the MongoDB database.
- **Where is it used?** Inside the `models/` folder, utilizing `new mongoose.Schema()`.
- **How does it work?** Code defines fields and types, which Mongoose translates into validation rules before saving documents to MongoDB.

## ❌ Error Handling
This project currently does not implement centralized error handling or API-level error responses.

## 🐛 Troubleshooting

| Problem | Possible Cause | Solution |
| :--- | :--- | :--- |
| **Server doesn't start** | Missing dependencies | Run `npm install` |
| **Port already in use** | Port 3010 is occupied | Open `index.js` and change `const port = 3010;` to another number |

## 📚 Learning Roadmap
If you are learning from this project, follow this order:
1. **Understand package.json**: Look at the dependencies and scripts.
2. **Understand the entry point**: Read `index.js` to see how a basic Express server starts.
3. **Understand Mongoose schemas**: Pick one module (e.g., `todos/todo.models.js`) and study how fields are defined.
4. **Understand Relationships**: Look at how `type: mongoose.Schema.Types.ObjectId` and `ref` are used to link documents together (e.g., in `order.models.js`).

## 🎯 Interview Questions
**Beginner**
- What is the purpose of `package.json`?
- What does `express.static` do in `index.js`?

**Intermediate**
- How do you create a relationship between two collections in Mongoose?
- Why do we define schemas in a NoSQL database like MongoDB?

**Advanced**
- If you were to expand this architecture, how would you structure the Routes and Controllers?
- How would you handle indexing for fields like `email` or `username` to optimize query performance?

## 🚀 Future Improvements
**Possible future enhancements:**
- Implement Controllers and Routes to expose full CRUD APIs.
- Connect to an active MongoDB Database instance.
- Add robust Authentication (JWT).
- Add Request Validation.
- Configure Environment Variables (`.env`).
- Implement comprehensive Error Handling.
- Add Automated Testing.

## ☁️ Deployment
This project is currently not configured for deployment.
*Deployment Considerations:*
To deploy this as a full backend in the future, you would need to set up a MongoDB cluster (like MongoDB Atlas), use environment variables for connection strings, and deploy the Node.js app to a service like Render, Heroku, or AWS.

https://stackblitz.com/edit/stackblitz-starters-mg2tiy

## 📋 Quick Reference
```text
git clone URL ↓ npm install ↓ npm start ↓ Open http://localhost:3010
```

---
*Created by Mohammad Asfin*
