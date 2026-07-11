# 🖥️ CraveCart Server (Backend API)

The backend server is a RESTful API service built on **Node.js** and **Express**. It handles data persistence using **MongoDB** (via Mongoose ODM), implements JSON Web Token (JWT) session security via HTTP-only cookies, and provides routes for user registration, authenticating credentials, profile data, cart management, and order operations.

---

## 🛠️ Tech Stack & Key Libraries

- **Runtime**: [Node.js](https://nodejs.org/)
- **Web Framework**: [Express](https://expressjs.com/)
- **Database integration**: [Mongoose](https://mongoosejs.com/) (MongoDB Object Document Mapper)
- **Authentication & Encryption**:
  - [JSON Web Token (JWT)](https://jwt.io/) for access sessions.
  - [Bcrypt](https://www.npmjs.com/package/bcrypt) for hashing user passwords securely.
- **Middleware**:
  - `cookie-parser` for handling HTTP-only authorization cookies (`uid`).
  - `cors` configured with credentials capability for frontend connections.
- **Development tools**: `nodemon` for hot-reloads during server editing.

---

## 📂 Folder Structure

```
server/
├── connection/
│   └── mongoConnection.js # Mongoose connection routine configuration
├── controller/
│   ├── cartController.js  # Moves cart items to verified orders
│   ├── category.js        # Controller requesting details from external endpoints
│   ├── meal.js            # Category lists, autocomplete search, and pagination controllers
│   └── user.js            # User accounts creation, sign in, and cart state mutations
├── middleware/
│   └── auth.js            # Session security validation filter (JWT verification)
├── model/
│   └── user.js            # Mongo schemas for Users, including embedded Cart and Order models
├── routes/
│   ├── cart.js            # Cart subroutes (/api/cart)
│   ├── category.js        # Category detail subroutes (/api/category)
│   ├── meal.js            # Meal listings & search subroutes (/api/meals)
│   └── user.js            # User sessions & profile mutations (/api/users)
├── .env.dev               # Dev environment defaults template
├── index.js               # Application Entrypoint (Express setup & middleware stack)
└── package.json
```

---

## 🔧 Environment Variables

The server requires several environment variables for security keys and database connections. Define these within a `.env` file in the root of the `server` directory:

```env
PORT=8000
MONGO_USER=your_mongodb_username
MONGO_PASS=your_mongodb_password
JSONKEY=your_secure_jwt_passphrase
```

---

## 🚦 REST API Endpoints

### 🔐 Authentication & User Management

| Method | Endpoint | Description | Middleware |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/users/createuser` | Register a new user account | Public |
| `POST` | `/api/users/loginuser` | Login, verify credentials, and issue cookie token (`uid`) | Public |
| `GET` | `/authuser` | Verifies active session token state | `auth` |
| `POST` | `/api/users/forgetpass` | Reset passwords (stub action) | Public |

### 🛒 Shopping Cart & Orders

| Method | Endpoint | Description | Middleware |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/users/fetchCart` | Retrieves current items from the user's cart | Public |
| `POST` | `/api/users/addToCart` | Appends a meal item to the user's cart | Public |
| `POST` | `/api/users/updateQuantity` | Updates the selected quantity for a cart item | Public |
| `POST` | `/api/cart/cartToOrder` | Convers all current cart contents into a new Order | Public |
| `POST` | `/api/users/orders` | Fetches history of completed orders for user | Public |

### 🍽️ Meal & Category Lookups

| Method | Endpoint | Description | Middleware |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/meals/category` | Fetches the full list of meal categories | Public |
| `GET` | `/api/meals/autosuggestion`| Autocomplete query for search text | Public |
| `GET` | `/api/meals/mealpagination` | Retrieve paginated list of meals | Public |
| `GET` | `/api/meals/getMealById/:id`| Retrieve meal details from MealDB | Public |
| `GET` | `/api/category/:id` | Get all meals inside a specific category | Public |

---

## 💻 Script Reference

From the `server/` subdirectory, you can execute:

- **Run Dev Server**:
  ```bash
  npm start
  ```
  Launches the server with `nodemon` listening on your defined `PORT` (or fallback port `8001`).
