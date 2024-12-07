# 🚆 IRCTC Railway Management System API

Welcome to the **IRCTC Railway Management System API**!  
This project simulates a real-world railway booking platform like IRCTC, providing functionalities for both **users** and **admins** to manage train schedules, seat bookings, and availability.

---

## 🌟 **API Workflow in Action**

![API Workflow](https://media.giphy.com/media/Ll22OhMLAlVDb8UQWe/giphy.gif)  
*Above is a representation of API workflows for user registration, train booking, and seat availability checks.*

---

## 🎯 **Problem Statement**

Your task is to design an **API** to:  
1. **Check Train Availability**: Retrieve train schedules and seat availability between two stations.  
2. **Book Seats**: Ensure concurrent booking with optimized race-condition handling.  
3. **Role-Based Access**: Secure admin operations and user bookings.  

Key Features:
- **Real-Time Traffic Handling**: Optimized to handle multiple simultaneous bookings.
- **Role Access**: Admin vs. User functionalities.
- **Secure Admin Endpoints**: Protected using API keys.
- **User Authentication**: JWT-based login system.

---

## 🛠️ **Tech Stack**

- **Backend Framework**: [Node.js](https://nodejs.org/) with [Express.js](https://expressjs.com/)  
- **Database**: [MySQL](https://www.mysql.com/)  
- **Authentication**: [JWT](https://jwt.io/) for secure session handling  
- **Encryption**: [bcrypt](https://www.npmjs.com/package/bcrypt) for passwords  
- **Environment Management**: [dotenv](https://www.npmjs.com/package/dotenv)  

---

## ⚙️ **Setup and Installation**

### Prerequisites
Ensure you have the following installed:
- **Node.js** (v14+)
- **MySQL** (or PostgreSQL)

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-repo/IRCTC_API.git
cd IRCTC_API
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Configure the Environment
Create a `.env` file and add the following variables:
```env
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=yourpassword
DB_NAME=irctc_db
JWT_SECRET=your_jwt_secret
API_KEY=your_admin_api_key
```

### Step 4: Set Up the Database
Run the following SQL commands to create the necessary tables:
```sql
CREATE DATABASE irctc_db;
USE irctc_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('user', 'admin') DEFAULT 'user'
);

CREATE TABLE trains (
    id INT AUTO_INCREMENT PRIMARY KEY,
    train_number VARCHAR(50) NOT NULL,
    source VARCHAR(255) NOT NULL,
    destination VARCHAR(255) NOT NULL,
    total_seats INT NOT NULL,
    available_seats INT NOT NULL
);

CREATE TABLE bookings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    train_id INT,
    seats INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (train_id) REFERENCES trains(id)
);
```

### Step 5: Start the Server
```bash
npm start
```
> The API will be live at `http://localhost:3000`.

---

## 🔗 **API Endpoints**

### User Routes
1. **Register**: `POST /user/register`  
2. **Login**: `POST /user/login`  
3. **Train Availability**: `GET /user/availability`  
4. **Book Seat**: `POST /user/book`  
5. **Get Booking Details**: `GET /user/getAllbookings`

### Admin Routes
1. **Add Train**: `POST /admin/addTrain`  
   > Requires `x-api-key` in headers.  
2. **Update Seats**: `PUT /admin/update-seats/:id`  

---

## 🚀 **Future Enhancements**

- Add a front-end using React.js for a seamless UI.
- Implement payment gateways for ticket purchases.
- Introduce train seat selection during booking.
- Add email notifications for booking confirmations.

---

## 🤝 **Contributing**

- Fork the repo  
- Create a new branch (`git checkout -b feature-name`)  
- Commit changes (`git commit -m "Add feature"`)  
- Push the branch (`git push origin feature-name`)  
- Create a Pull Request  

---

![API Flow GIF](https://media.giphy.com/media/L4FjRxANoi8LUxSDYx/giphy.gif)  

_**Happy Coding!**_ 🚀
