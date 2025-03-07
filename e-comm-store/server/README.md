# E-Commerce Backend Server

A robust REST API backend for an e-commerce platform built with Node.js, Express.js, and MongoDB.

## Features

- **User Authentication & Authorization**
  - JWT-based authentication
  - Role-based access control (Admin/User)
  - Secure password hashing with bcrypt

- **Product Management**
  - Complete CRUD operations
  - Product search and filtering
  - Category and brand filtering
  - Product reviews and ratings system
  - Inventory tracking

- **Order Management**
  - Order creation and tracking
  - Order status updates
  - Payment integration support
  - Shipping details management

## Tech Stack

- Node.js
- Express.js
- MongoDB with Mongoose
- JSON Web Tokens (JWT)
- bcryptjs for password hashing
- Cors for cross-origin resource sharing
- Morgan for HTTP request logging

## Prerequisites

- Node.js (v14 or higher)
- MongoDB (v4.4 or higher)
- npm or yarn package manager

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd server
```

2. Install dependencies:
```bash
npm install
```

3. Create a .env file in the root directory:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/ecommerce
JWT_SECRET=your-jwt-secret-key-here
```

4. Start the development server:
```bash
npm run dev
```

## API Documentation

### Authentication Endpoints

#### Register User
- **POST** `/api/auth/register`
- Body:
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "yourpassword"
}
```

#### Login
- **POST** `/api/auth/login`
- Body:
```json
{
  "email": "john@example.com",
  "password": "yourpassword"
}
```

#### Get User Profile
- **GET** `/api/auth/profile`
- Headers: `Authorization: Bearer <token>`

#### Update Profile
- **PUT** `/api/auth/profile`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "name": "Updated Name",
  "email": "updated@example.com",
  "password": "newpassword"
}
```

### Product Endpoints

#### Get All Products
- **GET** `/api/products`
- Query Parameters:
  - page (default: 1)
  - limit (default: 10)
  - category
  - brand
  - search

#### Get Single Product
- **GET** `/api/products/:id`

#### Create Product (Admin only)
- **POST** `/api/products`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "name": "Product Name",
  "description": "Product Description",
  "price": 99.99,
  "category": "Electronics",
  "brand": "Brand Name",
  "imageUrl": "image-url",
  "countInStock": 10
}
```

#### Update Product (Admin only)
- **PUT** `/api/products/:id`
- Headers: `Authorization: Bearer <token>`

#### Delete Product (Admin only)
- **DELETE** `/api/products/:id`
- Headers: `Authorization: Bearer <token>`

#### Add Product Review
- **POST** `/api/products/:id/reviews`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "rating": 5,
  "review": "Great product!"
}
```

### Order Endpoints

#### Create Order
- **POST** `/api/orders`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "orderItems": [
    {
      "product": "product_id",
      "name": "Product Name",
      "quantity": 2,
      "price": 99.99
    }
  ],
  "shippingAddress": {
    "address": "123 Street",
    "city": "City",
    "postalCode": "12345",
    "country": "Country"
  },
  "paymentMethod": "PayPal",
  "itemsPrice": 199.98,
  "shippingPrice": 10.00,
  "totalPrice": 209.98
}
```

#### Get All Orders (Admin only)
- **GET** `/api/orders`
- Headers: `Authorization: Bearer <token>`

#### Get My Orders
- **GET** `/api/orders/myorders`
- Headers: `Authorization: Bearer <token>`

#### Get Order by ID
- **GET** `/api/orders/:id`
- Headers: `Authorization: Bearer <token>`

#### Update Order Status (Admin only)
- **PUT** `/api/orders/:id/status`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "status": "processing"
}
```

#### Update Order to Paid
- **PUT** `/api/orders/:id/pay`
- Headers: `Authorization: Bearer <token>`
- Body:
```json
{
  "id": "payment_id",
  "status": "completed",
  "update_time": "timestamp",
  "email_address": "payer@example.com"
}
```

## Error Handling

The API uses consistent error response format:
```json
{
  "message": "Error message here",
  "stack": "Error stack trace (only in development)"
}
```

## Development

Start the development server with hot reload:
```bash
npm run dev
```

For production:
```bash
npm start
```

## Security Features

- Password hashing using bcrypt
- JWT for secure authentication
- Protected routes with middleware
- CORS enabled
- Request logging
- Error handling middleware

## Project Structure

```
server/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── product.controller.js
│   │   └── order.controller.js
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Product.js
│   │   └── Order.js
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── product.routes.js
│   │   └── order.routes.js
│   └── index.js
├── .env
├── package.json
└── README.md
```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the ISC License.
