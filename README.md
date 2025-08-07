
# 8.3 Travel Tracker

## Overview

This is a Node.js web application built with Express and EJS that allows multiple users to track the countries they have visited. It utilizes a PostgreSQL database to manage user data and the list of visited countries.

## Features

- **Multi-user Support**: The application supports multiple users, each with their own unique travel log.
- **Country Tracking**: Users can add countries they have visited to their personal list.
- **Database Integration**: All user and country data is stored persistently in a PostgreSQL database.
- **User-specific Experience**: The UI adapts to the currently logged-in user, showing their visited countries and a unique color.

## Technologies Used

- **Backend**: Node.js, Express.js
- **Templating**: EJS (Embedded JavaScript)
- **Database**: PostgreSQL
- **Database Driver**: `pg`

### Dependencies

- `express`: Web framework for Node.js.
- `body-parser`: Middleware to parse incoming request bodies.
- `ejs`: A simple templating language.
- `pg`: A non-blocking PostgreSQL client for Node.js.

## Database Setup

The database schema is defined in the `queries.sql` file. You will need to set up a PostgreSQL database named `world` with the following tables:

- `users`: Stores user information (`id`, `name`, `color`).
- `visited_countries`: Stores a record of a country visited by a specific user (`country_code`, `user_id`).

### SQL Setup

```sql
DROP TABLE IF EXISTS visited_countries, users;

CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  name VARCHAR(15) UNIQUE NOT NULL,
  color VARCHAR(15)
);

CREATE TABLE visited_countries(
  id SERIAL PRIMARY KEY,
  country_code CHAR(2) NOT NULL,
  user_id INTEGER REFERENCES users(id)
);

INSERT INTO users (name, color)
VALUES ('Angela', 'teal'), ('Jack', 'powderblue');

INSERT INTO visited_countries (country_code, user_id)
VALUES ('FR', 1), ('GB', 1), ('CA', 2), ('MX', 2);
````

## Getting Started

1. Clone the repository.

2. Install dependencies:

   ```bash
   npm install
   ```

3. Set up the PostgreSQL database using the commands provided above.

4. Ensure your database connection settings in `index.js` are correct.

5. Run the application:

   ```bash
   node index.js
   ```

6. Open your browser and navigate to:
   `http://localhost:3000`

## Endpoints

* `GET /`: Renders the main page, displaying the map with visited countries for the current user.
* `POST /add`: Adds a new country to the current user's visited list.
* `POST /user`: Handles switching between users or adding a new user.
* `POST /new`: (To be completed) This endpoint is intended to handle the creation of a new user.

```


