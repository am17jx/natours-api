# Natours Project 🏞️

Natours is a comprehensive backend application for a fictional tour company, built with Node.js, Express, and MongoDB. The project provides a complete RESTful API for managing tours, users, and reviews, featuring a robust authentication and authorization system, advanced security features, and much more.

This project is an implementation of the popular Node.js course by Jonas Schmedtmann, applying all the best practices and advanced concepts taught.
![Natours Project Architecture](https://github.com/am17jx/natours-api/blob/master/natours%20project%20global%20architecture.webp?raw=true)

---

## ✨ Key Features

-   **RESTful API:** Clean and logical API for managing tours, users, and reviews.
-   **Authentication & Authorization:** Secure JWT-based authentication with role-based access control (user, guide, lead-guide, admin).
-   **Password Security:** Hashed passwords using `bcryptjs` for secure storage.
-   **Password Reset:** Full password reset functionality via email.
-   **Advanced Security:**
    -   Secure HTTP Headers with `helmet`.
    -   Rate Limiting to protect against brute-force attacks.
    -   Protection against NoSQL Injection and XSS attacks.
-   **Advanced API Querying:**
    -   Easy filtering, sorting, field limiting, and pagination of results.
    -   Geospatial queries to find tours within a certain radius.
-   **Error Handling:** Centralized error handling with distinct responses for development and production environments.
-   **Database Operations:** Efficient use of Mongoose with data validation, middleware, and virtual properties.
-   **Data Seeding Script:** A dedicated script to easily import or delete development data.

---

## 🛠️ Tech Stack

-   **Backend:** Node.js, Express.js
-   **Database:** MongoDB, Mongoose
-   **Authentication:** JSON Web Tokens (jsonwebtoken)
-   **Security:** `helmet`, `express-rate-limit`, `hpp`, `xss-clean`, `express-mongo-sanitize`
-   **Environment Variables:** `dotenv`
-   **Email:** `nodemailer`
-   **Utilities:** `slugify`, `validator`, `bcryptjs`

---

## 🚀 Installation & Setup

Follow these steps to run the project locally:

**1. Clone the repository:**
```bash
git clone [https://github.com/your-username/natours-project.git](https://github.com/your-username/natours-project.git)
cd natours-project
```

**2. Install dependencies:**
```bash
npm install
```

**3. Set up environment variables:**

Create a new file in the root directory named `config.env`. Then, copy the following content into it and fill in your credentials.

```env
NODE_ENV=development
PORT=3000

# DATABASE
DATABASE=mongodb+srv://<USER>:<PASSWORD>@cluster0-omexv.mongodb.net/natours?retryWrites=true
DATABASE_PASSWORD=<YOUR_DATABASE_PASSWORD>

# JWT
JWT_SECRET=my-ultra-secure-and-long-jwt-secret-for-this-project
JWT_EXPIRES_IN=90d
JWT_COOKIE_EXPIRES_IN=90

# EMAIL (using Mailtrap for development)
EMAIL_HOST=smtp.mailtrap.io
EMAIL_PORT=2525
EMAIL_USERNAME=<YOUR_MAILTRAP_USERNAME>
EMAIL_PASSWORD=<YOUR_MAILTRAP_PASSWORD>
```

**4. Import development data:**

You can use the provided script to seed your database with initial data (tours, users, reviews).

```bash
# To import data
node ./dev-data/data/import-dev-data.js --import

# To delete all data
node ./dev-data/data/import-dev-data.js --delete
```

**5. Run the server:**
```bash
# For development with nodemon
npm start

# For production
npm run start:prod
```

The application should now be running on `http://localhost:3000`.

---

## 🗺️ API Endpoints

### Tours API

| Method | Endpoint                    | Description                                  | Access      |
| :----- | :-------------------------- | :------------------------------------------- | :---------- |
| GET    | `/api/v1/tours`             | Get all tours with filtering and sorting     | Public      |
| GET    | `/api/v1/tours/top-5-cheap` | Get the top 5 cheapest tours                 | Public      |
| GET    | `/api/v1/tours/tour-stats`  | Get tour statistics                          | Public      |
| GET    | `/api/v1/tours/:id`         | Get a specific tour by ID                    | Public      |
| POST   | `/api/v1/tours`             | Create a new tour                            | Admin, Lead-Guide |
| PATCH  | `/api/v1/tours/:id`         | Update a specific tour                       | Admin, Lead-Guide |
| DELETE | `/api/v1/tours/:id`         | Delete a specific tour                       | Admin, Lead-Guide |

### Users API

| Method | Endpoint                       | Description                        | Access      |
| :----- | :----------------------------- | :--------------------------------- | :---------- |
| POST   | `/api/v1/users/signup`         | Create a new user                  | Public      |
| POST   | `/api/v1/users/login`          | Log in a user                      | Public      |
| POST   | `/api/v1/users/forgotPassword` | Request a password reset           | Public      |
| PATCH  | `/api/v1/users/resetPassword/:token` | Reset the password             | Public      |
| GET    | `/api/v1/users`                | Get all users                      | Admin       |
| GET    | `/api/v1/users/me`             | Get the current user's data        | Logged-in User |
| PATCH  | `/api/v1/users/updateMe`       | Update the current user's data     | Logged-in User |
| DELETE | `/api/v1/users/deleteMe`       | Deactivate the current user's account| Logged-in User |


### Reviews API

| Method | Endpoint                        | Description                   | Access         |
| :----- | :------------------------------ | :---------------------------- | :------------- |
| GET    | `/api/v1/reviews`               | Get all reviews               | Public         |
| GET    | `/api/v1/tours/:tourId/reviews` | Get all reviews for a specific tour | Public         |
| POST   | `/api/v1/tours/:tourId/reviews` | Create a new review           | User (logged in) |
| PATCH  | `/api/v1/reviews/:id`           | Update a review               | User (owner), Admin |
| DELETE | `/api/v1/reviews/:id`           | Delete a review               | User (owner), Admin |

---
