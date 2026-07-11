# 💻 CraveCart Client (Frontend)

The frontend client of the CraveCart application is built with **React**, **Vite**, **Tailwind CSS**, and **Redux Toolkit**. It provides an interactive, stateful, and responsive user interface for browsing recipes/meals, managing a cart, executing checkout, and maintaining user profiles.

---

## 🛠️ Tech Stack & Key Libraries

- **Framework**: [React](https://react.dev/) + [Vite](https://vite.dev/) (with Fast Refresh and ES modules)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) & [SASS](https://sass-lang.com/) for hybrid stylesheet organization
- **State Management**: [Redux Toolkit](https://redux-toolkit.js.org/) (Slices for Cart, Order, and Categories)
- **Routing**: [React Router DOM v6](https://reactrouter.com/) (Browser router with nested layout routes)
- **Form Handling**: [React Hook Form](https://react-hook-form.com/)
- **HTTP Client**: [Axios](https://axios-http.com/) (Custom baseURL configuration and cookie credentials)
- **Notifications**: [React Toastify](https://fkhadra.github.io/react-toastify/)

---

## 📂 Folder Structure

```
client/
├── Redux/
│   ├── features/
│   │   ├── cart/         # Redux slice for shopping cart state
│   │   ├── category/     # Redux slice for handling meal categories
│   │   └── order/        # Redux slice for managing placed orders
│   └── store/
│       └── store.js      # Root store definition and middleware registration
├── src/
│   ├── api/
│   │   ├── apiConfig.js  # Main class for client requests (Axios & Fetch)
│   │   └── axiosConfig.js# Axios instance configuration (baseURL + credentials)
│   ├── components/       # UI Components & Page Containers
│   │   ├── authProvider/ # Session context listener (AuthProvider.jsx)
│   │   ├── cart/         # Cart drawer or cart pages
│   │   ├── catergory/    # Category grid & Meal details
│   │   ├── loginPage/    # Sign-in UI
│   │   ├── signup/       # Sign-up UI
│   │   ├── profile/      # UserProfile UI
│   │   ├── order/        # Order lists and summary components
│   │   └── NavBar.jsx    # Sticky navigation bar with search features
│   ├── App.jsx           # Home / Hero section
│   ├── Route.jsx         # App router layout configuration
│   ├── main.jsx          # Mount target
│   └── index.css         # CSS Entrypoint (Tailwind directives)
├── tailwind.config.js    # Tailwind layout customizations
└── package.json
```

---

## 🔧 Environment Configuration

The client requires an environment variable to establish communication with the backend REST API server.

Create a `.env` file in the root of the `client` directory:
```env
VITE_APP_BACKEND_URL=http://localhost:8000
```

---

## 🚦 Navigation Routes

All core paths are configured inside [Route.jsx](./src/Route.jsx):

| Route Path | Component | Description | Access Level |
| :--- | :--- | :--- | :--- |
| `/` | `Login` | Sign in page | Public |
| `/signup` | `SignUp` | Account registration | Public |
| `/themeal` | `App` | Home portal page (Hero banner, Category lists) | Protected / User |
| `/themeal/profile` | `UserProfile` | Settings & User Details | Protected / User |
| `/themeal/cart` | `Cart` | Current checkout bag and items overview | Protected / User |
| `/themeal/order` | `Order` | Summary of user orders | Protected / User |
| `/themeal/catergory/:id` | `Catergory` | View all meals under a category | Protected / User |
| `/themeal/catergory/:id/:mealId`| `MealById` | Full detail page of a meal | Protected / User |
| `/themeal/meal/:mealId` | `MealById` | Direct path to full detail of a meal | Protected / User |

---

## 💻 Script Reference

From the `client/` subdirectory, you can execute standard npm scripts:

- **Run Dev Server**:
  ```bash
  npm run dev
  ```
  Runs the local React web app at [http://localhost:5173](http://localhost:5173).

- **Production Build**:
  ```bash
  npm run build
  ```
  Compiles and optimizes source files into static assets ready for hosting in the `dist/` directory.

- **Preview Build locally**:
  ```bash
  npm run preview
  ```
  Hosts the locally generated `dist/` static files to review the production output.

- **Linter execution**:
  ```bash
  npm run lint
  ```
  Checks files for static code standard issues using ESLint.
