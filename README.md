# Hotel Room Booking Management System

A Java-based web application developed for **Advance Java Technology (01CE0308)**. The system allows guests to browse rooms, check availability, make bookings, view their bookings, and cancel eligible bookings. Administrators can manage rooms and bookings and view dashboard statistics.

## Project Information

- **Project:** Hotel Room Booking Management System
- **Course:** Advance Java Technology (01CE0308)
- **Department:** CSE - CS, Faculty of Engineering & Technology

### Project Members

1. Netla Manjunath Reddy
2. Raghavapurapu Nagaraju Naidu
3. Panditi Srinivasa Reddy

## Technologies Used

| Technology | Purpose |
|---|---|
| Java 11 | Application programming language |
| JSP | Dynamic web pages / presentation layer |
| HTML and CSS | Page structure and styling |
| JavaScript | Client-side form validation |
| Java Servlets | Handle browser requests and application flow |
| JDBC | Connect Java code to the database |
| MySQL | Relational database |
| MySQL Connector/J 8.0.33 | JDBC driver |
| JSTL 1.2 | JSP tag library |
| Apache Tomcat 9 | Runs the web application |
| Apache Maven | Dependency management and WAR packaging |

## Main Features

### Guest Features

- Register a new guest account.
- Log in and log out.
- Browse active hotel rooms.
- Search for rooms using check-in date, check-out date, and guest count.
- View room type, capacity, and price per night.
- Calculate the booking amount based on the length of stay.
- View personal bookings.
- Cancel eligible confirmed bookings.

### Administrator Features

- Access protected admin pages.
- View dashboard statistics, including total rooms, total guests, active bookings, today's check-ins, and recorded paid revenue.
- Add, update, and delete room records, subject to database constraints.
- View and manage bookings.
- Update booking status, including check-in and check-out.
- View booking and payment information.

### Booking and Payment Records

- Checks room status, guest capacity, and date overlap before showing available rooms.
- Validates booking dates and guest count.
- Uses JDBC prepared statements for database operations.
- Saves booking and payment information as part of the booking transaction.
- Records payment method and payment status.

**Note:** The application records payment details and status. A real third-party online payment gateway is not included in the documented implementation.

## Application Architecture

The application follows a layered structure:

1. **Presentation layer:** JSP pages display information and collect user input.
2. **Controller layer:** Servlets receive requests, validate input, and coordinate application actions.
3. **Data access layer:** DAO classes execute database operations using JDBC.
4. **Model layer:** Java model classes represent users, rooms, room types, and bookings.
5. **Database layer:** MySQL stores application records.

### Important Classes

| Class / Component | Responsibility |
|---|---|
| `RegisterServlet` | Handles guest registration |
| `LoginServlet` | Handles user authentication |
| `LogoutServlet` | Ends the user's session |
| `RoomSearchServlet` | Displays rooms and searches availability |
| `BookingServlet` | Handles booking requests |
| `MyBookingsServlet` | Displays a guest's bookings |
| `UserDAO` | User database operations |
| `RoomDAO` | Room and room-type database operations |
| `BookingDAO` | Booking, payment, and dashboard data operations |
| `DBConnection` | Creates JDBC database connections |
| `PasswordUtil` | Hashes passwords using SHA-256 |
| `AuthFilter` | Restricts selected pages to logged-in users |
| `AdminFilter` | Restricts admin URLs to administrator accounts |

## Database

The application code uses these main database tables:

- `users` — guest and administrator account information.
- `room_types` — room type, description, price per night, and capacity.
- `rooms` — room number, room type, floor, and status.
- `bookings` — guest, room, stay dates, guest count, amount, and booking status.
- `payments` — booking payment amount, method, and status.

The database connection settings are loaded from:

`src/main/resources/db.properties`

Configure the database URL, username, and password for your local MySQL installation. Do not commit real database passwords or other secrets to a public repository.

The database and required tables must be created before running the application. Use the SQL setup script supplied with the project, if included. The project report documents the table names and application queries but does not include a complete database creation script.

## Requirements

Install and configure:

- JDK 11
- Apache Maven
- Apache Tomcat 9
- MySQL Server
- A browser

## Configuration and Running

1. Clone or download this repository.
2. Create the MySQL database and required tables.
3. Open `src/main/resources/db.properties`.
4. Set the correct database URL, username, and password for your MySQL server.
5. Open a terminal in the project directory.
6. Build the project:

   ```bash
   mvn clean package
   ```

7. After a successful build, locate the generated WAR file:

   ```text
   target/hotel-booking.war
   ```

8. Copy the WAR file into the `webapps` folder of your Tomcat 9 installation.
9. Start Tomcat.
10. Open the application in your browser:

   ```text
   http://localhost:8080/hotel-booking/
   ```

The context path may differ if the WAR file is renamed during deployment.

## Security and Validation

The implementation includes:

- Server-side validation for registration, login, room search, and booking inputs.
- SHA-256 password hashing through `PasswordUtil`.
- JDBC `PreparedStatement` for parameterized SQL operations.
- Session-based authentication.
- Authentication and administrator filters for protected routes.
- A 30-minute session timeout.
- HTTP-only session cookies.
- Booking transaction handling and room-row locking to reduce conflicting bookings.

For production use, password storage should be upgraded to a password-hashing algorithm designed for passwords, such as Argon2id, bcrypt, or PBKDF2, with unique salts.

## Booking Calculation

The booking amount is calculated using:

```text
Total Amount = Price Per Night × Number of Nights
```

For example, if a room costs ₹2,800 per night and the stay is 2 nights:

```text
₹2,800 × 2 = ₹5,600
```

## Future Enhancements

- Integrate a secure third-party payment gateway.
- Add email or SMS booking notifications.
- Add guest reviews and ratings.
- Provide downloadable booking invoices.
- Add reporting and analytics features.
- Develop a mobile-friendly application.

## Academic Use

This project was developed as part of the **Advance Java Technology (01CE0308)** coursework at the Department of CSE - CS, Faculty of Engineering & Technology.

---

**Hotel Room Booking Management System**
