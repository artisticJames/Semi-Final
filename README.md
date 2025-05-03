# 🛒 E-commerce Microservices – Step-by-Step Guide

This project is a simple e-commerce system built using **Node.js**, **Express**, and **MongoDB**, structured as three independent microservices:

- 🧑‍💼 **User Service** – Manages users
- 📦 **Product Service** – Manages products
- 📑 **Order Service** – Places and stores orders by interacting with the User and Product services

---

## 📁 Folder Structure

```
ecommerce-microservices/
├── user-service/
├── product-service/
└── order-service/
```

Each folder contains its own Express server, models, routes, and runs independently.

---

## 🛠️ Prerequisites

- Node.js (v16 or later)
- MongoDB (running locally or cloud instance like MongoDB Atlas)
- Postman (or similar API testing tool)
- Terminal with script permissions (fix PowerShell issues if needed)

---

## 🚀 Setup & Run Services

> Repeat the following steps **in separate terminal windows** for each service.

### 1. Clone the Repository (or set up project folders)

```bash
cd ecommerce-microservices
```

### 2. Install Dependencies

Navigate to each service and install required modules:

```bash
cd user-service
npm install express mongoose
```

Do the same for `product-service` and `order-service` with:

```bash
cd product-service
npm install express mongoose
```

```bash
cd order-service
npm install express mongoose axios
```

---

## ▶️ Start Each Service

In separate terminal tabs or windows:

```bash
# Terminal 1
cd user-service
node server.js
# => Running at http://localhost:3001
```

```bash
# Terminal 2
cd product-service
node server.js
# => Running at http://localhost:3002
```

```bash
# Terminal 3
cd order-service
node server.js
# => Running at http://localhost:3003
```

---

## 📬 Testing with Postman

### 1. Add a User

```http
POST http://localhost:3001/users
Content-Type: application/json

{
  "name": "Juan",
  "email": "juan@example.com",
  "password": "1234"
}
```

Save the returned `_id` as `userId`.

---

### 2. Add a Product

```http
POST http://localhost:3002/products
Content-Type: application/json

{
  "name": "Laptop",
  "price": 40000,
  "stock": 10
}
```

Save the returned `_id` as `productId`.

---

### 3. Place an Order

```http
POST http://localhost:3003/orders
Content-Type: application/json

{
  "userId": "PUT_USER_ID_HERE",
  "productId": "PUT_PRODUCT_ID_HERE"
}
```

> You should receive a response with `order`, `user`, and `product` data combined.

---

## 🔄 How It Works

1. **User creates an account** via the User Service.
2. **Product is added** via the Product Service.
3. **Order Service**:
   - Takes `userId` and `productId`
   - Fetches user and product from respective services
   - Saves a new order to its own DB
   - Responds with combined data

---

## 🧪 Verifying Independently

You can also use GET routes to verify:

- `GET http://localhost:3001/users/{userId}`
- `GET http://localhost:3002/products/{productId}`

---

## ✅ Final Tips

- Ensure MongoDB is running.
- Use Postman collections to organize your API tests.
- Each service can run independently — scale or update them without affecting others.
